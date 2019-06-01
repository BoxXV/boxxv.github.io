---
layout: post
title: Formatting xml layout trong Android Studio
subtitle: Formatting xml layout files for Android
image: /img/hello_world.jpeg
---

Hôm nay tôi phát hiện ra trình formatting xml trong Android Studio, thử nghiệm với nó một chút và tôi đã rất hài lòng với nó cho đến nay. Tôi tuân theo các quy tắc nghiêm ngặt trong việc formatting các tệp xml để tăng khả năng đọc (một phần quan trọng để đánh giá mã cho tôi) và cho đến nay tôi đã formatting các thuộc tính theo cách thủ công và theo trí nhớ nhưng nó sẽ rất tốt để tự động.

### Formatting xml layout files

Các quy tắc tôi tuân theo là tùy ý và tùy chọn cá nhân, nhưng một điều tôi thấy quan trọng về formatting code là nó xảy ra, không chính xác các quy tắc là gì. Miễn là mọi thứ đều nhất quán, khả năng đọc sẽ được cải thiện.

Quy tắc của tôi là như sau:

- xmlns (tất cả các name spaces được sử dụng, được sắp xếp theo thứ tự abc)

Để tập trung hơn vào các tags thực tế và thuộc tính, tôi khai báo name space android ở trên cùng như là:
```java
xmlns:a=”http://schemas.android.com/apk/res/android
```
Điều này sẽ được theo sau bởi tất cả các name spaces khác được sử dụng trong tệp, ví dụ: tools, app, custom, .v.v. được sắp xếp theo thứ tự abc

- id
- style
- layout_width
- layout_height
- layout_weight
- all other layout_* attributes
- all other android: attributes except what follows below
- text attributes (textColor, etc.) with the actual text last
- background
- orientation
- visibility
- elevation
- all other name space attributes, sorted alphabetically


Tham khảo:
- [Formatting xml layout files for Android](https://medium.com/@VeraKern/formatting-xml-layout-files-for-android-47aec62722fc)