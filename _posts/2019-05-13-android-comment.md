---
layout: post
title: Comment trong Android
subtitle: Vì một tương lai lương Android cao hơn iOS
date: "2019-05-12"
tags:
- Android
- Comment
- Commenting Convention
- Coding Conventions
modified: 2019-05-13
---

A doc comment is written in HTML and must precede a class, field, constructor or method declaration. It is made up of two parts -- a description followed by block tags. In this example, the block tags are @param, @return, and @see.
```java
/**
 * Returns an Image object that can then be painted on the screen. 
 * The url argument must specify an absolute {@link URL}. The name
 * argument is a specifier that is relative to the url argument. 
 * <p>
 * This method always returns immediately, whether or not the 
 * image exists. When this applet attempts to draw the image on
 * the screen, the data will be loaded. The graphics primitives 
 * that draw the image will incrementally paint on the screen. 
 *
 * @param  url  an absolute URL giving the base location of the image
 * @param  name the location of the image, relative to the url argument
 * @return      the image at the specified URL
 * @see         Image
 */
 public Image getImage(URL url, String name) {
        try {
            return getImage(new URL(url, name));
        } catch (MalformedURLException e) {
            return null;
        }
 }
```



Tham khảo:
- [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html)
- [AOSP Java Code Style for Contributors](https://source.android.com/setup/contribute/code-style#use-javadoc-standard-comments)
