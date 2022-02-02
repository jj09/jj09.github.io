I started this blog in 2013. My first year in the USA, while I was in Grad School. It’s almost 10 years ago! I started a blog mostly, to improve my English and for documenting my own learnings.

I decided to use WordPress for my blog as it was a to-go platform for beginners back then.

I don’t remember where I initially hosted it…but I moved it to Azure App Service in 2014(?) when I started working for Microsoft. Since then I did many improvements:
* Added custom domain: jj09.net
* Created web job that was performing backup of all files + db
* Enabled comments with Disqus
* Added performance optimizations (minifications, image compressions, etc.) - all with WordPress plugins
* Added HTTPS with CloudFlare
* Enabled caching with CloudFlare
* Added SEO optimization
* Added Google Analytics

Later on, the web job was not needed anymore as App Service introduced Backup. They also introduced an in-app MySQL database, so I didn’t have to maintain a separate MySQL instance.

## WordPress to Jekyll migration
I wasted a lot of time trying to install the Jekyll Exported plugin.
It turns out, you don’t need it. With [this guide](https://dev.to/rupeshtiwari/importing-wordpress-or-blogger-blogs-to-jekyll-blog-mpg), it’s enough to use built in Wordpress export!

* [Jekyll Tutorial for Beginners](https://blog.webjeda.com/jekyll-guide/)
* [4 Steps To Migrate From WordPress To Jekyll ](https://blog.webjeda.com/wordpress-to-jekyll-migration/)
* [Migrae from Wordpress to Jekyll part 1](https://blog.floriancourgey.com/2018/11/migrate-from-wordpress-to-jekyll)
* [official docs - posts](https://jekyllrb.com/docs/posts/)

### Themes
* https://forever-jekyll.github.io/
    * https://jekyll-themes.com/forever-jekyll/
    * https://jessechen.net/
* http://www.jekyllnow.com/
    * https://jekyllthemes.io/theme/jekyll-now
* https://www.bodunhu.com/minimalist/
    * https://jekyll-themes.com/minimalist/
* https://chirpy.cotes.page/
    * https://jekyll-themes.com/chirpy/