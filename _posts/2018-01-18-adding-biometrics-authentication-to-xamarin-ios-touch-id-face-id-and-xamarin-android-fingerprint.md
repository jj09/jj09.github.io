---
layout: post
title: Adding biometrics authentication to Xamarin.iOS (Touch ID / Face ID) and Xamarin.Android
  (Fingerprint)
date: 2018-01-18 22:02:10.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- android
- AzureApp
- C#
- ios
- Xamarin
meta:
  _edit_last: '1'
  layout: default
  feature_size: blank
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  builder_switch_frontend: '0'
  dsq_thread_id: '6423576105'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/adding-biometrics-authentication-to-xamarin-ios-touch-id-face-id-and-xamarin-android-fingerprint/"
---
<p>One of the top <a href="http://aka.ms/azureapp">Azure App</a> users requests was to <a href="https://feedback.azure.com/forums/568069-azure-mobile-app/suggestions/19251607-add-touch-id-support">add Touch ID support</a> for additional security. In this post I will share the details of implementing biometrics authentication for iOS and Android with Xamarin.</p>
<p>There are three aspects of biometrics auth:<br />
1. Enable user to turn biometrics authentication on and off. Users shouldn't be forced to use this additional security feature.<br />
2. Detecting when user should be asked for biometrics authentication, e.g., when app is coming from background, and when app is starting.<br />
3. Authentication process. Includes detecting hardware capabilities (is touch or face id available?), and local setup (does user configured local authentication in system settings).</p>
<p>Enabling biometrics authentication usually can be controlled in settings (like in Outlook or OneDrive). We did the same in Azure App:</p>
<p><img class="aligncenter size-full wp-image-19453" src="{{ site.baseurl }}/assets/2018/01/RequireTouchIdSettings-e1514930926880.png" alt="Require Touch ID Settings" width="350" height="623" /></p>
<h3>iOS</h3>
<p>Detecting when user is switching back to our app in iOS is pretty simple. Every time when user switch from background, method <code>WillEnterForeground</code> in <code>AppDelegate</code> is being called. We just need to override it with our custom implementation:</p>

{% highlight csharp %}
public override void WillEnterForeground(UIApplication application)
{
    // biometrics authentication logic here
}
{% endhighlight %}

<p>You should also authenticate user when app is being launched. In that case authentication should be performed in your initial view controller.</p>
<p>In iOS we have 2 kinds of biometrics authentication:<br />
1. Touch ID<br />
2. Face ID (available from iPhoneX)</p>
<p>We can also fallback to passcode if touch/face ID is not configured, or user's device does not support it.</p>
<p>The <a href="https://developer.xamarin.com/guides/ios/platform_features/introduction_to_touchid/#Adding_Touch_ID_to_your_application">iOS Local Auth API</a> is pretty straightforward, and well documented. I created simple helper to handle feature detection and authentication:</p>

{% highlight csharp %}
public static class LocalAuthHelper
{
    private enum LocalAuthType
    {
        None,
        Passcode,
        TouchId,
        FaceId
    }

    public static string GetLocalAuthLabelText()
    {
        var localAuthType = GetLocalAuthType();

        switch (localAuthType)
        {
            case LocalAuthType.Passcode:
                return Strings.RequirePasscode;
            case LocalAuthType.TouchId:
                return Strings.RequireTouchID;
            case LocalAuthType.FaceId:
                return Strings.RequireFaceID;
            default:
                return string.Empty;
        }
    }

    public static string GetLocalAuthIcon()
    {
        var localAuthType = GetLocalAuthType();

        switch (localAuthType)
        {
            case LocalAuthType.Passcode:
                return SvgLibrary.LockIcon;
            case LocalAuthType.TouchId:
                return SvgLibrary.TouchIdIcon;
            case LocalAuthType.FaceId:
                return SvgLibrary.FaceIdIcon;
            default:
                return string.Empty;
        }
    }

    public static string GetLocalAuthUnlockText()
    {
        var localAuthType = GetLocalAuthType();

        switch (localAuthType)
        {
            case LocalAuthType.Passcode:
                return Strings.UnlockWithPasscode;
            case LocalAuthType.TouchId:
                return Strings.UnlockWithTouchID;
            case LocalAuthType.FaceId:
                return Strings.UnlockWithFaceID;
            default:
                return string.Empty;
        }
    }

    public static bool IsLocalAuthAvailable => GetLocalAuthType() != LocalAuthType.None;

    public static void Authenticate(Action onSuccess, Action onFailure)
    {
        var context = new LAContext();
        NSError AuthError;

        if (context.CanEvaluatePolicy(LAPolicy.DeviceOwnerAuthenticationWithBiometrics, out AuthError)
            || context.CanEvaluatePolicy(LAPolicy.DeviceOwnerAuthentication, out AuthError))
        {
            var replyHandler = new LAContextReplyHandler((success, error) =>
            {
                if (success)
                {
                    onSuccess?.Invoke();
                }
                else
                {
                    onFailure?.Invoke();
                }
            });

            context.EvaluatePolicy(LAPolicy.DeviceOwnerAuthentication, Strings.PleaseAuthenticateToProceed, replyHandler);
        }
    }

