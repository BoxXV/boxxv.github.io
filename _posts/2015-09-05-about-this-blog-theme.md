---
layout:     post
title:      "About This Blog Theme"
description: This is a modified version of Clean Blog Jekyll to be compatible with GitHub Pages. Modified by Thanh Tran for his own blog.
date:       2015-09-05T14:53:26+07:00
author:     "Tran Trong Thanh"
image: "img/post-bg-02.jpg"
modified: 2015-09-20T11:29:15+07:00
---

# Clean Blog by Start Bootstrap - GitHub Pages Version

> This is a modified version of [Clean Blog Jekyll](https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll) to be compatible with [GitHub Pages](https://help.github.com/articles/using-jekyll-with-pages/). Modified by [Thanh Tran](https://github.com/trongthanh) for his own blog.

The official Jekyll version of the Clean Blog theme by [Start Bootstrap](http://startbootstrap.com/).

### [View Live Demo &rarr;](https://trongthanh.github.io/startbootstrap-clean-blog-jekyll)

## Changes from Original Jekyll Theme

+ Use SASS (SCSS flavor) instead of LESS, with minimal Bootstrap SCSS bundle
+ New choice of typography, remarkably Source Sans Pro for titles and Georgia for body texts
+ Support Vietnamese texts
+ Use client-side [Prism](http://prismjs.com) syntax highlighter (compatible with GitHub-flavored Markdown code fences) instead of pre-rendered Pygments
+ Include Google Analytics script tag. Set your GA ID at `site.gaid`
+ Include [Disqus](http://disqus.com) script to enable commenting. Set your Disqus site's ID at `site.disqus_site_id`. If not set, the comment section is omitted.
+ Full text search using Google site search. See _search.html_.
+ A compact posts archive (which list all published blog posts). I believe listing the post tittles is better than Search and it generate some sort of information scent.
+ Better image caption using `img + em` technique. See [this example](http://blog.int3ractive.com/startbootstrap-clean-blog-jekyll/2015/08/10/Muc-Toi-Thieu-Cua-Lap-Trinh-Vien-Front-End/)
+ Optional: To enable [automatic feed generation](https://help.github.com/articles/atom-rss-feeds-for-github-pages/) supported by GitHub Pages, remove or rename the _feed.xml_ file and add the following line to your site's *_config.yml* file:
```
gems:
	+ jekyll-feed
```
+ TODO: Facebook & Twitter metadata
+ TODO: Social network sharing integration
+ TODO: Add modified / update time using front matter or pushed time

## Before You Begin

In the _config.yml file, the base URL is set to /startbootstrap-clean-blog-jekyll which is this themes gh-pages preview. It's recommended that you remove the base URL before working with this theme locally!

It should look like this:
`baseurl: ""`

## What's Included

This Jekyll theme is customized to run well on GitHub Pages, therefore it must be built or previewed with `github-pages` gem to align the plugins and settings. Follow [this article](https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll) for enviroment installation. After that, you can start previewing the generated site with `bundle exec jekyll serve`.

A Grunt environment is also included. There are a number of tasks it performs like minification of the JavaScript, compiling of the SCSS files, adding banners to keep the Apache 2.0 license intact, and watching for changes. Run the grunt default task by entering `grunt` into your command line which will build the files. You can use `grunt watch` if you are working on the JavaScript or the SCSS.

You can also run `grunt serve` to watch for changes and test the blog in one command.

## Support

This theme is for my own blog which is customized with my own preferences. Issue reports are welcome but I may have little time to respond to questions or installation support. 

Besides, please visit Clean Blog's template overview page on Start Bootstrap at http://startbootstrap.com/template-overviews/clean-blog/ for extra info and comments.
