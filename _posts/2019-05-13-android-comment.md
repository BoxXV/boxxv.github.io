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
 * 
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

## TODO comments
Chúng ta nên viết chú thích TODO để lưu ý điều gì đó mà chúng ta sẽ làm trong fuction
```java
// TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception {
  return null;
}
```

## Warning of Consequence
Cảnh báo về hậu quả là tốt nếu chúng ta sử dụng chú thích để giải thích một số lý do đặc biệt
```java
public static SimpleDateFormat makeStandardHttpDateFormat() {
  // SimpleDateFormat is not thread safe,
  // so we need to create each instance independently.
  SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z");
  df.setTimeZone(TimeZone.getTimeZone("GMT"));
  return df;
}
```

## Explanation of Intent
Trong ví dụ dưới đây, sẽ tốt hơn nếu chúng ta có thể thay đổi giá trị trả về rõ ràng hơn. Nhưng khi nó là một phần của thư viện chuẩn hoặc trong mã mà bạn không thể thay đổi thì một chú thích về ý định có thể hữu ích
```java
assertTrue(a.compareTo(a) == 0); // a == a
assertTrue(a.compareTo(b) != 0);  // a != b
assertTrue(ab.compareTo(ab) == 0); // ab == ab
```

## Legal Comments
Chú thích pháp lý giúp người khác biết mã nguồn đến từ đâu và khi nào
```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```

Tham khảo:
- [Code Conventions for the Java Programming Language: Comments](https://www.oracle.com/technetwork/java/codeconventions-141999.html#385)
- [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html)
- [How to write comment (from Clean code book)](https://viblo.asia/p/how-to-write-comment-from-clean-code-book-1VgZv3nYlAw)
- [Source Code Comment Styling: Tips and Best Practices](https://www.hongkiat.com/blog/source-code-comment-styling-tips/)
