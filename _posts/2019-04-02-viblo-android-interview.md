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

#### 9. Job Scheduling là gì?
Job Scheduling API, như tên gọi của nó, cho phép chúng ta lên lịch công việc trong khi hệ thống sẽ thực hiện công việc tối ưu hóa dựa trên bộ nhớ, nguồn và trạng thái kết nối. JobScheduler hỗ trợ lập lịch biểu các công việc. Hệ thống Android có thể kết hợp các công việc này để giảm lượng tiêu thụ pin. JobManager giúp việc xử lý upload dễ dàng hơn vì nó tự động xử lý các trạng thái kết nối của mạng. Nó cũng sẽ sống sót kể cả khi ứng dụng bị khởi động lại. Một số tình huống hữu ích:
- Các tác vụ cần được thực hiện khi thiết bị được kết nối với nguồn điện.
- Các tác vụ yêu cầu truy cập mạng hoặc kết nối Wi-Fi.
- Các tác vụ không quan trọng hay không được người dụng chú ý đến.
- Các tác vụ cần được chạy thường xuyên dưới dạng hàng loạt trong đó yếu tố thời gian không quá quan trọng.

#### 10. Mối quan hệ giữa vòng đời của AsyncTask và Activity? Những vấn đề gì có thể xảy ra khi sử dụng chúng chung với nhau? Giải quyết những vấn đề đó thế nào?
AsyncTask không được gắn với vòng đời của Activity chứa nó. Ví dụ, nếu bạn khởi động AsyncTask bên trong một Activity và khi người dùng quay thiết bị, Activity sẽ bị hủy (và một instance mới của Activity sẽ được tạo) nhưng AsyncTask sẽ không bị hủy mà thay vào đó sẽ tiếp tục chạy cho đến khi nó hoàn thành.

Sau đó, khi AsyncTask hoàn thành, thay vì cập nhật giao diện người dùng của Activity mới, nó sẽ cập nhật phiên bản Activity trước đó (Activity đã bị hủy). Điều này có thể dẫn đến một Exception: java.lang.IllegalArgumentException.

Ngoài ra còn có khả năng dẫn đến rò rỉ bộ nhớ (memory leak) vì AsyncTask duy trì một tham chiếu đến Activity cũ, ngăn cản Activity này bị thu gom rác của Java thu thập khi vẫn còn hoạt động.

Vì những lý do này, việc sử dụng AsyncTask cho các tác vụ nền chạy dài thường là một ý tưởng tồi. Thay vào đó đối với các tác vụ nền chạy dài, bạn nên sử dụng một cơ chế khác (chẳng hạn như service).

#### 11. Phương thức onTrimMemory() là gì?
onTrimMemory (): Được gọi khi hệ điều hành xác định rằng đây là thời điểm tốt để xử lý bộ nhớ không cần thiết từ một tiến trình của nó. Ví dụ điều này sẽ xảy ra khi tiến trình chạy ở chế độ nền và không đủ bộ nhớ để duy trì được nhiều tiến trình nền như mong muốn, khi đó hệ thống sẽ dựa trên độ ưu tiên của tiến trình để kill bớt cho tới khi bộ nhớ đã ổn định. Hệ thống Android có thể lấy lại bộ nhớ cấp phát cho ứng dụng của bạn theo nhiều cách hoặc kill ứng dụng của bạn nếu cần thiết để giải phóng bộ nhớ cho các tác vụ quan trọng. Để giúp cân bằng bộ nhớ của hệ thống và tránh việc hệ thống hủy tiến trình của ứng dụng, bạn có thể implement interface ComponentCallbacks2 ở trong các lớp Activity của mình. Phương thức callback onTrimMemory () được cung cấp cho phép ứng dụng của bạn lắng nghe các sự kiện liên quan đến bộ nhớ khi ứng dụng của bạn ở foreground hoặc background từ đó bạn có thể xử lý khi hệ thống cần thu hồi lại bộ nhớ từ ứng dụng của bạn.

#### 12. Android Interface Definition Language (AIDL) và Messenger Queue.
- Messenger Queue tạo cho ta một hàng đợi và các dữ liệu / thông điệp được truyền giữa 2 hoặc nhiều hơn các tiến trình một cách tuần tự. Trong trường hợp của AIDL thì các thông điệp được truyền đi một cách song song.
- AIDL sử dụng dành cho mục đích khi bạn phải giao tiếp ở mức ứng dụng để chia sẻ và kiểm soát dữ liệu. Ví dụ: một ứng dụng yêu cầu danh sách tất cả các liên hệ từ ứng dụng Danh bạ và nó cũng muốn hiển thị thời lượng cuộc gọi và bạn có thể ngắt kết nối nó khỏi ứng dụng đó.
- Đối với trương hợp của Messenger Queue, bạn sẽ chủ yếu làm việc trên nhiều thread và process để quản lý hàng đợi chứa các thông điệp để không xuất hiện sự can thiệp của các dịch vụ bên ngoài tại đây.

#### 13. ThreadPool là gì? Có hiệu quả hơn nếu sử dụng nó thay vì sử dụng nhiều Thread riêng biệt.
Việc tạo và hủy các Thread có mức sử dụng CPU cao, vì vậy khi chúng ta cần thực hiện rất nhiều tác vụ đơn giản, nhỏ, chi phí để tạo các Thread riêng rẽ có thể chiếm một phần đáng kể chu kỳ CPU và ảnh hưởng nghiêm trọng đến thời gian đáp ứng cuối cùng. ThreadPool bao gồm một hàng đợi nhiệm vụ và một nhóm các worker thread, cho phép nó chạy nhiều instance một cách song song của một tác vụ.

#### 14. Sự khác biệt giữa Serializable và Parcelable?
Serialization là quá trình chuyển đổi một đối tượng thành một luồng (stream) byte để lưu trữ một đối tượng vào bộ nhớ, để nó có thể được tái tạo sau này khi cần, trong khi vẫn giữ trạng thái và dữ liệu ban đầu của đối tượng. Serializable là một standard Java interface. Parcelable là một interface cụ thể của Android, bạn phải tự triển khai việc serialization. Tuy nhiên Parcelable có hiệu quả hơn nhiều so với Serializable (vấn đề với cách tiếp cận sử dụng Serializable là nó sự dụng cơ chế reflection và đó là một quá trình tương đối chậm. Cơ chế này cũng có xu hướng tạo ra rất nhiều đối tượng tạm thời và gây tiêu tốn tài nguyên khi bộ Garbage collection phải thu thập tất cả chúng).

#### 15. Bạn sẽ cập nhật UI trên activity từ một background service như thế nào?
Ta cần phải đăng ký một LocalBroadcastReceiver trong activity đó. Và gửi một broadcast với dữ liệu chứa trong intent từ background service này. Miễn là activity còn hoạt động ở trên foreground, giao diện người dùng sẽ được cập nhật. Lưu ý bạn nên nhớ hủy đăng ký broadcast receiver ở trong phương thức Stop()của activity để tránh bị memory leak. Ta cũng có thể sử dụng một Handler để truyền dữ liệu thông qua nó.

#### 

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
