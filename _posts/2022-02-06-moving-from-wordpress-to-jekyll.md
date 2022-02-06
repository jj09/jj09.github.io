---
layout: post
title: Moving from WordPress to Jekyll
categories: 
    - blog
published: true
status: publish
date: 2022-02-06 10:59:24.000000000 -08:00
permalink: "/moving-from-wordpress-to-jekyll/"
---
<div style="text-align: center;"><img src="{{ site.baseurl }}/assets/2022/wordpress-to-jekyll-migration.png" alt="WordPress to Jekyll migration" /></div>

## Brief story of this blog and why WordPress

I started this blog in 2013. It was my first year living in the USA. I was in Grad School at the time. It has been almost 10 years! I started this blog mostly to improve my English and for documenting my own learnings. I decided to use WordPress as it was a to-go platform for beginners back then. I need to admit, it was pretty neat and straighforward to setup.

Intially I was hosting my blog on webio.pl (that was BC time - Before Cloud). I [moved it to Azure App Service in 2014]({{ site.baseurl }}/moving-wordpress-blog-azure-webio-hosting/) (it was called Azure Website back then). I did many tweaks and improvements since then:
* Added Google Analytics
* Added custom domain: jj09.net
* Created web job that was performing backup of all files + database
* Enabled comments with Disqus
* Added performance optimizations (minifications, image compressions, etc.) - all with WordPress plugins
* Added HTTPS with Cloudflare
* Enabled caching with Cloudflare
* Added SEO optimization

Later on, the web job was not needed anymore as App Service introduced Backup. In Azure I trust I thought. Azure also introduced an in-app MySQL database, so I didn’t have to maintain a separate MySQL instance. Yay! Everything is great. Database was backed up together with App Service instance. Nice!

I was super cautious and I was also making a copy of a database backup periodically and putting it on Dropbox.

## WordPress blog needs to be maintained

For last 2 years I didn't do much blogging, and I didn't do much maintenance neither. I didn't even bother to update plugins or WordPress version.

It was always bothering me though when I was seeing these "update available" upsells. Should I do it now? What am I getting? Do I care? Am I willing to risk an hour if something goes wrong? Will I even know whether something went wrong?

Some time ago I started seeing a big red warning asking me to upgrade to PHP 7. My blog was using PHP 5.6 (default from App Service). Everything was working so I ignored it.

## WordPress to Jekyll migration