    private static LocalAuthType GetLocalAuthType()
    {
        var localAuthContext = new LAContext();
        NSError AuthError;

        if (localAuthContext.CanEvaluatePolicy(LAPolicy.DeviceOwnerAuthentication, out AuthError))
        {
            if (localAuthContext.CanEvaluatePolicy(LAPolicy.DeviceOwnerAuthenticationWithBiometrics, out AuthError))
            {
                if (GetOsMajorVersion() >= 11 && localAuthContext.BiometryType == LABiometryType.TypeFaceId)
                {
                    return LocalAuthType.FaceId;
                }

                return LocalAuthType.TouchId;
            }

            return LocalAuthType.Passcode;
        }

        return LocalAuthType.None;
    }

    private static int GetOsMajorVersion()
    {
        return int.Parse(UIDevice.CurrentDevice.SystemVersion.Split('.')[0]);
    }
}
{% endhighlight %}

<p>There are helper methods determining proper label (<code>GetLocalAuthLabelText</code>), icon (<code>GetLocalAuthIcon</code>) and authentication text (<code>GetLocalAuthUnlockText</code>) depending on available authentication type. There is also one liner <code>IsLocalAuthAvailable</code> checking if Local Authentication (face/touch ID or passcode) is available, and <code>Authenticate</code> method that performs authentication, which takes <code>success</code> and <code>failure</code> callbacks as parameters. It can be used in <code>WillEnterForeground</code> method as follows:</p>

{% highlight csharp %}
public override void WillEnterForeground(UIApplication application)
{
    if (!AppSettings.IsLocalAuthEnabled)
    {
        return;
    }

    LocalAuthHelper.Authenticate(null, // do not do anything on success
    () =>
    {
        // show View Controller that requires authentication
        InvokeOnMainThread(() =>
        {
            var localAuthViewController = new LocalAuthViewController();
            Window.RootViewController.ShowViewController(localAuthViewController, null);
        });
    });
}
{% endhighlight %}

<p>We do not have to do anything on success. The popup shown by iOS will disappear and user will be able to use the app. On failed authentication though we should display some kind of shild (e.g., ViewController) that prevent user from using the app until authorization succeed. This is how it looks in Azure App:</p>
<p><img class="aligncenter size-full wp-image-19464" src="{{ site.baseurl }}/assets/2018/01/AzureAppUnlockWithTouchId-e1515522992230.png" alt="Azure App - Unlock with Touch ID" width="300" height="534" /></p>
<h3>Android</h3>
<p>Detecting when app is coming from background in Android is tricky. There is no single method that is invoked only when app is coming back from background. The <code>OnResume</code> method is being called when app is coming back from the background, but it's also called when you switch from one activity to another. Solution for that is to keep a time stamp with last successful authentication, and update it to <code>DateTime.Now</code> every time when activity is calling <code>OnPause</code>. This happen when app is going to background, but also when app is changing between activities. Thus we cannot simply set flag <code>Background=true</code> when <code>OnPause</code> is called. However, when difference between subsequent <code>OnPause</code> and <code>OnResume</code> is larger than some period of time (e.g., more than a few seconds) we can assume that app went to background. Below code should be implemented in some <code>BaseActivity</code> class that all activities inherit from:</p>

{% highlight csharp %}
public class BaseActivity
{
  public const int FingerprintAuthTimeoutSeconds = 5;
  public static DateTime LastSuccessfulFingerprintAuth = DateTime.MinValue;
    
  protected override void OnResume()
  {
    base.OnResume();

    if (IsFingerprintAvailable() && LastSuccessfulFingerprintAuth > DateTime.Now.AddSeconds(-FingerprintAuthTimeoutSeconds))
    {
      StartActivity(typeof(FingerprintAuthActivity));
    }
  }

  protected override void OnPause()
  {
    base.OnPause();

    if (IsFingerprintAvailable())
    {
      LastSuccessfulFingerprintAuth = DateTime.Now;
    }
  }
}
{% endhighlight %}

<p>The basics of Fingerprint authentication are very well described in <a href="https://developer.xamarin.com/guides/android/platform_features/fingerprint-authentication/">Xamarin docs</a>.</p>
<p>Even better reference is a sample app <a href="https://github.com/xamarin/monodroid-samples/tree/master/FingerprintGuide">FingerprintGuide</a> from Xamarin.</p>
<p>The main disadvantage of adding fingerprint authentication in Android (over Face/Touch ID in iOS) is requirement to build your own UI and logic for the authentication popup. This includes adding icon, and handling all authentication results. iOS handles incorrect scan, and displays popup again with passcode fallback after too many unsuccessful tries. In Android you have to implement this entire logic by yourself.</p>
<h3>Summary</h3>
<p>Adding biometrics authentication is useful for apps that hold sensitive data, like banking apps, file managers (Dropbox, OneDrive), or an app that has access to your Azure Resources :)</p>
<p>Implementing local authentication in iOS is pretty straightforward, and iOS APIs provide authentication UI for free. In Android however, the APIs are only working with the backend, and UI has to be implemented by you.</p>
<p>Local authentication should be always optional. Some users may not need nor want it. Thus, it should be configurable in the app settings.</p>
<p>Try out biometrics auth in Azure App!</p>
<p><a href="https://itunes.apple.com/us/app/microsoft-azure/id1219013620?ls=1&mt=8"><img src="{{ site.baseurl }}/assets/2018/01/appstore.png" alt="Download on the App Store" width="200" height="59" class="aligncenter size-full wp-image-18061" /></a><br />
<a href="https://play.google.com/store/apps/details?id=com.microsoft.azure"><img src="{{ site.baseurl }}/assets/2018/01/playstore.png" alt="Get it on Google Play" width="200" height="59" class="aligncenter size-full wp-image-18071" /></a></p>
