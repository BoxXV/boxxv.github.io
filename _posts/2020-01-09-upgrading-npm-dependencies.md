---
layout: post
title: Upgrading npm dependencies
subtitle: Cập nhật các thư viện phụ thuộc trong NPM
---

Làm thế nào chúng ta có thể nâng cấp một cách an toàn các phụ thuộc npm trong dự án của chúng ta? Các ký tự ^ và ~ có nghĩa là gì trước các phiên bản gói phụ thuộc? Làm thế nào chúng ta có thể nâng cấp phiên bản chính trên một phụ thuộc npm trong dự án của chúng ta? Chúng ta sẽ tìm ra trong bài viết này.

#### Version parts

phiên bản gói npm theo phiên bản ngữ nghĩa. Vì vậy, một phiên bản gói có 3 phần - Major.Minor.Patch

{% highlight js %}
> node -v
v10.16.0

> npm -v
6.9.0
{% endhighlight %}



-----
### X. Resources
Dưới đây là một bản tóm tắt các tài nguyên bạn sẽ sử dụng trong khi làm việc thông qua sự khởi đầu nhanh chóng này. Các liên kết này cũng được cung cấp trong các bước dưới đây:
- [Upgrading npm dependencies](https://www.carlrippon.com/upgrading-npm-dependencies/)