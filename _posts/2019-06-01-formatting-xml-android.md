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

Danh sách này không đầy đủ tất cả các thuộc tính nhưng nó bao gồm những thuộc tính tôi sử dụng nhiều nhất, mà tôi muốn thấy được nhóm hoặc ở một vị trí nhất định và nó đủ. Tôi vẫn còn trên hàng rào về độ cao nhưng nó đã được thêm vào gần đây (tôi đã viết hướng dẫn của mình vào tháng 10 năm 2012) rằng tôi đã không biết nên đặt nó ở đâu để nó di chuyển xuống đáy. Các thuộc tính như `gravity` và `padding` được bao phủ bởi tất cả các thuộc tính khác và tôi hầu như bỏ qua các quy tắc rõ ràng ở đây bên cạnh việc phân nhóm các `padding` cho đến nay vì nỗ lực thủ công sẽ quá nhiều. Không còn nữa!

### The xml formatter in Android Studio

Trình định dạng xml (Tôi không biết phiên bản Android studio nào đã thêm phiên bản mở rộng này nhưng có trong Android Studio 2.1.1) bằng cách mở `Preferences` (Command +,), sau đó chuyển đến `Editor -> Code Style -> XML`. Có bốn tab, `Arrangement` sẽ cho phép bạn xác định thứ tự các attributes. (Bạn cũng có thể xác định thứ tự cho các thẻ. Điều này có ý nghĩa đối với các tệp chứa các giá trị độ phân giải khác nhau như dimen, số nguyên, bool nhưng tôi đã giành chiến thắng ở đây. Tôi thích giữ các tệp đó trong các tệp giá trị riêng cho hầu hết các phần.)

![placeholder](/img/formatting-xml-android.png "Editor -> Code Style -> XML \ Arrangement Tab")_Editor -> Code Style -> XML \ Arrangement Tab_

Bạn có thể thêm, xóa và di chuyển từng hàng khi bạn cần chúng. Theo quy tắc của tôi, tôi bắt đầu với các namespaces. Tôi rõ ràng đặt `xmlns:a` đầu tiên, chủ yếu là cho rõ ràng, tôi nghi ngờ tôi sẽ bao giờ có `xmlns:aa` cho bất cứ điều gì. Sau đó, các attributes dự kiến theo danh sách trên. Với điều này được tự động hóa bây giờ tôi đã lấy tự do để đảm bảo các định nghĩa lề và phần đệm tuân theo thứ tự css và tất cả các thuộc tính namespace Android được chuyển xuống dưới cùng, được sắp xếp theo thứ tự bảng chữ cái. Có lẽ nếu tôi có nhiều người trong số họ tại một số điểm, tôi sẽ chính xác hơn ở đây.

Phần khó khăn duy nhất là phần giữa, nơi tôi muốn tất cả các attributes Android khác nhưng một số và sau đó là tất cả các `text*` ngoại trừ `android:text` mà tôi muốn là thuộc tính cuối cùng của nhóm văn bản.

### Share your rules

Formatting  tệp thậm chí còn có ý nghĩa hơn khi nhiều người đang làm việc trên một dự án, vì vậy tất nhiên bạn nên chia sẻ quy tắc formatting của mình với nhóm của mình.

Nhấp vào nút “Manage…” của các ứng dụng khác nhau cung cấp cho bạn để `export` kiểu định dạng của bạn. Trong Android Studio 2.2, người khác có thể nhập tệp này thông qua tính năng `import`. Điều này không tồn tại trong các phiên bản Android Studio trước đó. Để sử dụng kiểu định dạng xml được xác định trong các phiên bản đó, hãy truy cập `~/Library/Preferences` và chọn phiên bản Android Studio bạn đang sử dụng. Nếu bạn tìm thấy một thư mục có tên là `codeststyle`, hãy dán tệp xml được chia sẻ của bạn vào đó. Nếu không có thư mục đó, hãy tạo nó và sau đó dán tệp. Khởi động lại Android Studio, đi đến trình định dạng và tệp sẽ hiển thị trong trình đơn thả xuống bên cạnh “Manage…”

Happy formatting!


Tham khảo:
- [Formatting xml layout files for Android](https://medium.com/@VeraKern/formatting-xml-layout-files-for-android-47aec62722fc)