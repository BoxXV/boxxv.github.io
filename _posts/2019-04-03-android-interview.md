---
layout: post
title: 22+ Câu hỏi phỏng vấn Android và gợi ý trả lời
subtitle: Vì một tương lai lương Android cao hơn iOS
date: "2019-04-03"
tags:
- Android
- Interview
- Questions
- Answers
modified: 2019-04-21
---

1) Có bốn lớp Java liên quan đến việc sử dụng cảm biến trên nền tảng Android. Liệt kê và giải thích mục đích của mỗi lớp.

2) `ContentProvider` là gì và nó thường được sử dụng để làm gì?

3) Trong điều kiện nào code mẫu dưới đây có thể làm crash ứng dụng của bạn? Làm thế nào bạn sẽ sửa đổi mã để tránh vấn đề tiềm năng này? Giải thích câu trả lời của bạn.
```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
startActivity(sendIntent);
```

4) Callback cuối cùng trong vòng đời của một activity là `onDestroy()`. Hệ thống gọi phương thức này trong activity của bạn là tín hiệu cuối cùng cho thấy activity của bạn đang bị xóa hoàn toàn khỏi bộ nhớ hệ thống. Thông thường, hệ thống sẽ gọi `onPause()` và `onStop()` trước khi gọi `onDestroy()`. Tuy nhiên, hãy mô tả một kịch bản, trong đó `onPause()` và `onStop()` sẽ không được gọi.

5) Đoạn mã nào dưới đây là cách chính xác để kiểm tra xem có cảm biến La bàn trên hệ thống không? Giải thích câu trả lời của bạn.

<ins>Câu trả lời 1:</ins>
```java
PackageManager m = getPackageManager();
if (!m.hasSystemFeature(PackageManager.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

<ins>Câu trả lời 2:</ins>
```java
SensorManager m = getSensorManager();
if (!m.hasSystemFeature(SensorManager.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

<ins>Câu trả lời 3:</ins>
```java
Sensor s = getSensor();
if (!s.hasSystemFeature(Sensor.FEATURE_SENSOR_COMPASS)) {
    // This device does not have a compass, turn off the compass feature
}
```

6) Mô tả ba trường hợp sử dụng phổ biến để sử dụng một `Intent`.

7) Giả sử rằng bạn đang bắt đầu một service trong Activity như sau:
```java
Intent service = new Intent(context, MyService.class);
startService(service);
```
nơi `MyService` truy cập là máy chủ từ xa thông qua kết nối Internet.

Nếu Activity đang hiển thị một hình động cho biết một số loại tiến bộ, bạn có thể gặp phải vấn đề gì và làm thế nào bạn có thể giải quyết nó?

8) Thông thường, trong quá trình thực hiện định hướng lại màn hình, nền tảng Android phá vỡ activity nền trước và tạo lại nó, khôi phục từng giá trị chế độ xem trong bố cục activity.

Trong một ứng dụng mà bạn đang làm việc, bạn nhận thấy rằng giá trị của chế độ xem không được khôi phục sau khi định hướng lại màn hình. Điều gì có thể là nguyên nhân có thể của vấn đề mà bạn nên xác minh, ở mức tối thiểu, về quan điểm cụ thể đó?

9) DDMS là gì? Mô tả một số khả năng của nó.

10) Mối quan hệ giữa vòng đời của `AsyncTask` và `Activity` là gì? Những vấn đề này có thể dẫn đến? Làm thế nào những vấn đề này có thể tránh được?

11) `Intent` là gì? Nó có thể được sử dụng để cung cấp dữ liệu cho một `ContentProvider`? Tại sao hoặc tại sao không?

12) Sự khác biệt giữa fragment và một activity là gì? Giải thích mối quan hệ giữa cả hai.

13) Sự khác biệt giữa `Serializable` và `Parcelable` là gì? Cách tiếp cận tốt nhất trong Android là gì?

