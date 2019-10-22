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
Lớp `Application` trong Android là lớp cơ sở trong ứng dụng Android chứa tất cả các `component` khác như `activity` và `service`. Lớp `Application` hoặc bất kỳ lớp con nào của lớp nó sẽ được khởi tạo trước bất kỳ lớp nào khác khi `process` cho ứng dụng của bạn được khởi tạo.

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

#### 16. Sự khác biệt giữa việc add / replace fragment trong backstack?
- replace loại bỏ fragment hiện có và thêm một fragment mới vào. Điều này có nghĩa là khi bạn nhấn nút quay lại, fragment đã được thay thế sẽ được khởi tạo lại với onCreateView của nó được gọi.
- add giữ lại các fragment hiện có và thêm một fragment mới đè lên chúng, có nghĩa là fragment hiện có sẽ hoạt động và những fragment ở dưới sẽ không rơi vào trạng thái paused. Do đó khi nút back được nhấn onCreateView không được gọi cho những fragment này.

#### 17. Tại sao ta nên truyền các tham số vào Fragment thông qua Bundle?
Lý do tại sao bạn nên chuyển các tham số thông qua bundle là vì khi hệ thống khôi phục một fragment (ví dụ: người dùng thay đổi cấu hình), nó sẽ tự động khôi phục bundle của bạn. Bằng cách này, bạn đảm bảo được rằng trạng thái của fragment sẽ được khôi phục một cách chính xác về đúng trạng thái của fragment đó khi được khởi tạo.

#### 18. Retained fragment là gì?
Mặc định, Fragment sẽ bị hủy và được tạo lại cùng với parent Activity của chúng khi thay đổi cấu hình xảy ra. Lời gọi tới phương thức setRetainInstance(true) cho phép chúng ta bỏ qua chu trình "hủy-và-tái tạo" này; báo hiệu cho hệ thống rằng bạn muốn giữ lại instance hiện tại của fragment khi activity được tạo lại, đó chính là retainted fragment.

#### 19. Sự khác nhau giữa FragmentPagerAdapter và FragmentStatePagerAdapter?
- FragmentPagerAdapter: fragment của mỗi trang mà người dùng truy cập sẽ được lưu trữ trong bộ nhớ, mặc dù view của nó sẽ bị hủy. Vì vậy, khi trang được hiển thị lại, chỉ view được tạo lại còn instance của fragment không được tạo lại. Điều này có thể dẫn đến việc một lượng bộ nhớ đáng kể được sử dụng cho công việc này. FragmentPagerAdapter chỉ nên được sử dụng khi chúng ta cần lưu toàn bộ fragment trong bộ nhớ. FragmentPagerAdapter gọi detach(Fragment) trong transaction thay vì remove(Fragment).
- FragmentStatePagerAdapter: instance của fragment sẽ bị phá hủy khi nó không còn hiển thị cho người dùng nữa, ngoại trừ saved state của nó. Điều này dẫn đến việc chỉ sử dụng một lượng nhỏ bộ nhớ và có thể hữu ích để xử lý các tập dữ liệu lớn hơn. Nên được sử dụng khi chúng ta phải sử dụng các fragment động. Nó sẽ không ảnh hưởng đến hiệu suất ngay cả khi có số lượng fragment là rất lớn.

