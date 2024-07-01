---
layout: post
title: So sánh Tool test tự động Coded UI Test, Selenium và QTP
subtitle: Công cụ AI hỗ trợ lập trình
image: "img/2024/f915c918009ca0c2f98d.jpg"
tags:
- Mạt Code
- lập trình
---

## Mục lục

- [Mục lục](#mục-lục)
- [Bắt đầu với kiểm thử tự động](#bắt-đầu-với-kiểm-thử-tự-động)
- [Nền tảng (framework) kiểm thử tự động](#nền-tảng-framework-kiểm-thử-tự-động)
- [Tổng kết So Sánh](#tổng-kết-so-sánh)
- [Kết luận](#kết-luận)


`Người dùng bình thường`: Cách để automation testing trong ứng dụng winform

`Claude-3-Sonnet`: Để thực hiện automation testing trong ứng dụng WinForm, có một số công cụ và framework phổ biến có thể sử dụng. Dưới đây là một số gợi ý:

1. **Coded UI Test (CUIT)**: CUIT là một công cụ kiểm thử tự động được tích hợp sẵn trong Microsoft Visual Studio. Nó hỗ trợ kiểm thử giao diện người dùng trên nhiều loại ứng dụng, bao gồm WinForm. CUIT sử dụng mô hình đối tượng UI để định vị và tương tác với các đối tượng giao diện người dùng.
2. **TestStack.White**: TestStack.White là một framework mã nguồn mở dựa trên Windows Automation (.NET UI Automation) để kiểm thử ứng dụng Windows. Nó hỗ trợ WinForm, WPF, Windows Store Apps và nhiều loại ứng dụng khác.
3. **WinAppDriver**: WinAppDriver là một dịch vụ đi kèm với Windows Application Driver, cho phép thực hiện kiểm thử tự động trên các ứng dụng Windows. Nó hỗ trợ WinForm, WPF và Universal Windows Platform (UWP). WinAppDriver sử dụng WebDriver API giống như Selenium WebDriver để tương tác với ứng dụng.
4. **Ranorex**: Ranorex là một công cụ kiểm thử tự động thương mại dành cho các ứng dụng Windows, web và di động. Nó cung cấp một giao diện đơn giản để ghi lại và chỉnh sửa các bước kiểm thử, cũng như hỗ trợ tích hợp với các công cụ quản lý phiên bản.
5. **TestComplete**: TestComplete là một công cụ kiểm thử tự động của SmartBear Software, hỗ trợ kiểm thử các ứng dụng Windows, web, di động và nhiều loại ứng dụng khác. Nó cung cấp một môi trường tích hợp để tạo, thực thi và quản lý các bài kiểm thử.
Khi chọn công cụ, bạn nên cân nhắc các yếu tố như tính năng, khả năng tương thích, tài liệu hướng dẫn, cộng đồng hỗ trợ và chi phí. Ngoài ra, việc tích hợp với hệ thống quản lý mã nguồn, xây dựng và triển khai liên tục cũng là một yếu tố quan trọng cần xem xét.


Software testing là một cách để kiểm tra và xác nhận hoạt động của sản phẩm hoặc ứng dụng cụ thể. Nó có thể được xác nhận ở nhiều điểm khác nhau tại thời điểm trong quá trình phát triển phụ thuộc vào phương pháp và công cụ sử dụng. Kiểm thử thường bắt đầu sau khi tổng hợp requirement. Ở mức unit test, hoạt động test bắt đầu đồng thời vớ coding. Nhưng trái lại, ở mức intergration test, thì bắt đầu khi coding kết thúc. Testing được sử dụng để tìm bugs trong các ứng dụng, giúp tìm ra lỗi để xử lý trước khi nó làm treo ứng dụng. Mục đích là thỏa mãn yêu cầu người dùng và đảm bảo sản phẩm của phần mềm.

## Bắt đầu với kiểm thử tự động

Khi mà các yêu cầu cho kiểm thử tự động được thiết lập, nó bao gồm tạo ra các kịch bản test (test script) có liên quan. Việc tạo test script có thể chỉ được thực hiện bởi tester có kinh nghiệm, các tool thích hợp cũng như các chức năng cũng được phát triển. Tốn nguồn lực và giá thành cao nên cần cân nhắc những trường hợp nào có thể sử dụng automation test Một trong số những điểm để quyết định sử dụng automation test là:

- Những phần trong hệ thống mà yêu cầu không thay đổi thường xuyên
- Có thời gian để mô tả test thông qua các script
- Những phần cần sử dụng automation test cần đủ quan trọng để tương xứng với giá chi trả
- Sau khi test chức năng chúng ta muốn thực hiện test hiệu năng với nhiều người dùng ảo sử dụng cùng chung một kịch bản test.

Với phạm vi automation test đã mô tả, bước tiếp theo là chọn test tool. Những so sánh dưới đây có thể giúp chọn tool test.

![testing](https://boxxv.github.io/img/test/testing-automation-process.png "testing")

## Nền tảng (framework) kiểm thử tự động

So sánh 3 tool test tự động: `Selenium`, `QTP` (Quality Test Professional) và `Coded UI Test` (CUIT) with Visual Studio 2012.

Thông tin chung về tool

- Selenium được tạo bởi Jason Huggins. Là một testing tool mã nguồn mở. Sau đó Simon Stewart bắt đầu WebDriver (để khắc phục một số hạn chế của Selenium). Cả hai công cụ này được sáp nhập để có được một công cụ thử nghiệm tuyệt vời.
- HP QTP (Quick Test Professional) ban đầu được viết bởi Mercury Interactive. Nó là một phần của HP Quality Centre Suite (QC).
-Coded UI Test (CUIT) đã được giới thiệu bởi Microsoft cùng với Visual Studio 2010. Nó tích hợp với Team Foundation Server.

Thuận tiện sử dụng

**Chức năng Record và Playback:** Mỗi công cụ thử nghiệm có khả năng ghi lại những hành động và phát lại các hành động ghi lại. Selenium cung cấp những plug-in có tên Selenium IDE với Mozilla Firefox những hành động có thể được ghi lại. QTP cung cấp nút Record để ghi lại một kiểm thử mới. Record cho CUIT có thể được thực hiện bằng cách sử dụng hai công cụ khác nhau. Microsoft Test Manager có thể được sử dụng để ghi lại hành động mà sau đó có thể được chuyển đổi sang CUIT. Các Playback có thể sẵn sàng để chạy các test case trong một chế độ bán tự động (semi-automatic) trước khi chuyển sang script. Với Visual Studio CUIT cung cấp Coded UI Test Builder để ghi lại các hành động. Cả 3 công cụ này rất dễ dàng để ghi và phát lại.

**IDE và công cụ tester dùng để viết script:** Với Selenium IDE không có công cụ đặc biệt và công nghệ cụ thể để viết kịch bản. Chúng ta có thể chèn lệnh với “Table or Source View” khi có yêu cầu. QTP cung cấp Keyword View để hiển thị các bước thử nghiệm đồ họa hoặc Expert View trong đó cho thấy VB Script line. Đối với CUIT chúng ta có thể dễ dàng sử dụng Visual Studio IDE để viết kịch bản. Selenium IDE như là một plug-in với Mozilla Firefox. Với điều này chúng ta có thể tạo ra một bộ kiểm thử trong đó bao gồm các trường hợp thử nghiệm khác nhau. Với Selenium IDE, bạn có thể chuyển đổi recorded Selenium IDE scripts sang các ngôn ngữ khác nhau và sau khi chuyển đổi có thể chạy nó trong Selenium RC. Selenium RC có hai thành phần, một là "Selenium Server" và một là "Selenium Client". Với QTP IDE, trong lần đầu tiên, 3 add-in đầu tiên được cung cấp ActiveX, Visual Basic và Web. Liên kết khác nhau để thực hành tốt nhất, tính năng mới cho phiên bản hiện đang có sẵn với trang bắt đầu. Chúng ta có thể kiểm tra trường hợp hiện có mở hoặc tạo một hình mới. Với CUIT chúng ta có IDE như một record thể được thực hiện bằng cách sử dụng Visual Studio. Tất cả các tính năng của Visual Studio có thể áp dụng. Các script hỗ trợ với Visual Studio là một cách tuyệt vời để viết và gỡ lỗi. CUIT có lẽ có ưu thế hơn trong lĩnh vực này.

**Sự dễ dàng trong thực thi Test case:** Với Selenium IDE chúng ta có quyền lựa chọn thực hiện toàn bộ bộ kiểm thử đã record hoặc một một tescase tại một thời điểm. Nhờ vào các add-ins được load trong QTP IDE, các record và run window cho thấy các tab. Windows Application tab luôn luôn có sẵn. Kiểm thử có thể được thực hiện với nút Run, nó sẽ mở ra dialog box. Chúng ta có thể xác định vị trí cụ thể cho kết quả chạy và cung cấp các thông số nếu có. CUIT có thể được thực hiện với Visual Studio hoặc bằng cách sử dụng Microsoft Test Manager (MTM). Với MTM chúng tôi có thể cung cấp các thiết lập khác nhau để thực thi test case để thu thập rất nhiều thông tin trong khi thực hiện các test case. Thực hiện test có thể được thực hiện nhiều hơn hoặc ít hơn một cách chính xác với 3 tool. CUIT cung cấp các thiết lập kiểm thử khác nhau để thực hiện test case để thu thập dữ liệu khác nhau khi chúng ta cần phải tạo ra một lỗi. Cả 3 tool trên đều có thể thực hiện test case mà không cần sự can thiệp của con người.

**Platform support:**

- **Hỗ trợ ngôn ngữ:** Selenium sử dụng Selenese, ngôn ngữ nền tảng(platform language) để viết các lệnh Selenium (Selenium command . Có 3 category cơ bản cho các lệnh(command) - named actions, accessors and assertions. Để viết test có rất nhiều ngôn ngữ lập trình như C #, Java, Perl, PHP, Python hay Ruby. Script QTP có thể được viết bằng VBScript- một ngôn ngữ cấp cao(high-level language) với sự hỗ trợ cho tất cả mọi thứ trừ đa hình(polymorphism) và thừa kế(inheritance). Đối với CUIT chúng ta có thể viết kịch bản với Visual Studio với những cái mà chúng ta có thể sử dụng tất cả các khái niệm lập trình đối tượng nếu cần thiết. Viết mã VBScript là rất dễ dàng từ góc độ kiểm định viên. Mặc dù CUIT hỗ trợ lập trình hướng đối tượng, những người thử nghiệm có thể không thích vì nó liên quan đến rất nhiều kỹ năng để viết hoặc tùy biến các kịch bản tạo ra.

- **Hỗ trợ cho nhiều loại ứng dụng khác nhau:** Selenium chỉ hỗ trợ ứng dụng Web QTP hỗ trợ hầu hết các loại ứng dụng CUIT hỗ trợ cho ứng dụng Windows, Web, WPF, SharePoint, và các ứng dụng như Office Client Applications Dynamics CRM Web Client. Selenium có vẻ kém lợi thế hơn vì nó chỉ hỗ trợ ứng dụng web trong khi QTP hỗ trợ hầu hết các ứng dụng.

- **Hỗ trợ cho nhiều trình duyệt(browser):** Selenium hỗ trợ hầu hết các version của IE, Firefox, Safari, Opera và một vài trình duyệt khác. QTP hỗ trợ IE và Firefox. Nhưng cả hai đều không cung cấp đầy đủ hỗ trợ trình duyệt. CUIT hỗ trợ chỉ IE8, IE 9 và IE 10 (IE 10 chỉ support trên desktop). Không hỗ trợ cho IE6, IE7, Chrome, Opera hay Safari. Đối với việc hỗ trợ trình duyệt thì Selenium chiếm ưu điểm hơn.

- **Xử lý ngoại lệ:** Selenium IDE không hỗ trợ xử lý error đặc biệt là những lỗi không mong đợi(nó chỉ hỗ trợ HTML). Tuy nhiên Selenium RC sẽ cung cấp hỗ trợ cho nó (Selenium RC hỗ trợ ngôn ngữ .NET, Java, Perl, Python, PHP, Ruby). QTP cung cấp VBScript, có thể sử dụng câu lệnh On Error. CUIT hỗ trợ các ngôn ngữ cấp cao như C # hay VB.Net chúng ta có thể sử dụng try catch construct ở đây. Đối với xử lý ngoại lệ thì cả 3 tool đều có những hạn chế riêng của nó. CUIT được gợi ý là tốt trong việc nắm bắt các ngoại lệ cơ bản và viết code phù hợp.

- **Xác minh(Validation) và xác nhận(Assertion):** Selenium assertion có thể được sử dụng trong 3 chế độ assert verify và waitfor. Khi một "assert" fail, kiểm thử được hủy bỏ. Khi một "verify" (Soft Assertion) fail, việc kiểm thử sẽ tiếp tục thực hiện, ghi lại những failure. Cơ sở này có thể được sử dụng với TestNG framework. Các câu lệnh "waitfor" chờ các điều kiện để trở thành true. Nó sẽ thành công ngay lập tức nếu điều kiện là đã đúng. Tuy nhiên, nó sẽ thất bại và ngăn chặn sự kiểm tra nếu điều kiện không trở thành true trong thời gian chờ thực(current timeout). Đối với QTP có checkpoint: để xác minh ứng dụng khi test. Có 10 loại - Standard, Table, Image, Bitmap, Database, Text, Text Area, Page, Accessibility, and XML. Một check point là một điểm xác minh so sánh giá trị hiện tại với giá trị kỳ vọng. Nếu giá trị hiện tại và giá trị mong đợi khớp nhau, nó sẽ kết hợp nó tạo ra trạng thái Pass hoặc Fail. Chúng ta có thể sử dụng Coded UI Test Builder để thêm assertions cho UI control. Chúng ta cần thay đổi assertion condition theo yêu cầu (equal to, in between, contains…), cung cấp các giá trị mong đợi và tạo code cho nó. Sự kiện di chuột có thể được record thủ công nếu cần thiết. QTP and CUIT là tool tốt nhất trong trường hợp này.

- **Hỗ trợ cho đối tượng(object):** Thuộc tính đối tượng không được hỗ trợ bởi Selenium. Selenium object có thể được quản lý bởi UI element user extension. QTP đi kèm với in-built object repository. QTP object có tên thân thiện với người sử dụng. Coded UI Test code được viết với 3 phần chính cho UI controls. UIMap.designer.cs, UIMap.cs và UIMap.uitest. Việc đầu tiên là 2 tập tin vật lý khác nhau cho cùng một partial class trong khi file thứ 3 là một XML equivalent của tất cả các hành động được record bằng CUIT Builder. Bất kỳ yêu cầu thay đổi nào cũng có thể được kết hợp với sự giúp đỡ của partial class file. Chúng ta cũng có thể chỉnh sửa các UIMap với sự giúp đỡ của Coded UI Editor và tìm hiểu các thuộc tính của đối tượng. Các CUIT có thể hand code nếu cần. Coded UI Test bao gồm một thư viện API phong phú để code và công cụ record, playback. Coded UI Test có thể được mở rộng để hỗ trợ điều khiển tùy chỉnh. CUIT chiếm ưu thế hơn trong việc hỗ trợ đối tượng

## Tổng kết So Sánh

Bảng dưới cung cấp một cách khái quát cho các mục mà tool hỗ trợ

![testing](https://boxxv.github.io/img/test/comparison.png "testing")

_Chú thích_

![testing](https://boxxv.github.io/img/test/legend.png "testing")

## Kết luận

Trên đây là tổng quan cho thấy thế nào là test tự động, đã đến lúc chúng ta cần nghĩ đến test tự động trong vòng đời phát triển phần mềm (software development cycle) Nhìn vào 3 tool test tự động phổ biến Selenium, CUIT và QTP, xác định điểm mạnh, điểm yếu của chúng. Cuối cùng thì sự lựa chọn sử dụng tool nào phụ thuộc vào ngân sách và điểm mạnh của đội dự án(có thể sử dụng dễ dàng, quen thuộc với tool nào) Tuy nhiên đối với test ứng dụng Web thì cả 3 tool đều có những ưu điểm riêng. Đối với ứng dụng trên desktop thì CUIT và QTP được đề xuất lựa chọn.

-----
- [Comparison of Automated Testing Tools: Coded UI Test, Selenium and QTP](https://www.dotnetcurry.com/tools/1004/comparing-automated-testing-tools-codedui-qtp-selenium)
- [So sánh Tool test tự động: Coded UI Test, Selenium và QTP](https://viblo.asia/p/so-sanh-tool-test-tu-dong-coded-ui-test-selenium-va-qtp-57rVRqEER4bP)
- [Coded UI Test Automation Framework Tutorial](https://www.guru99.com/coded-ui-test-cuit.html)
- [Coded UI Test (CUIT)](https://viblo.asia/p/coded-ui-test-cuit-djeZ1Bq3lWz)
- [Tìm hiểu về QTP (phần 1)](https://viblo.asia/p/tim-hieu-ve-qtp-phan-1-ORNZqwDn50n)
- [Tìm hiểu về testing API sử dụng QTP](https://viblo.asia/p/tim-hieu-ve-testing-api-su-dung-qtp-eW65GdWaKDO)
- [Các loại kiểm thử tự động và một số hiểu lầm về kiểm thử tự động](https://viblo.asia/p/cac-loai-kiem-thu-tu-dong-va-mot-so-hieu-lam-ve-kiem-thu-tu-dong-Qbq5Qv1zKD8)
- [Làm thế nào để lựa chọn công cụ kiểm thử tự động hóa hiệu quả nhất (Hướng dẫn hoàn chỉnh)](https://viblo.asia/p/lam-the-nao-de-lua-chon-cong-cu-kiem-thu-tu-dong-hoa-hieu-qua-nhat-huong-dan-hoan-chinh-Qbq5QWGzZD8)