14) Thế nào là "“launch modes"? Hai cơ chế mà theo đó chúng có thể được định nghĩa là gì? Loại chế độ khởi chạy cụ thể nào được hỗ trợ?

15) Sự khác biệt giữa `Service` và `IntentService` là gì? Mỗi loại được sử dụng như thế nào?

16) Làm thế nào để bạn cung cấp các đối số xây dựng vào một Fragment?

17) ANR là gì và tại sao nó lại xảy ra?

18) Phương pháp nào chỉ được gọi là một lần trong một vòng đời của fragment?

19) Trong lập trình Android có thể tạo activity mà không có giao diện người dùng không?

20) Nhận broadcast là gì?

-----
## Gợi ý trả lời


#### 1) Bốn lớp Java liên quan đến việc sử dụng các cảm biến trên nền tảng Android là:
- `Sensor`: Cung cấp các phương pháp để xác định khả năng nào khả dụng cho một cảm biến cụ thể.
- `SensorManager`: Cung cấp các phương pháp để đăng ký lắng nghe sự kiện cảm biến và hiệu chỉnh cảm biến.
- `SensorEvent`: Cung cấp dữ liệu cảm biến thô (raw), bao gồm thông tin liên quan đến độ chính xác.
- `SensorEventListener`: Interfacen định nghĩa phương thức gọi lại (callback) sẽ nhận thông báo sự kiện cảm biến.