#### 20. Sự khác nhau giữa margin & padding.
Padding là khoảng không gian được thêm vào bên trong container (ví dụ, nếu nó là một button, padding sẽ được thêm vào bên trong button đó. Còn margin sẽ được thêm vào không gian bên ngoài của container.

#### 21. View Group là gì? Nó khác View như thế nào?
- View: các đối tượng View là các khối giao diện cơ bản User Interface (UI) trong Android. View là một hộp hình chữ nhật đơn giản, nó có thể phản hồi hành động của người dùng lên nó. Ví dụ: EditText, Button, CheckBox, ... View tham chiếu đến lớp android.view.View, là lớp cơ sở của tất cả các lớp UI.
- ViewGroup: ViewGroup là một container vô hình. Nó có thể chứa các View và ViewGroup. Ví dụ, LinearLayout là một ViewGroup có thể chứa Button (View) và các Layouts khác. ViewGroup là lớp cơ sở cho Layout.

#### 22. Sự khác nhau giữa hình ảnh .png thông thường và hình ảnh nine-patch là gì?
Nine-patch là một trong những tài nguyên bitmap có thể thay đổi được kích thước, chúng được sử dụng làm hình nền hoặc các hình ảnh khác trên thiết bị. Lớp NinePatch cho phép vẽ một bitmap trong chín bộ phận (section). Bốn góc (corner) không scale được; phần ở giữa của hình ảnh có thể được scale theo cả hai trục, bốn cạnh được scale trên một trục.

#### 23. Khi nào thì bạn nên sử dụng FrameLayout?
FrameLayout được thiết kế để chứa một item duy nhất, làm cho chúng trở thành lựa chọn hiệu quả khi bạn cần hiển thị một View duy nhất. Nếu bạn thêm nhiều View vào FrameLayout thì chúng sẽ xếp chồng lên nhau (cái sau đè lên cái trước), vì vậy FrameLayout cũng hữu ích trong trường hợp nếu bạn cần các View xếp chồng chéo.

#### 24. Adapter là gì?
Một Adapter chịu trách nhiệm chuyển đổi từng data entry vào View, sau đó có thể được thêm vào AdapterView (ListView / RecyclerView) để hiển thị.

#### 25. Tóm tắt quá trình tạo một custom View.
- Tạo một lớp là Subclass của một View.
- Tạo một file res/value/attrs.xml và định nghĩa các thuộc tính bạn muốn sử dụng với custom View đó.
- Trong lớp này, tạo một constructor, khởi tạo các đối tượng Paint và lấy các thuộc tính ở trên.
- Ghi đè onSizeChanged() hoặc onMeasure().
- Vẽ View của bạn bằng cách ghi đè onDraw().

#### 26. Mô tả ngắn gọn một số cách để tối ưu hóa View usage.
- Kiểm tra những quá trình draw tiêu tốn nhiều tài nguyên (excessive overdraw): cài đặt ứng dụng của bạn trên thiết bị Android và sau đó bật tùy chọn Debug GPU Overview.
- Làm phẳng view hierarchy: kiểm tra hệ thống phân cấp view của bạn bằng công cụ Hierarchy Viewer của Android Studio (nên sử dụng ConstraintLayout nhiều nhất có thể để đảm bảo layout của bạn luôn chỉ có một tầng duy nhất).
- Ước lượng thời gian mỗi View cần để hoàn thành quá trình measure, layout và các giai đoạn draw. Bạn cũng có thể sử dụng Hierarchy Viewer để xác định bất kỳ phần nào của rendering pipeline mà bạn cần tối ưu hóa.

#### 27. Bitmap pooling trong Android?
Bitmap pooling là một kỹ thuật đơn giản nhằm mục đích sử dụng lại bitmap thay vì tạo các đối tượng bitmap mới mỗi lần cần. Khi bạn cần một bitmap, bạn sẽ kiểm tra một bitmap stack để xem có bất kỳ bitmap nào có sẵn hay không. Nếu không có bitmap có sẵn, bạn tạo một bitmap mới, ngược lại bạn pop một bitmap từ stack và sử dụng lại nó. Sau đó, khi bạn hoàn thành công việc với bitmap này, bạn có thể đặt nó lại lên một stack.

#### 28. Sự khác biệt giữa commit() và apply() trong SharedPreferences là gì?
commit () ghi dữ liệu một cách đồng bộ và trả về giá trị boolean thành công hay thất bại tùy thuộc vào kết quả ngay lập tức. apply() hoạt động một cách bất đồng bộ và nó sẽ không trả về bất kỳ giá trị boolean nào. Ngoài ra nếu có apply() chưa được hoàn thành và bạn thực hiện một commit() khác. commit() đó sẽ bị chặn cho đến khi apply() được hoàn thành. Về hiệu năng apply nhanh hơn commit vì nó xử lý việc lưu trữ dữ liệu một cách bất đồng bộ.

#### 29. Làm giảm dung lượng file apk trong Android như thế nào?
- Bật Proguard trong project của bạn.
- Bật shrinkResources.
- Loại bỏ tất cả các tài nguyên cục bộ không được sử dụng bằng cách thêm tên tài nguyên cần thiết trong resConfigs.
- Chuyển đổi tất cả các hình ảnh sang dạng webp hoặc vector drawable.

#### 30. S.O.L.I.D principles trong phát triển phần mềm.
- The Single Responsibility Principle (SRP)
- The Open-Closed Principle (OCP)
- The Liskov Substitution Principle (LSP)
- The Interface Segregation Principle (ISP)
- The Dependency Inversion Principle (DIP)

#### 31. Tại sao nói Java độc lập về nền tảng?
Vì việc thực thi code java không phụ thuộc vào hệ điều hành (OS).

#### 32. Khác biệt giữa 'throw' và 'throws' khi xử lý ngoại lệ trong Java?
Từ khóa throw được sử dụng để ném Exception cụ thể từ bất kỳ phương thức hoặc khối tĩnh nào trong khi throws được sử dụng để chỉ ra rằng Exception có thể được ném bởi phương thức này. Ví dụ:
throw new ArithmeticException("Arithmetic Exception");
Và:
throws ArithmeticException;

#### 33. Trong trường hợp nào thì chúng ta có thể bỏ qua khối finally trong một đoạn code try catch?
Bằng cách gọi System.exit (0) trong khối try hoặc catch, chúng ta có thể bỏ qua khối finally.
Tuy nhiên, phương thức System.exit (int) có thể ném ra một SecurityException. Nếu System.exit (0) thoát JVM mà không ném ngoại lệ này thì khối finally sẽ không được thực thi. Ngược lại, nếu System.exit (0) ném ngoại lệ này thì khối finally vẫn sẽ được thực thi.

#### 34. Garbage collector là gì? Nó hoạt động như thế nào?
Tất cả các đối tượng được phân bổ trên vùng heap do JVM quản lý. Miễn là một đối tượng đang được tham chiếu tới hay còn đang được sử dụng, JVM sẽ coi rằng nó còn 'sống'. Khi một đối tượng không còn được tham chiếu và do đó không thể truy cập được bằng code trong ứng dụng, trình thu gom rác - Garbage collector sẽ loại bỏ nó và lấy lại bộ nhớ không sử dụng.

#### 35. Sự khác biệt giữa bộ nhớ stack và bộ nhớ heap?
Stack được sử dụng để phân bố bộ nhớ tĩnh và Heap cho phân bố bộ nhớ động, cả hai được lưu trữ trong RAM của máy tính.

Các biến được phân bổ trên stack được lưu trữ trực tiếp vào bộ nhớ và việc truy cập vào bộ nhớ này là rất nhanh; việc phân bổ của nó được xử lý khi chương trình được biên dịch. Khi một hàm hay một phương thức gọi một hàm khác và hàm này lại gọi một hàm khác nữa, ... việc thực thi các hàm này sẽ bị hoãn lại cho đến khi hàm cuối cùng trả về. Stack hoat động theo cơ chế Last In First Out (LIFO), khối gần hiện tại nhất sẽ luôn là khối tiếp theo được thực thi. Điều này làm cho việc theo dõi stack rất đơn giản, giải phóng một khối khỏi stack tương đương với việc điều chỉnh một con trỏ.

Bộ nhớ của các biến ở trong heap được phân bổ tại run time và việc truy cập các vùng nhớ này tương đối chậm so với trên stack, bù lại thì kích thước heap chỉ bị giới hạn bởi kích thước bộ nhớ ảo. Các thành phần của heap không hề phụ thuộc vào nhau và có thể truy cập một cách ngẫu nhiên tại bất kỳ thời điểm nào. Bạn có thể xác định một khối tại mọi thời điểm và giải phóng nó bất cứ khi nào bạn muốn. Điều này làm cho việc theo dõi phần nào của heap đang được phân bổ và để giải phóng chúng phức tạp hơn.

Bạn có thể sử dụng stack nếu bạn biết chính xác số lượng dữ liệu mà ban muốn cấp phát trước khi biên dịch và nó không quá lớn. Bạn có thể sử dụng heap nếu bạn không biết chính xác kích thước dữ liệu bạn sẽ cần tại thời điểm runtime hoặc bạn cần cấp phát mọt lượng lớn dữ liệu.

Trong trường hợp multi-thread, mỗi thread sẽ có stack độc lập của nó nhưng đều sử dụng chung bộ nhớ heap. Stack được xác định riêng cho từng thread còn Heap là cho ứng dụng. Stack rất quan trọng trong việc xử lý ngoại lệ và luồng thực thi.

Khi một object được khởi tạo, nó sẽ được lưu trữ ở trong không gian bộ nhớ của heap và bộ nhớ stack chứa tham chiếu tới nó. Bộ nhớ stack chỉ chứa các biến nguyên thủy cục bộ và tham chiếu tới các object lưu trữ trong heap. Object lưu trữ trong heap có thể được truy cập một cách toàn cục còn trong stack thì các luồng khác không thể truy cập được.

Bộ nhớ stack tồn tại ngắn hơn trong khi bộ nhớ heap tồn tại từ khi ứng dụng khởi động cho tới khi nó kết thúc thực thi. Khi bộ nhớ stack bị đầy, Java runtime sẽ ném ngoại lệ java.lang.StackOverFlowError và trong trường hợp của heap là java.lang.OutOfMemoryError: Java Heap Space error. Kích thước của stack nhỏ hơn nhiều so với heap nhưng có tốc độ truy cập nhanh hơn.

#### 36. Java có hỗ trợ đa kế thừa không?
Java chỉ hỗ trợ đa kế thừa thông qua interface (vì các class có thể implement nhiều interface nhưng chỉ có thể extend từ một class).

#### 37. Abstract class là gì?
- Abstract class là những lớp chứa một hoặc nhiều phương thức abstract. Một phương thức abstract là một phương thức chỉ được định nghĩa chứ không được triển khai (không có thân hàm).
- Kể cả nếu chỉ có một phương thức là abstract thì cả lớp đó phải được định nghĩa là abstract.
- Các abstract class không thể được khởi tạo.
- Bạn không thể định nghĩa một lớp vừa là abstract vừa là final.
- Các phương thức non-abstract có thể truy cập các phương thức abstract.

#### 38. Interface là gì?
- Interface chỉ định nghĩa các phương thức mà một lớp kế thừa nó sẽ cần triển khai.
- Interface không thể là final, các biến trong interface phải là static hoặc final.
- Interface không thể được khởi tạo một cách trực tiếp.
- Marker interface: marker interface là các interface không định nghĩa bất cứ phương thức nào. Ví dụ điển hình đó chính là java.io.Serializable, và mục đích chính của nó cũng chỉ là để đánh dấu.

#### 39. Tại sao không nên gọi abstract method trong hàm khởi tạo?
Vấn đề là khi một class chưa được khởi tạo một cách hoàn toàn thì khi phương thức abstract này được gọi trong một subclass, nó có thể dẫn đến những tình huống không mong muốn.

#### 40. Sự khác nhau giữa == và phương thức equals() trong Java?
Ta có thể sử dụng toán tử == khi so sánh tham chiếu (so sánh địa chỉ ô nhớ) của đối tượng, còn phương thức equals() để so sánh nội dung của đối tượng đó. Nói một cách đơn giản, == kiểm tra xem nếu hai đối tượng trỏ tới cùng một địa chỉ ô nhớ trong khi equals() so sánh dựa trên các giá trị của các đối tượng này.

#### 41. String Pool trong Java
String Pool trong Java là một pool (bể chứa) của các chuỗi kí tự được lưu trữ ở trọng bộ nhớ Heap. Khi ta sử dụng "" để tạo một đối tượng String, đầu tiên nó sẽ tìm String với giá trị tương tự ở trong String pool, nếu tìm thấy nó sẽ trả về tham chiếu tương ứng còn không sẽ tạo một String mới ở trong pool và trả về tham chiếu tới đối tượng mới này. Tuy nhiên, khi sử dụng toán tử new, ta bắt buộc lớp String tạo một đối tượng String mới ở trong heap. Ta có thể sử dụng phương thức intern() để đưa nó vào trong pool hoặc tham chiếu tới đối tượng String khác ở trong pool mà có giá trị tương tự.

#### 42. String.intern() là gì? Khi nào thì nên sử dụng nó?
- Phương thức String.intern() có thể được sử dụng để giải quyết vấn đề lặp String trong Java. Bằng cách cẩn thận sử dụng intern(), bạn có thể tiết kiệm khá nhiều bộ nhớ bị tiêu thụ bởi việc lặp các String instance. Một string bị lặp khi nó chứa cùng nội dung so với string khác nhưng chiếm vị trí bộ nhớ khác nhau.
- Bằng cách gọi phương thức intern() cho một string (ví dụ "abc"), JVM sẽ đưa chuỗi này vào một pool và bất cứ khi nào một chuỗi "abc" khác được tạo ra, đối tượng ở trong pool sẽ được trả về thay vì tạo ra một đối tượng mới. Do vậy, bạn sẽ tiết kiệm được rất nhiều tài nguyên bộ nhớ, tùy thuộc vào việc các chuỗi của bạn có bị lặp nhiều hay không.

#### 43. Final modifier?
Final modifier: một khi đã được định nghĩa thì không thể sửa đổi được.
- Final class: không thể kế thừa từ final class được.
- Final variable: các biến final không thể bị thay đổi một khi nó đã được khởi tạo.
- Final method: các phương thức final không thể bị ghi đè.

#### 44. Phương thức finalize() là gì?
finalize() là phương thức được sử dụng để thực hiện quá trình "clean up" trước khi một đối tượng được garbage collector thu thập lại. Nói đơn giản, nó được gọi trên đối tượng khi GC quyết định rằng đối tượng này không được tham chiếu tới nữa.

#### 45. Từ khóa finally.
Finally là một đoạn code và được sử dụng để đặt những dòng code quan trọng mà bạn muốn nó được thực thi cho dù ngoại lệ có được xử lý hay không. (try - catch - finally).

#### 46. Từ khóa synchronized.
Khi bạn có hai thread cùng đọc và ghi tới cùng một tài nguyên, ví dụ một biến test, bạn cần phải đảm bảo rằng các thread này truy cập biến trên một cách tuần tự. Nếu không sử dụng từ khóa synchronized, thread 1 có thể không biết những thay đổi mà thread 2 tạo ra đối với biến test và ngược lại. synchronized sẽ block lời gọi tiếp theo của thread tới tài nguyên nếu tài nguyên đó chưa được sử dụng trong một thread khác. Nói cách khác, chỉ có duy nhất một thread được truy cập tới tài nguyên này tại một thời điểm.

#### 47. Từ khóa volatile.
Giả sử hai thread đang cùng chạy trong một phương thức. Nếu hai thread này được chạy trên các processor khác nhau thì mỗi thread có thể có một bản ghi copy cục bộ riêng của biến. Nếu một thread chỉnh sửa giá trị của nó, thread còn lại có thể không biết được sự thay đổi của biến ban đầu (the original variable) một cách ngay lập tức. Điều này dẫn tới vấn đề không đồng nhất dữ liệu. Về cơ bản, volatile được sử dụng để chỉ định rằng giá trị của một biến sẽ bị chỉnh sửa bởi những thread khác nhau. volatile nói cho trình biên dịch rằng giá trị của một biến không nên được cache vì giá trị của nó có thể thay đổi ngoài phạm vi của chương trình. Giá trị của biến này sẽ không bao giờ được cache một cách cục bộ trên thread: tất cả quá trình đọc, ghi sẽ được thực hiện thẳng trong main memory.

#### 48. Autoboxing và Unboxing là gì?
Autoboxing là quá trình tự động chuyển đổi mà trình biên dịch Java tạo ra giữa kiểu dữ liệu nguyên thủy và các lớp wrapper tương ứng của chúng (ví dụ: int - Integer, long - Long, double - Double...). Quá trình chuyển đổi ngược lại chính là unboxing.

#### 49. Externalization là gì?
Trong serialization, JVM chịu trách nhiệm cho qúa trình ghi và đọc các đối tượng. Việc này khá là hữu ích trong đa số các tình huống bởi lập trình viên không cần tốn thời gian hay công sức quan tâm tới chi tiết của các tầng hoạt động phía dưới của quá trình serialization. Tuy nhiên, theo mặc định thì serialization không thể bảo vệ các thông tin nhạy cảm ví dụ như mật khẩu, thông tin nhân dạng, ... Bởi vậy, externalization sinh ra cho phép lập trình viên quyền điều khiển hoàn toàn quá trình đọc, ghi các đối tượng trong quá trình serialization. Việc bạn cần làm là implement java.io.Externalizable, sau đó triển khai code của riêng mình để ghi trạng thái của đối tượng trong phương thức writeExternal() và đọc trạng thái đối tượng trong phương thức readExternal().

#### 50. Sự khác nhau giữa ArrayList và Vector?
Vector là thread safe (synchronized) trong khi ArrayList thì không. Vì vậy hiệu năng của ArrayList sẽ tốt hơn so với Vector, nhưng Vector an toàn đối với những bài toán đa luồng mà bạn cần đồng bộ dữ liệu. Tuy nhiên nếu bạn sử dụng phương thức Collections.synchronizedList() thì nó cũng sẽ trả về cho bạn một synchronized list tương tự như Vector. Thực chất, cả hai đều chứa các phần tử của chúng ở trong một Array (mảng). Khi một phần tử mới được thêm vào một ArrayList hay Vector, chúng cần phải mở rộng mảng chứa phần tử của mình nếu kích thước của nó đã đạt giới hạn. Một Vector mặc định sẽ mở rộng ra gấp đôi kích thước mảng của nó, trong khi ArrayList thì chỉ gấp rưỡi.

#### 51. Việc chèn và xóa phần tử trong ArrayList có chậm hơn so với LinkedList không?
ArrayList sử dụng một mảng để lưu trữ các phần tử, khi mảng đó được lấp đầy thì một mảng mới có kích thước khoảng 1,5 lần kích thước của mảng ban đầu được tạo ra và tất cả dữ liệu của mảng cũ sẽ được sao chép sang mảng mới. Đối với quá trình xóa, tất cả phần tử trong mảng phải được lùi lại một index để lấp vào khoảng trống mà phần tử bị xóa để lại. Trong LinkedList, dữ liệu được lưu trữ trong các node và các node này có thể tham chiếu tới phần tử trước hoặc sau nó; vì vậy việc thêm phần tử mới vào rất đơn giản và nhanh chóng. Đó là tạo ra node mới, cập nhật con trỏ next của node cuối cùng và con trỏ previous của node mới. Quá trình xóa phần tử trong linked list cũng nhanh hơn vì nó chỉ cần cập nhật con trỏ next của node ngay trước node bị xóa và con trỏ previous của node nằm ngay sau node bị xóa.

#### 52. HashMap hoạt động như thế nào?
HashMap trong Java hoạt động dựa trên nguyên tắc băm. Đó là một cấu trúc dữ liệu cho phép chúng ta lưu trữ đối tượng và lấy nó với thời gian thực hiện là hằng số (độ khó O(1)) nếu ta biết trước key. Khi ta gọi phương thức put(), phương thức hashCode() của đối tượng đóng vai trò là key sẽ được gọi theo để hàm băm của map có thể tìm thấy vị trí để lưu trữ đối tượng Map.Entry (chính là đối tượng mà HashMap sử dụng để lưu trữ cả cặp key và value). Về cơ bản, HashMap sử dụng một mảng để lưu trữ các đối tượng Map.Entry này, và vì mảng có kích thước cố định nên nếu bạn tiếp tục đẩy vào các phần tử mới, đến một lúc hàm băm sẽ trả về cùng một địa chỉ cho hai key khác nhau, việc này được gọi là collision (xung đột) trong HashMap. Trong trường hợp này, một linked list sẽ hình thành tại vị trí đó và một entry mới được lưu trữ lại dưới dạng node tiếp theo. Nếu bạn cần lấy đối tượng từ linked list này, bạn sẽ cần phải thực hiện một quá trình kiểm tra thêm để tìm kiếm đúng giá trị mình mong muốn, điều này được thực hiện thông qua phương thức equals(). Vì mỗi node đều chứa một entry, HashMap sẽ liên tục so sánh key của các entry này với key được truyền vào sử dụng phương thức equals() và khi nó trả về true, Map sẽ trả về giá trị tương ứng cho bạn.

Cảm ơn các bạn đã đọc bài của mình. Nếu có đóng góp hay thắc mắc các bạn hãy để lại ở phần comment nhé, mình sẽ cố gắng trả lời một cách sớm nhất có thể.

Chúc các bạn thành công!

Tham khảo:
- [Voz: Tổng hợp các câu hỏi phỏng vấn Android Dev cho sinh viên mới ra trường](https://forums.voz.vn/showthread.php?t=7216185)
- [20 Essential Android Interview Questions and Answers](https://www.toptal.com/android/interview-questions)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 1)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)
- [Một số câu hỏi phỏng vấn Android bạn nên lưu ý (phần 2)](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-2-L4x5xkyglBM)
- [Top 22 câu hỏi phỏng vấn thường gặp & câu trả lời hoàn hảo (Mọi ngành)](http://boxxv.com/2019/05/19/top-20-questions-interview-and-asked/)
- [Tất cả các bài viết về phỏng vấn trên Viblo](https://viblo.asia/tags/interview)
