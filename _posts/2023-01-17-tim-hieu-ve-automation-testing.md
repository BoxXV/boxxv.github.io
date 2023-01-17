---
layout: post
title: Tìm hiểu về Automation Testing
subtitle: 7 bước để trở thành một Automation Testing Engineer
image: "img/projects-bg.jpg"
tags:
- Automation
- Testing
- PerformanceTest
---

![Automation Testing](https://boxxv.github.io/img/2023/1-2.png "Automation Testing")

Làm thế nào để trở thành một Automation Testing Engineer? Như mọi người đều biết răng, kiểm thử tự động đang dần trở thành một xu hướng HOT để các bạn tìm hiểu, cũng như thị trường việc làm của công việc này ngày càng tăng. Vậy thì các bạn cần tìm hiểu những kiến thức gì, và cần có những kỹ năng gì để bước vào lĩnh vực này.

## I. Automation Test là gì? Khi nào nên sử dụng Automation Test?

Khi khái niệm Automation Test (kiểm tra tự động) ra đời, Tester chỉ cần viết một đoạn code hoặc sử dụng một số công cụ như Selenium, Test Complete, Jmetter… để chạy tự động tất cả các bước bao gồm nhập thông tin, click, kiểm tra kết quả, so sánh kết quả thực tế với kết quả giả định.

Nhiều loại test có thể làm auto, ví dụ như functional testing, performance/load testing, unit testing.

### Ưu điểm của Automation Test

![Automation Testing](https://boxxv.github.io/img/2023/MVP.png "Automation Testing")

1. Độ tin cậy cao: Test chạy chính xác theo quy trình đã định sẵn. vì vậy tránh được nhiều lỗi do con người tạo ra, ví dụ như nhập sai dữ liệu.
2. Khả năng lặp: Mình có thể test cách phần mềm xử lý (tính năng/hiệu năng) khi gặp tình huống chạy lặp đi lặp lại nhiều lần (cùng lúc) trên cùng script test. Đây còn gọi là performance/load testing.
3. Mình có thể lập trình nhiều test tinh vi hơn để thu về những thông tin ẩn từ ứng dụng. Ở điểm này thì Manual Test không thể làm được.
4. Test mang tính toàn diện cao. Mình có thể tạo ra một bộ test để bao quát hết tất cả tính năng trong ứng dụng.
5. Khả năng tái sử dụng: Mình có thể tái sử dụng test trên nhiều phiên bản khác nhau của ứng dụng, ngay cả khi có sự thay đổi giao diện. Nếu chạy Manual Test thì một test case mất một tiếng, ba môi trường tốn ba tiếng. Mà trong suốt quá trình phát triển sản phẩm, chúng ta phải lặp lại quá trình test vô số lần, dẫn đến mất thời gian nếu làm Manual Test. Thay vào đó, chỉ cần viết một script test thì mỗi lần deploy lên môi trường mới, mình chỉ cần thay đổi URL là test tự chạy được.
6. Chất lượng và hiệu suất phần mềm tốt hơn bởi vì mình có thể chạy nhiều test trong thời gian ngắn hơn với ít resource nhất.
7. Tốc độ cao: Automation Testing Tools giúp chạy test nhanh hơn test bằng tay. Do thực thi bởi máy nên tốc độ của kiểm thử tự động nhanh hơn nhiều so với tốc độ của con người. Nếu cần 5 phú để thực thi một test case một cách thủ công thì có thể người ta chỉ cần khoảng 30s để thực thi một cách tự động.
8. Có tính kinh  tế cao vì có thể giảm thiểu nguồn nhân lực làm kiểm tra hồi quy.

### Nhược điểm của Automation Test

1. Khó mở rộng, khó bảo trì: trong cùng một dự án, để mở rộng phạm vi cho kiểm thử tự động khó hơn nhiều so với kiểm thử thủ công vì cập nhật hay chỉnh sửa yêu cầu nhiều công việc như debug, thay đổi dữ liệu đầu vào và cập nhật code mới.
2. Khả năng bao phủ thấp: do khó mở rộng và đòi hỏi nhiều kỹ năng lập trình nên độ bao phủ của kiểm thử tự động thấp xét trên góc nhìn toàn dự án.
3. Vấn đề công cụ và nhân lực: hiện nay cũng có nhiều công cụ hỗ trợ kiểm thử tự động khá tốt nhưng chúng vẫn còn nhiều hạn chế. Ngoài ra nhân lực đạt yêu cầu (có thể sử dụng thành thạo các công cụ này) cũng không nhiều.
4. Nhiều tool có chi phí rất cao, ví dụ như commercial tool: HP Quick Test Pro.
5. Thường thì lương trả cho Automation Tester nhiều hơn Manual Tester, vì công việc đòi hỏi họ có kỹ năng cao hơn, ví dụ như phải biết code, phải viết được script.
6. Chi phí để phát triển và bảo trì test script cao. Ví dụ một test case nếu Manual Test thì mất 1 tiếng. Nhưng nếu đổi sang chạy Automation Test, cần chuẩn bị test script (mà trong trường hợp khó) thì phải mất 6-7 tiếng để viết test script. Người viết test script cần có kỹ năng lập trình và tool để chạy test. Vì vậy chi phí cho Automation Test cao hơn Manual Test.
7. Đòi hỏi Tester phải có kinh nghiệm technical và kỹ năng lập trình.
8. Đòi hỏi thời gian chuẩn bị dài hơn để thiết kế, cài đặt kỹ càng trước khi cần đưa dự án đi test.
9. Có những dự án không nên chạy Automation Test, nhưng nhiều Tester vẫn hiểu nhầm và chạy Automation Test, dẫn đến mất thời gian, resource, công sức. Ví dụ như khi test một chức năng quá phức tạp của một ứng dụng hoặc một GUI object thì phải chạy Manual Test.


### Những kỹ năng nào là cần thiết dành cho một Automation Tester?

1. Types testing: `Unit test`, `Intergration test`, `System test`, `Sanity test`, `Regression test`.... là gì?
2. Testing Techniques: Phân tích giá trị biên/Phân vùng tương đương/Biểu đồ kết quả/Đoán lỗi/... là gì?
3. Hiểu nguyên lý nhận dạng test objects. Nếu làm Web Automation Test cần nắm rõ HTML và XPath. Bạn có thể học hai mảng này ở W3School.
4. Hiểu nguyên lý lập trình, và thành thạo ít nhất một ngôn ngữ lập trình. Web Automation Engine được dùng phổ biến ở thị trường hiện nay là Selenium WebDriver, có kết hợp cho các ngôn ngữ Java, C#, Ruby, Python… Ngoài ra các bạn có thể tham khảo thêm các ngôn ngữ scripting phổ biến như VBScript, JavaScript hoặc Groovy nếu cần.
5. Không bỏ qua SQL và XML. Hai mảng này bạn có thể học tại TutorialsPoint và W3School. Đa số các dự án lập trình đều cần có cơ sở dữ liệu. XML được hiểu như một phần của portal database và SML cũng được sử dụng khá nhiều hiện nay.
6. Sử dụng thành thạo thư viện của Selenium WebDriver API bởi Selenium open source, dễ sử dụng, cộng đồng lớn.
7. Sử dụng thành thạo ít nhất 1 framework testing: Junit/TestNG/NUnit/... Từ đây sẽ giúp bạn rất nhiều trong việc build framework, hỗ trợ trong việc phân nhóm, quản lý testscript, report, prepare data/environment/browsers.
8. Những bạn muốn đi sâu vào thiết kế tốt framework/common library thì nên tìm hiểu sâu về software design pattern.
9. Sử dụng/build framework thành thạo từ Page Object Model pattern.
9. Làm Automation Tester là liên quan đến coding nên các bạn cần quan tâm đến những kỹ năng của code như debug, source version control, coding convention, unit testing… cách sử dụng IDE: Visual Studio, Eclipse, IntelliJ..., làm việc với database...
10. Nên ham học hỏi những cái mới trong mảng automation testing: build tools: Maven, ANT..., CI/CD: Jenkins, TeamCity, CircleCI, TFS, Docker.., Clould: AWS, Saucelab, Browserstack, Testingbot..., big data: Hadoop, HBase, Hive..., mobile: Appinum...


## Automation Testing Tool

- Quick Test Profressional - (HP)
- Selenium
- Test Architect - (LogiGear)
- Ranorex
- Visual Studio CodedUI Testing
- TestComplete (SmartBear)
- SOAPUI - Web Services Testing (SmartBear)


## Automation Testing Frameworks




## Tổng kết

Cách mạng công nghiệp lần thứ tư đánh dấu kỷ nguyên vạn vật kết nối Internet. Nó xảy ra dựa trên sự hội tụ của nhiều công nghệ trong đó có công nghệ cốt lõi có công nghệ thông tin với sự phát triển không ngừng của công nghệ Internet từ thời kỳ kết nối nội dung như email đến mạng xã hội, Internet vạn vật, Internet kết nối thiết bị máy móc kết nối quá trình vận hành của các nhà máy. Ngoài công nghệ cốt lõi còn có sự hội tụ của công nghệ in 3D, công nghệ vật liệu tiên tiến, công nghệ lưu trữ…

Hiện nay, nền công nghiệp 4.0 đang phát triển mạnh mẽ, kéo theo sự phát triển của rất nhiều ngành nghề, đặc biệt là ngành công nghệ thông tin. Do đó, yêu cầu về nhân lực trong mảng này cũng đòi hỏi cac ứng viên cần phải có kỹ năng tốt hơn nữa về lập trình, technical, các kỹ năng về automation....

Nếu search trên các trang mạng tuyển dụng lớn như ITviec, Vietnamworks, LinkIn, Indeed, Dice, Monster, CareerBuilder … thì bạn sẽ thấy có vô vàn kết quả với các từ khóa tìm kiếm như:

- Test Automation Engineer
- Automation Developer
- Automation Testing/Automation Tester
- QA Automation Engineer
- Software Development Engineer in Test (SDET)

Từ đây, bạn có thể thấy được nhu cầu tuyển một QA có kiến thức và kinh nghiệm về automation test là rất lớn. Do đó, đủ để hiểu automation test sẽ là tiềm năng lớn cho tương lai của mảng Test nói riêng và công nghệ thông tin nói chung.


-----
Tham khảo:

- [Tìm hiểu về Automation Testing](https://viblo.asia/p/tim-hieu-ve-automation-testing-aWj532DQl6m)
- [Automation Test là gì? Khi nào nên sử dụng Automation Test?](https://itviec.com/blog/automation-test/)
- [7 bước để trở thành một Automation Testing Engineer](https://viblo.asia/p/7-buoc-de-tro-thanh-mot-automation-testing-engineer-4P856XBGZY3)
- [Automation Test là gì? Khi nào nên sử dụng Automation Test?](https://itviec.com/blog/automation-test/)
- [NHỮNG CÂU HỎI PHỎNG VẤN QC // MANUAL TESTER // FRESHER](https://viblo.asia/p/nhung-cau-hoi-phong-van-qc-manual-tester-fresher-ddtcmt-n1j4l3vlVwl)
- [Top 10 Benefits of Automated Testing](https://testinium.com/blog/top-10-benefits-of-automated-testing-2/)
- [Test automation 101](https://bootcamp.uxdesign.cc/test-automation-264d219ac83)
- [What Is Full Stack QA or Tester? 4 Steps Guide For Beginners](https://www.opencodez.com/software-testing/become-full-stack-qa-engineer.htm)
- [ROADMAP TO QA AUTOMATION ENGINEER](https://synapse-qa.com/2020/11/15/roadmap-to-qa-automation-engineer/)
