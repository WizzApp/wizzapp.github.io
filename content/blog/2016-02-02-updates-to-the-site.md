---
title: "Updates to the Site"
date: 2016-02-02
tags: [blogging]
RedirectFrom: blog/2016/02/02/updates-to-the-site/*
---

Since changing the layout of the blog I also did some optimizations to enhance it a little bit. Most of those enhancements were proposed by Google PageSpeed, another one I took from the theme setup pages of the used theme, others are more or less mandated by law ;-).

So what did I do?

* I optimized the used feature image and my "avatar" using [jpegtran](http://jpegclub.org/) which decreased the initial file size by about 10 percent for each image.
* I changed my Nginx config to send out _Cache-Control_ and _Expires_ headers for all static assets set to 1 year from request. Here is the config snippet I added to the corresponding server directive:

{% highlight Nginx %}
location ~\* \.(js|css|png|jpg|jpeg|gif|ico)$ {
expires 1y;
}
{% endhighlight %}

* I added the async attribute to some of the locally hosted scripts to hopefully shave of a little time by asynchronously executing scripts.
* I also added a basic cookie consent notification using [Cookie Consent](https://silktide.com/tools/cookie-consent/) and a little cookie policy site (located [here](/cookiepolicy/)). The text is more or less shamelessly stolen from [Silktides own privacy policy site](https://silktide.com/privacy-policy/).
* Next I added support for responsive images using the [Jekyll Picture Tag](https://github.com/robwierzbowski/jekyll-picture-tag) plugin suggested in the original [theme setup pages](https://mmistakes.github.io/minimal-mistakes/theme-setup/) of the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme.
* And last but not least I added [Jekyll HTML compression](https://github.com/penibelst/jekyll-compress-html) to compress the generated HTML just a little bit. This reduces the index page by about 1570 bytes (which is by about 16 percent) using the following settings:
  {% highlight Yaml %}
  compress_html:
  clippings: all
  comments: ["<!-- ", " -->"]
  endings: all
  ignore:
  envs: []
  blanklines: false
  profile: false
  startings: [html, head, body]
  {% endhighlight %}
  It's not much, but it's not bad either and it depends on what markup to original markdown document contains, so numbers will differ.

All in all those are all just micro optimizations but I learned some new stuff and I won't have to do it in the future.