I was thinking about migrating from WordPress to Jekyll for [some time](https://twitter.com/realJacobJed/status/1359244127443902465?s=20&t=mZxQPCGlbJ_-qxYWHi2PHQ). Why? It seemed much simpler to maintain (just static pages, no database), and cheaper (AKA free) when you host in Github Pages! 

I started with [4 Steps To Migrate From WordPress To Jekyll](https://blog.webjeda.com/wordpress-to-jekyll-migration/), and first step was to export my current content with [Jekyll Exporter plugin](https://wordpress.org/plugins/jekyll-exporter/). I wasted a lot of time on that step. First, it turned out that I couldn't install the plugin as it required more recent PHP version. As I had backups I just went and upgraded PHP. After that none of my posts didn't show up :O

I freaked out a little so I went to restore backup. After that, I loded my home page and...WordPress asked me to setup my blog!!! My heart rate spiked. The last database backup I had was from 2018 :( I went to backup settings and it looked like backing up database was unchecked :(

<div style="text-align: center;"><img src="{{ site.baseurl }}/assets/2022/azure-backup-configuration.jpg" alt="Azure Backup Database configuration" /></div>

I tried to use previous backup (from day before), and...it worked fine. It restored database! Yay...but WTF?! I quickly copied database to my Dropbox, just in case, and upgraded PHP version again. After second attempt I went and installed Jekyll Exporter, but I couldn't export my stuff because of timeouts. I tried to play with [`set_time_limit`](https://thimpress.com/knowledge-base/how-to-increase-maximum-execution-time-for-wordpress-site/), but no luck. I screwed up my WordPress instance a few times along the way, and I had to restore backup a few times. **It always took 2 restores to properly restore the in-app MySQL database**! This convinced me that my current setup is too fragile to keep it that way and I need to migrate to Jekyll now. I actually started this effort with plan to just export WordPress to Jekyll format, and see how much work it's gonna be to do the migration. Plan changed: I'm doing migration :)

I found out another [WordPress -> Jekyll migration guide](https://dev.to/rupeshtiwari/importing-wordpress-or-blogger-blogs-to-jekyll-blog-mpg), and discovered that it’s enough to use built-in Wordpress export! From now on, migration was very smooth. I followed README from [Forever Jekyll theme](https://github.com/forever-jekyll/forever-jekyll) (theme I chose) and [Importing WordPress or Blogger Blogs to Jekyll Blog](https://dev.to/rupeshtiwari/importing-wordpress-or-blogger-blogs-to-jekyll-blog-mpg) mentioned above.

List things I did (and to be done as I'm done yet):

- [x] Export wordpress.xml (easy)
- [x] Rename posts from .html to .md (easy with simple node script)
- [x] Migrate syntax highlighting tags: `<pre>` to `\{\% highlight \%\}` (I did it manually instead of writing a script, as I had multiple variations of code snippets and wanted to fix text formatting along the way)
- [x] setup domain
    * [github guide](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
    * [pages settings](https://github.com/jj09/jj09.github.io/settings/pages)
    * [How to setup google domain for github pages](https://dev.to/trentyang/how-to-setup-google-domain-for-github-pages-1p58)
- [x] setup HTTPS (this took a few hours to get certificate through Github Pages)
    * [github FAQ](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
    * [troubleshooting](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages#https-errors)
    * [article](https://timeandupdate.com/2018/05/custom-domain-in-github-page-support-https/))
    * learnings:
        - map both A record and CNAME
        - I had to wait ~10h for cert to be issued, and to be able to  'Enforce HTTPS' in Github Pages settings
- [x] Add Google Analytics (easy)
- [x] migrate comments ([link](https://desiredpersona.com/disqus-comments-jekyll/), [link](https://jj09.disqus.com/admin/install/platforms/universalcode/))
- [ ] add buy me a coffee
- [ ] optimize perf ([Google Page Speed](https://pagespeed.web.dev/report?url=https%3A%2F%2Fjj09.net%2F))
    [ ] optimize images ([link](https://jetholt.com/automatic-image-optimisation/))
    [ ] have landing page like mfranc and dhh
    [ ] upgrade template to more performant?
- [ ] configure backup to Dropbox
- [ ] SEO

## Pros and Cons

After a few days with Jekyll I absolutely love it!

Pros:
- simplicity - just text files on Github
- no database
- no need to maintain Azure App Service
- free hosting on Github Pages <3
- much less fear of something going wrong and losing all my posts: one WordPress plugin update can corrupt Db, I don't care if I mess up my Jekyll setup as my posts are in .md files that won't be touched
- writing posts in MarkDown is much better! I prefered HTML over WordPress visual editor anyway. Writing posts/making changes is much faster (for me) using Jekyll than WordPress. I just open VSCode and have blog post readily available. In WordPress World I need to go to wp-admin, then posts, then find my post (multiple steps). Many times,  WordPress would mess up my HTML formatting, which was annoying. Now, I'm in control.
- can write posts offline
- editing themes is much easier: I just play with html/css without loging in to FTP

Cons:
- none **for me**! - people say that it's complicated for non-programmers, no CMS, no WYSWIG editor, but none of these are an issue **for me**

## References

### Migration and Jekyll guides

* [Why Jekyll over WordPress](https://blog.webjeda.com/why-jekyll-over-wordpress/)
* [Jekyll Tutorial for Beginners](https://blog.webjeda.com/jekyll-guide/)
* [4 Steps To Migrate From WordPress To Jekyll](https://blog.webjeda.com/wordpress-to-jekyll-migration/)
* [Migrae from Wordpress to Jekyll part 1](https://blog.floriancourgey.com/2018/11/migrate-from-wordpress-to-jekyll)
* [official docs - posts](https://jekyllrb.com/docs/posts/)
* [Hosting a website for free — Get started with Google Domains & Github Pages](https://medium.com/8px-magazine/hosting-a-website-for-free-get-started-with-google-domains-github-pages-980986550958)

### Cool themes
* https://jekyll-themes.com/forever-jekyll/ (https://github.com/forever-jekyll/forever-jekyll) 
* https://jekyllthemes.io/theme/jekyll-now
* https://jekyll-themes.com/minimalist/
* https://jekyll-themes.com/chirpy/
* https://jekyll-themes.com/developr/ 
* https://jekyll-themes.com/project-negya/ (hacker style)
* https://jekyll-themes.com/texture/
* https://jekyll-themes.com/premium/cocoa/
* https://jekyll-themes.com/premium/avocado/
* https://jekyll-themes.com/leaf/
* https://mfranc.com
* http://dyszkiewicz.me/

## Fun Fact

I first learned about Jekyll in 2014/2015 from my ex-MSFT coworker Justin Beckwith. During migration I recalled that he wrote a [blog post where he described his migration adventure](https://jbeckwith.com/2013/07/17/wordpress-to-jekyll). I wish I just used that guide from the beginning as it has everything what's needed :)