Để tìm hiểu thêm về [Sensor](https://developer.android.com/guide/topics/sensors/sensors_overview.html), hãy tham khảo hướng dẫn dành cho nhà phát triển Android.


#### 2) `ContentProvider` là một thành phần để quản lý truy cập dữ liệu. Nó đóng gói dữ liệu và cung cấp các cơ chế để xác định bảo mật dữ liệu. `ContentProvider` là interface chuẩn kết nối dữ liệu trong một quy trình với mã đang chạy trong quy trình khác.

Thông tin thêm về `ContentProvider` có thể được tìm thấy [ở đây](https://developer.android.com/guide/topics/providers/content-providers.html) trong Hướng dẫn dành cho nhà phát triển Android.


#### 3) Chỉ định một intent ngầm là một hành động có thể gọi bất kỳ ứng dụng nào trên thiết bị có thể thực hiện hành động. Sử dụng một intent ngầm rất hữu ích khi ứng dụng của bạn không thể thực hiện hành động, nhưng các ứng dụng khác có lẽ có thể. Nếu có nhiều ứng dụng được đăng ký có thể xử lý yêu cầu này, người dùng sẽ được nhắc chọn cái nào sẽ sử dụng.

Tuy nhiên, có thể không có ứng dụng nào có thể xử lý ý định của bạn. Trong trường hợp này, ứng dụng của bạn sẽ gặp crash khi bạn gọi `startActivity ()`. Để tránh điều này, trước khi gọi `startActivity ()` trước tiên bạn nên xác minh rằng có ít nhất một ứng dụng được đăng ký trong hệ thống có thể xử lý ý định đó. Để thực hiện việc này, hãy sử dụng `resolveActivity()` trên đối tượng intent của bạn:

```java
// Verify that there are applications registered to handle this intent
// (resolveActivity returns null if none are registered)
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}
```


#### 4) `onPause()` và `onStop()` sẽ không được gọi nếu `finish()` được gọi từ bên trong phương thức `onCreate()`. Điều này có thể xảy ra, ví dụ, nếu bạn phát hiện ra lỗi trong khi `onCreate()` và gọi `finish()`. Tuy nhiên, trong trường hợp như vậy, mọi thao tác dọn dẹp mà bạn dự kiến sẽ được thực hiện trong `onPause()` và `onStop()` sẽ không được thực thi.

Mặc dù `onDestroy()` là callback cuối cùng trong vòng đời của một activity, điều đáng nói là callback này có thể không luôn luôn được gọi và không nên dựa vào để giải phóng tài nguyên. Tốt hơn là có các tài nguyên được tạo trong `onStart()` và `onResume()` và giải phóng chúng tương ứng trong `onStop()` và `onPause()`.

Xem hướng dẫn dành cho nhà phát triển Android để biết thêm [thông tin](https://developer.android.com/guide/components/activities/activity-lifecycle) về vòng đời activity.


#### 5) Câu trả lời đúng là Câu trả lời số 1, sử dụng PackageManager.

`SensorManager` và `Sensor` là một phần của Android Sensor Framework và được sử dụng để truy cập trực tiếp và thu thập dữ liệu cảm biến thô. Các lớp này không cung cấp bất kỳ phương thức nào như `hasSystemFeature()` được sử dụng để đánh giá các khả năng của hệ thống.

Android định nghĩa tính năng IDs, dưới dạng ENUM, cho bất kỳ tính năng phần cứng hoặc phần mềm nào có thể có trên thiết bị. Chẳng hạn, tính năng ID cho cảm biến la bàn là `FEATURE_SENSOR_COMPASS`.

Nếu ứng dụng của bạn không thể hoạt động mà không có tính năng cụ thể có sẵn trên hệ thống, bạn có thể ngăn người dùng cài đặt ứng dụng của bạn với phần tử `<used-Feature>` trong tệp manifest của ứng dụng của bạn để chỉ định một phụ thuộc không thể thương lượng.

Tuy nhiên, nếu bạn chỉ muốn vô hiệu hóa các thành phần cụ thể của ứng dụng của mình khi thiếu một tính năng, bạn có thể sử dụng lớp `PackageManager`. `PackageManager` được sử dụng để truy xuất các loại thông tin khác nhau liên quan đến các gói ứng dụng hiện đang được cài đặt trên thiết bị.

Để tìm hiểu thêm về [khả năng tương thích và xử lý các loại thiết bị](https://developer.android.com/guide/practices/compatibility.html) hoặc [cảm biến](https://developer.android.com/guide/topics/sensors/sensors_overview.html) khác nhau, vui lòng tham khảo hướng dẫn dành cho nhà phát triển Android.


#### 6) Các trường hợp sử dụng phổ biến để sử dụng `Intent` bao gồm:

- Để bắt đầu một activity: Bạn có thể bắt đầu một phiên bản mới của một Activity bằng cách chuyển một phương thức Intent sang `startActivity()`.
- Để bắt đầu một service: Bạn có thể bắt đầu một service để thực hiện thao tác một lần (chẳng hạn như tải xuống một tệp) bằng cách chuyển một `Intent` đến `startService()`.
- Để truyền broadcast: Bạn có thể truyền broadcast các ứng dụng khác bằng cách chuyển `Intent` đến `sendBroadcast()`, `sendOrderedBroadcast()` hoặc `sendStickyBroadcast()`.

Thông tin thêm về [Intent](https://developer.android.com/guide/components/intents-filters.html) có thể được tìm thấy trong hướng dẫn của nhà phát triển Android.


#### 7) Phản hồi từ dịch vụ từ xa qua Internet thường có thể mất một chút thời gian, do độ trễ của mạng hoặc tải trên máy chủ từ xa hoặc thời gian cần thiết để dịch vụ từ xa xử lý và đáp ứng yêu cầu.

Kết quả là, nếu sự chậm trễ như vậy xảy ra, hình ảnh động trong hoạt động (và thậm chí tệ hơn, toàn bộ luồng UI) có thể bị chặn và có thể xuất hiện để người dùng bị đông lạnh trong khi khách hàng chờ phản hồi từ dịch vụ. Điều này là do dịch vụ được bắt đầu trên luồng ứng dụng chính (hoặc luồng UI) trong Activity.

Vấn đề có thể (và nên) tránh được bằng cách đưa bất kỳ yêu cầu từ xa nào vào luồng nền hoặc khi khả thi, sử dụng cơ chế phản hồi không đồng bộ.

Lưu ý rõ: Truy cập mạng từ luồng UI sẽ ném ngoại lệ thời gian chạy trong các phiên bản Android mới hơn khiến ứng dụng bị sập.


#### 8)
Bạn nên xác minh rằng nó có `id` hợp lệ. Để hệ thống Android khôi phục trạng thái của các chế độ xem trong activity của bạn, mỗi chế độ xem phải có một ID duy nhất, được cung cấp bởi thuộc tính `android:id`.

Thêm thông tin có sẵn [ở đây](https://developer.android.com/guide/components/activities/activity-lifecycle).


#### 9) DDMS là [Dalvik Debug Monitor Server ](https://developer.android.com/studio/profile/monitor) đi kèm với Android. Nó cung cấp một loạt các tính năng sửa lỗi bao gồm:
- services cổng chuyển tiếp
- chụp màn hình
- thông tin thread và heap
- theo dõi lưu lượng mạng
- cuộc gọi đến và giả mạo SMS
- mô phỏng trạng thái mạng, tốc độ và độ trễ
- giả mạo dữ liệu vị trí


#### 10) `AsyncTask` không được gắn với vòng đời của `Activity` có chứa nó.
Vì vậy, ví dụ, nếu bạn khởi động AsyncTask bên trong một Activity và người dùng xoay thiết bị, Activity sẽ bị hủy (và một phiên bản Activity mới sẽ được tạo) nhưng AsyncTask sẽ không chết mà thay vào đó tiếp tục tồn tại cho đến khi hoàn thành.

Sau đó, khi AsyncTask hoàn thành, thay vì cập nhật giao diện người dùng của Activity mới, nó sẽ cập nhật phiên bản cũ của Activity (nghĩa là, trong đó nó đã được tạo nhưng nó không được hiển thị nữa!). Điều này có thể dẫn đến `Exception` (thuộc loại `java.lang.IllegalArgumentException`: Chế độ xem không được đính kèm với trình quản lý cửa sổ nếu bạn sử dụng, ví dụ, `findViewById` để truy xuất chế độ xem bên trong Activity).

Ngoài ra, còn có khả năng điều này dẫn đến leak memory do AsyncTask duy trì tham chiếu đến Activty, điều này ngăn Activity giair phóng bộ nhớ khi mà AsyncTask vẫn còn tồn tại.

Vì những lý do này, sử dụng AsyncTask cho các tác vụ nền chạy dài thường là một ý tưởng tồi. Thay vào đó, đối với các tác vụ nền chạy dài, nên sử dụng một cơ chế khác (như service).


#### 11) Đối tượng `Intent` là một cơ chế chung để bắt đầu activity mới và chuyển dữ liệu từ activity này sang activity khác.
Tuy nhiên, bạn không thể khởi động `ContentProvider` bằng `Intent`.

Khi bạn muốn truy cập dữ liệu trong `ContentProvider`, thay vào đó, bạn phải sử dụng đối tượng `ContentResolver` trong ứng dụng của bạn `Context` để liên lạc với nhà cung cấp với tư cách là client. Đối tượng `ContentResolver` giao tiếp với đối tượng nhà cung cấp, một thể hiện của lớp thực hiện `ContentProvider`. Đối tượng nhà cung cấp nhận các yêu cầu dữ liệu từ khách hàng, thực hiện hành động được yêu cầu và trả về kết quả.


#### 12) Một [activity](https://developer.android.com/reference/android/app/Activity.html) thường là một hoạt động tập trung duy nhất mà người dùng có thể thực hiện (như quay số, chụp ảnh, gửi email, xem bản đồ, v.v.).
Tuy nhiên, đồng thời, không có gì ngăn cản nhà phát triển tạo ra một activity phức tạp tùy ý.

Việc triển khai activity có thể tùy ý sử dụng lớp [Fragment](https://developer.android.com/reference/android/app/Fragment.html) cho các mục đích lập trình theo mô-đun hơn, xây dựng giao diện người dùng tinh vi hơn cho màn hình lớn hơn, giúp mở rộng các ứng dụng giữa màn hình nhỏ và lớn, v.v. Nhiều fragments có thể được kết hợp trong một activity và ngược lại, cùng một đoạn thường có thể được sử dụng lại qua nhiều activity. Cấu trúc này chủ yếu nhằm thúc đẩy tái sử dụng mã và tạo điều kiện cho việc mở rộng tính năng.

Một fragment thực chất là một phần mô-đun của một activity, với vòng đời và các sự kiện đầu vào của chính nó, và có thể được thêm hoặc xóa theo ý muốn. Tuy nhiên, điều quan trọng cần nhớ là vòng đời của fragment bị ảnh hưởng trực tiếp bởi vòng đời activity chủ của nó; tức là, khi activity bị tạm dừng, tất cả các fragment trong đó và khi activity bị phá hủy, thì tất cả các fragment của nó cũng vậy.

Thông tin thêm có sẵn ở [đây](https://developer.android.com/guide/components/fragments.html) trong Hướng dẫn dành cho nhà phát triển Android.


#### 13) 
Serializable là một interface Java tiêu chuẩn. Bạn chỉ cần đánh dấu một lớp Serializable bằng cách triển khai giao diện và Java sẽ tự động Serializable nó trong các tình huống nhất định.

Parcelable là một giao diện cụ thể của Android nơi bạn tự thực hiện việc tuần tự hóa. Nó được tạo ra để hiệu quả hơn nhiều so với Serializable và để giải quyết một số vấn đề với sơ đồ Serializable Java mặc định.


#### 14) Một “launch mode” là cách thức mà một thể hiện mới của một activity là có liên quan đến nhiệm vụ hiện tại.

Các chế độ khởi chạy có thể được xác định bằng một trong hai cơ chế:

- Tệp Manifest. Khi khai báo một activity trong một manifest, bạn có thể chỉ định cách activity sẽ liên kết với các tác vụ khi nó bắt đầu. Các giá trị được hỗ trợ bao gồm:
 - `standard` (mặc định). Nhiều instances  lớp activity có thể được khởi tạo và nhiều instances có thể được thêm vào cùng một tác vụ hoặc các tác vụ khác nhau. Đây là chế độ phổ biến cho hầu hết các activity.
 - `singleTop`. Sự khác biệt so với `standard` là, nếu một instance của activity đã tồn tại ở đầu nhiệm vụ hiện tại và hệ thống định hướng ý định cho activity này, sẽ không có trường hợp mới nào được tạo ra bởi vì nó sẽ loại bỏ phương thức `onNewIntent()` thay vì tạo ra một đối tượng mới.
 - `singleTask`. Một tác vụ mới sẽ luôn được tạo và một thể hiện mới sẽ được đẩy đến tác vụ là gốc. Tuy nhiên, nếu có bất kỳ trường hợp activity nào tồn tại trong bất kỳ tác vụ nào, hệ thống sẽ định hướng ý định đến thể hiện activity đó thông qua lệnh gọi phương thức `onNewIntent()`. Trong chế độ này, các trường hợp activity có thể được đẩy đến cùng một nhiệm vụ. Chế độ này hữu ích cho các activity đóng vai trò là điểm vào.
 - `singleInstance`. Tương tự như `singleTask`, ngoại trừ trường hợp không có activity nào có thể được đẩy vào cùng một nhiệm vụ của SingleInstance. Theo đó, activity với chế độ khởi chạy luôn nằm trong một tác vụ thể hiện activity duy nhất. Đây là một chế độ rất chuyên biệt và chỉ nên được sử dụng trong các ứng dụng được triển khai hoàn toàn dưới dạng một activity.

- Intent flags. Các lệnh gọi `startActivity()` có thể bao gồm một cờ trong Ý định khai báo nếu và cách activity mới sẽ được liên kết với tác vụ hiện tại. Các giá trị được hỗ trợ bao gồm:
  - `FLAG_ACTIVITY_NEW_TASK`. Tương tự như giá trị singleTask trong tệp Manifest (xem bên trên).
  - `FLAG_ACTIVITY_SINGLE_TOP`. Tương tự như giá trị singleTop trong tệp Manifest (xem bên trên).
  - `FLAG_ACTIVITY_CLEAR_TOP`. Nếu activity đang bắt đầu đã chạy trong tác vụ hiện tại, thì thay vì khởi chạy một phiên bản mới của activity đó, tất cả các activity khác trên đầu activity đó sẽ bị hủy và ý định này được chuyển đến phiên bản tiếp tục của activity (bây giờ đầu trang), thông qua `onNewIntent()`. Không có giá trị tương ứng trong tệp Manifest tạo ra hành vi này.

Thông tin thêm về các chế độ khởi chạy có sẵn ở [đây](https://developer.android.com/guide/components/activities/tasks-and-back-stack#TaskLaunchModes).


#### 15)
`Service` là lớp cơ sở cho các dịch vụ Android có thể được mở rộng để tạo bất kỳ dịch vụ nào. Một lớp trực tiếp mở rộng Dịch vụ chạy trên luồng chính vì vậy nó sẽ chặn UI (nếu có) và do đó chỉ nên được sử dụng cho các tác vụ ngắn hoặc nên sử dụng các luồng khác cho các tác vụ dài hơn.

`IntentService` là một lớp con của Dịch vụ xử lý các yêu cầu không đồng bộ (được thể hiện dưới dạng “Intents”) theo yêu cầu. Khách hàng gửi yêu cầu thông qua các cuộc gọi `startService(Intent)`). Dịch vụ được bắt đầu khi cần thiết, lần lượt xử lý từng `Intent` bằng cách sử dụng một worker thread và tự dừng khi xong việc. Viết một `IntentService` có thể khá đơn giản; chỉ cần mở rộng lớp `IntentService` và ghi đè phương thức `onHandleIntent(Intent intent)` nơi bạn có thể quản lý tất cả các yêu cầu đến.


#### 16)
Các đối số xây dựng cho một `Fragment` được truyền qua Bundle bằng phương thức `Fragment#setArgument(Bundle)`. `Bundle` được truyền vào sau đó có thể được truy xuất thông qua phương thức `Fragment#getArguments()` trong phương thức vòng đời Fragment thích hợp.

Đó là một lỗi phổ biến để truyền dữ liệu thông qua một hàm tạo tùy chỉnh. Các hàm tạo không mặc định trên Fragment không được khuyến khích vì Fragment có thể bị hủy và được tạo lại do thay đổi cấu hình (ví dụ: thay đổi hướng). Sử dụng `#setArguments()` / `getArguments()` đảm bảo rằng khi Fragment cần được tạo lại, `Bundle` sẽ được tuần tự hóa / giải tuần tự một cách thích hợp để dữ liệu xây dựng được phục hồi.


#### 17)
‘ANR’, trong Android là ‘Application Not Responding.’ Có nghĩa là khi người dùng đang tương tác với activity và activity trong phương thức `onResume()`, một hộp thoại xuất hiện hiển thị ứng dụng không phản hồi.

Nó xảy ra bởi vì chúng tôi bắt đầu một tác vụ nặng và dài như tải xuống dữ liệu trong luồng UI chính. Giải pháp của vấn đề là bắt đầu các tác vụ nặng của bạn ở nền sau bằng cách sử dụng lớp Async Task.


#### 18) `onAttached()`


#### 19)
Có, một hoạt động có thể được tạo mà không cần bất kỳ giao diện người dùng. Những hoạt động này được coi là hoạt động trừu tượng.


#### 20)
Broadcast receiver liên lạc với các thông báo của hệ điều hành, chẳng hạn như kiểm tra xem có kết nối internet hay không, có phải là nhãn pin hay không, v.v.



Tham khảo:
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 1)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 2)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-2-L4x5xkyglBM)
- [Top 22 câu hỏi phỏng vấn thường gặp & câu trả lời hoàn hảo (Mọi ngành)](http://boxxv.com/2019/05/19/top-20-questions-interview-and-asked/)
