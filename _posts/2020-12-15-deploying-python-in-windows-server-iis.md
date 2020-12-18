---
layout: post
title: Deploy Python on Windows Server IIS
subtitle: How to Deploy Python on Microsoft Windows Server IIS
tags:
- Anaconda
- Miniconda
- Conda
- Python
- FreeCAD
- Flask
- Django
- Docker
- Windows
- IIS
- CGI
- FastCGI
---

Động lực cho bài viết này đến sau khi trải qua một thời gian dài theo đuổi trên các diễn đàn khác nhau, github how-to-dos và tìm hiểu một số điều mới và cuối cùng lưu trữ API REST của dự án của tôi được viết bằng Python với PostgreSQL là back end trong IIS thành công.

Hy vọng bài viết này bao gồm những chi tiết nhỏ mà tôi tìm thấy và hữu ích cho bất kỳ ai đang theo đuổi.

-----

# Flask on IIS

Mặc dù Windows Server thường không phải là hệ điều hành ưa thích của tôi để triển khai web [sites|services] dựa trên Python, nhưng đôi khi tình huống này lại dẫn đến điều đó. Đối với những tình huống xảy ra như vậy, tôi vẫn thường sử dụng Apache bằng mod_python cho đến bây giờ. FastCGI tương đối dễ thiết lập trên Windows Server 2012R2 và IIS bằng Microsoft Web Platform Installer.

(LƯU Ý: Tôi đang sử dụng Flask, nhưng bất kỳ ứng dụng Python nào tương thích với WSGI sẽ hoạt động theo cùng một cách)

## Cài đặt IIS

Bạn cần đảm bảo rằng IIS được cài đặt và định cấu hình với dịch vụ vai trò CGI (điều này cũng cho phép FastCGI).




-----

# Deploying Flask app on IIS

Những bài học quan trọng mà tôi đã có khi thực hiện dự án này:

1. Thật dễ dàng để lưu trữ một tập lệnh flask qua IIS trên máy tính xách tay cá nhân của bạn. Nhưng với một máy chủ web được lưu trữ trong giới hạn của chính sách bảo mật mạnh mẽ thì không.

2. `pip install` không phải lúc nào cũng hoạt động và trong một số trường hợp khi máy chủ mục tiêu của bạn không được kết nối với internet, bạn cần tìm cách cài đặt ngoại tuyến.

3. Quyền của người dùng để thiết lập điều này là tối quan trọng. Chỉ cần xác nhận từ quản trị viên máy chủ rằng ID của bạn có đặc quyền máy cục bộ hoặc là một phần của nhóm quản trị viên là không đủ.

## Cơ sở hạ tầng của tôi để thiết lập:

| Server Operating System | Windows Server 2012              |
|-------------------------|----------------------------------|
| IIS version             | 8.5                              |
| Python version          | 3.6.3 on a virtual environment   |
| wfastcgi package        | 3.0.0                            |
| Web server serving on   | https port (443)                 |


{% highlight js %}
> node -v
v10.16.0

> npm -v
6.9.0
{% endhighlight %}




-----
### X. Resources
Dưới đây là một bản tóm tắt các tài nguyên bạn sẽ sử dụng trong khi làm việc thông qua sự khởi đầu nhanh chóng này. Các liên kết này cũng được cung cấp trong các bước dưới đây:
- Tải xuống và cài đặt: [Node.js](https://nodejs.org) (Điều này bao gồm npm) Sử dụng phiên bản "Recommended For Most Users".
- [video.js generator](https://github.com/videojs/generator-videojs-plugin)
- [video.js plugin conventions](https://github.com/videojs/generator-videojs-plugin/blob/master/docs/conventions.md)
- [Getting started with npm](https://docs.npmjs.com)
- [The yeoman scaffolding tool](https://yeoman.io)
- [Step-by-Step: Video.js Plugin Generator](https://support.brightcove.com/step-step-videojs-plugin-generator)
- [Step-by-Step: Plugin Development](https://support.brightcove.com/step-step-plugin-development)
- [Creating a videojs plugin](https://rants.broonix.ca/creating-a-videojs-plugin)
- [Tutorial plugins - Video.js Documentation](https://docs.videojs.com/tutorial-plugins.html)
- [Video.js Plugins](https://github.com/videojs/Video.js/blob/master/docs/guides/plugins.md)
- [Feature Spotlight: Advanced Plugins](https://blog.videojs.com/feature-spotlight-advanced-plugins/)
- [Plugins](https://docs.videojs.com/docs/guides/plugins.html)
- [Pass Data to the Plugin](https://support.brightcove.com/pass-data-plugin)

