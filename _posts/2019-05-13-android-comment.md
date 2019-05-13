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

Một chú thích trong Android phải đứng trước khai báo lớp (class), trường, hàm tạo hoặc phương thức. Nó được tạo thành từ hai phần: một mô tả theo sau là các block tags. Trong ví dụ này, các block tags là `@param`, `@return` và `@see`.
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
