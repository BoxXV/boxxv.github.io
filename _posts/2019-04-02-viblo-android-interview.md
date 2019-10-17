---
layout: post
title: Một số câu hỏi phỏng vấn Android bạn nên lưu ý
subtitle: Vì một tương lai lương Android cao hơn iOS
tags:
- Android
- Interview
- Questions
- Answers
---
Sau đây là một số câu hỏi thường gặp khi đi phỏng vấn về vị trí lập trình Android mà mình tổng hợp lại được. Trước khi bước vào buổi phỏng vấn hãy review lại một lần nhé, biết đâu lại gặp phải "câu tủ". Mình sẽ bỏ qua một số câu hỏi định nghĩa cơ bản như `activity` là gì, hay liệt kê vòng đời của `activity` và `fragment`, ... mà tập trung vào các câu hỏi thường bị bỏ qua. Các câu trả lời sẽ tập trung vào các ý chính một cách vắn tắt, bạn có thể tìm hiểu chi tiết hơn sử dụng các từ khóa chính trong câu hỏi.

#### 1. Application là gì?
Lớp Application trong Android là lớp cơ sở trong ứng dụng Android chứa tất cả các component khác như activity và service. Lớp Application hoặc bất kỳ lớp con nào của lớp nó sẽ được khởi tạo trước bất kỳ lớp nào khác khi process cho ứng dụng của bạn được khởi tạo.

#### 2. Context là gì?
Một Context là một đối tượng để phục vụ các xử lý liên quan tới hệ thống hay cung cấp thông tin của môi trường hệ thống. Nó cung cấp các dịch vụ như để giải quyết resources, lấy quyền truy cập vào cơ sở dữ liệu và preferences, ... Context có thể được coi là thành phần xử lý về môi trường mà ứng dụng của bạn đang hoạt động trong đó. Application Context: là một context gắn liền với vòng đời của một ứng dụng. Application context có thể được sử dụng khi bạn cần một context có vòng đời riêng biệt với context hiện tại hoặc khi bạn truyền một context ra ngoài phạm vi hoạt động của một activity. Activity Context: context này là có sẵn ở trong một activity, nó gắn liền với vòng đời của activity này. Bạn nên sử dụng loại context này khi phạm vi hoạt động bạn cần chỉ ở trong activity này hay bạn cần một context có vòng đời gắn liền với context hiện tại.

#### 3. Tại sao bytecode không thể chạy được trong Android?
Bởi vì Android sử dụng DVM - Dalvik Virtual Machine (từ các phiên bản trước Lollipop) và ART - Android Runtime (chính thức từ phiên bản Lollipop trở lên, tuy nhiên nó đã được thông báo và cho dùng thử nghiệm từ phiên bản Kitkat) để thực thi chương trình chứ không sử dụng JVM (Java Virtual Machine).

#### 4. BuildType ở trong Gradle là gì? Nó được sử dụng với mục đích gì?
Các loại build định nghĩa những thuộc tính mà Gradle sử dụng khi xây dựng và đóng gói một ứng dụng Android.
- Build type xác định cách một module được xây dựng, ví dụ như có sử dụng ProGuard hay không, ...
- Product flavor xác định những gì sẽ được tạo ra, ví dụ như tài nguyên nào được bao gồm trong bản build.
- Gradle tạo ra một build variant cho mọi tổ hợp có thể có từ product flavor và build type trong dự án của bạn.

#### 5. Quá trình build một ứng dụng trong Android.
![placeholder](http://boxxv.com/img/android-build.png "Quá trình build một ứng dụng trong Android.")

#### 6. Ở trong activity, khi nào thì onDestroy() được gọi mà không có onPause() và onStop()?
Khi finish() được gọi ở trong phương thức onCreate() của activity đó, hệ thống sẽ gọi trực tiếp onDestroy().

#### 7. Tại sao chỉ nên gọi setContentView() trong onCreate() ở trong một activity?
Vì onCreate() chỉ được gọi tới một lần nên đây là thời điểm chúng ta nên khởi tạo hầu hết các yếu tố cần thiết. Nó sẽ không hiệu quả nếu ta gọi setContentView() ở trong onResume() hay onStart() (bởi chúng được gọi tới nhiều lần) vì setContentView() là một hoạt động tiêu tốn khá nhiều tài nguyên.

#### 8. Phân biệt Service, Intent Service, AsyncTask và Thread.
- Service là một thành phần được sử dụng để thực hiện các tác vụ ở background ví dụ như chơi nhạc. Nó không có giao diện người dùng (user interface). Service có thể chạy ở trong background vô thời hạn ngay cả khi ứng dụng bị hủy.
- AsyncTask cho phép bạn thực hiện các công việc bất đồng bộ ở background thread và publish kết quả lên trên UI thread mà không yêu cầu bạn phải xử lý cách các thread hay handler hoạt động.
- IntentService là một loại Service để xử lý lần lượt các yêu cầu bất đồng bộ (thông qua Intent) ở background thread. Client sẽ gửi yêu cầu thông qua việc gọi tới startService(Intent) và nó cũng không yêu cầu bạn phải "động tay động chân" tới việc xử lý thread / handler.
- Một Thread là một luồng thực thi tuần tự trong một chương trình. Thread có thể được coi là một mini-process chạy ở trong main process.


#### 
#### 
#### 


Tham khảo:
- [Voz: Tổng hợp các câu hỏi phỏng vấn Android Dev cho sinh viên mới ra trường](https://forums.voz.vn/showthread.php?t=7216185)
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 1)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 2)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-2-L4x5xkyglBM)
- [Top 22 câu hỏi phỏng vấn thường gặp & câu trả lời hoàn hảo (Mọi ngành)](http://boxxv.com/2019/05/19/top-20-questions-interview-and-asked/)
- [Tất cả các bài viết về phỏng vấn trên Viblo](https://viblo.asia/tags/interview)
