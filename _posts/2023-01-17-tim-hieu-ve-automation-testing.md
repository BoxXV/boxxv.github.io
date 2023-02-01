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

![Automation Testing](https://boxxv.github.io/img/2023/624462bdfaecc44bc3dd0c9d_testing-diagram.png "Automation Testing")

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

![Automation Testing](https://boxxv.github.io/img/2023/board.png "Automation Testing")

- Quick Test Profressional - (HP)
- Selenium
- Test Architect - (LogiGear)
- Ranorex
- Visual Studio CodedUI Testing
- TestComplete (SmartBear)
- SOAPUI - Web Services Testing (SmartBear)
- Appium
- Cucumber
- Silk Test
- Rspec


## Automation Testing Frameworks

- [QA Wolf](https://www.qawolf.com) - Cloud-based platform for zero-effort automated QA
- [Cypress](https://www.cypress.io) - Tool kiểm thử giao diện cho web, được viết bằng `javascript` và rất dễ sử dụng
- [Webdriver.io](https://webdriver.io) - Test framework for `node.js`
- [Jasmine](https://jasmine.github.io) - 1 trong 3 thư viện hỗ trợ `unit test` mạnh nhất cho `javascript`
- [Nightwatch](https://nightwatchjs.org) - open-source automated testing framework được cung cấp bởi Node.js và cung cấp các giải pháp E2E (từ đầu đến cuối) hoàn chỉnh để thử nghiệm tự động hóa với Selenium Javascript dành cho ứng dụng web, ứng dụng trình duyệt và trang web.
- [Robot Framework](https://robotframework.org) - giải pháp cho người mới trong lĩnh vực kiểm thử tự động
- [Selenium](https://www.selenium.dev) - open-source automation testing framework hỗ trợ nhiều loại ngôn ngữ lập trình như: Java, C #, Python, ...
- [Jest](https://jestjs.io) - JavaScript Testing Framework tập trung vào sự đơn giản
- [Puppeteer](https://developer.chrome.com/docs/puppeteer/) - 
- [Playwright](https://playwright.dev) - end-to-end testing cho các ứng dụng web hiện đại.


## Cơ hội nghề nghiệp

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
- [Đánh giá 100 công cụ kiểm thử phần mềm tốt nhất (Phần I)](https://viblo.asia/p/danh-gia-100-cong-cu-kiem-thu-phan-mem-tot-nhat-phan-i-4dbZNqgkKYM)
- [Đánh giá 100 công cụ kiểm thử phần mềm tốt nhất (Phần II)](https://viblo.asia/p/danh-gia-100-cong-cu-kiem-thu-phan-mem-tot-nhat-phan-ii-3P0lP9G85ox)
- [Công cụ Automation Testing tốt nhất](https://www.tma.vn/Hoi-dap/Cam-nang-nghe-nghiep/Cong-cu-Automation-Testing-tot-nhat-nam-2018/21596)
- [The Top 4 Open Source Tools That Make Appium Easier to Use](https://digital.ai/catalyst-blog/the-top-4-open-source-tools-that-make-appium-easier-to-use/)
- [Top 10 Automation Testing frameworks](https://www.testrigtechnologies.com/top-10-automation-testing-frameworks/)
- [Top 11 open-source test automation frameworks](https://techbeacon.com/app-dev-testing/top-11-open-source-testing-automation-frameworks-how-choose)
- [13 Best Test Automation Frameworks](https://www.lambdatest.com/blog/best-test-automation-frameworks-2021/)
- [18 BEST Automation Testing Tools](https://www.guru99.com/automated-testing-tools.html)
- []()
- [Phân biệt các role của QA Engineering: Skills, Tools, và Responsibilities trong một Testing Team](https://viblo.asia/p/phan-biet-cac-role-cua-qa-engineering-skills-tools-va-responsibilities-trong-mot-testing-team-Qpmleawnlrd)
- [Giới thiệu về WebDriverIO](https://viblo.asia/p/gioi-thieu-ve-webdriverio-gGJ59GN9ZX2)
- [VIẾT UNIT TEST CHO JAVASCRIPT VỚI JASMINE](https://toidicodedao.com/2015/04/02/viet-unit-test-cho-javascript-voi-jasmine/)
- [VIẾT UNIT TEST CHO JAVASCRIPT VỚI JASMINE – PHẦN 2](https://toidicodedao.com/2015/04/07/viet-unit-test-cho-javascript-voi-jasmine-phan-2/)
- [Angular Unit Testing](https://viblo.asia/p/angular-unit-testing-l5XRBV1kRqPe)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 1: Unit Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-1-unit-test-ByEZk96E5Q0)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 2: Integration Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-2-integration-test-bWrZn1ObKxw)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 3: End-to-End Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-3-end-to-end-test-aWj53kD156m)
- [Kiểm thử tự động cùng Robot Framework dành cho tester](https://viblo.asia/p/kiem-thu-tu-dong-cung-robot-framework-danh-cho-tester-aRBvXndbeWE)
- [Robot framework dành cho tester (Phần I)](https://viblo.asia/p/robot-framework-danh-cho-tester-phan-i-DzVkpopJenW)
- [Robot framework dành cho tester (Phần II)](https://viblo.asia/p/robot-framework-danh-cho-tester-phan-ii-xQMGJLPLkam)
- [Robot framework dành cho tester (Phần III)](https://viblo.asia/p/robot-framework-danh-cho-tester-phan-iii-EoDkQOPnGbV)
- [Robot framework dành cho tester (Phần IV)](https://viblo.asia/p/robot-framework-danh-cho-tester-phan-iv-mDYKDPZlKpx)
- [Phần 1: Tổng quan về Robot Framework, cài đặt Robot Framework](https://viblo.asia/p/phan-1-tong-quan-ve-robot-framework-cai-dat-robot-framework-63vKjAkV52R)
- [Phần 2: Robot Framework (Giới thiệu qua về các cấu trúc viết kịch bản cách khai báo biến trong robot framework)](https://viblo.asia/p/phan-2-robot-framework-gioi-thieu-qua-ve-cac-cau-truc-viet-kich-ban-cach-khai-bao-bien-trong-robot-framework-QpmleRx75rd)
- [Phần 3. Các kiến thức cơ bản trong robot framework như vòng lặp for, dictionary ...](https://viblo.asia/p/phan-3-cac-kien-thuc-co-ban-trong-robot-framework-nhu-vong-lap-for-dictionary-LzD5dRxwZjY)
- [Phần 4: Thư viện của Robot Framework, Builth](https://viblo.asia/p/phan-4-thu-vien-cua-robot-framework-builth-Eb85oAxjZ2G)
- [Phần 5: Robot Framework : Collections keyword làm việc với List](https://viblo.asia/p/phan-5-robot-framework-collections-keyword-lam-viec-voi-list-RnB5pAx6KPG)
- [Phần 6: Robot Framework ( Dictionary , Thư viện DateTime )](https://viblo.asia/p/phan-6-robot-framework-dictionary-thu-vien-datetime-4P856rNL5Y3)
- [Phần 7: Robot Framework - Cách tạo test case auto làm việc với API với phương thức GET](https://viblo.asia/p/phan-7-robot-framework-cach-tao-test-case-auto-lam-viec-voi-api-voi-phuong-thuc-get-3P0lP8nglox)
- [Phần 8: Robot Framework - Cách tạo test case auto làm việc với API (phương thức POST)](https://viblo.asia/p/phan-8-robot-framework-cach-tao-test-case-auto-lam-viec-voi-api-phuong-thuc-post-Az45bRzL5xY)
- [Robot Framework Làm việc với Database](https://viblo.asia/p/robot-framework-lam-viec-voi-database-aWj53m3bZ6m)
- [Giới thiệu về Selenium](https://viblo.asia/p/gioi-thieu-ve-selenium-jvElagRxKkw)
- [Tổng quan về Selenium và vai trò của các thành phần](https://tech.cybozu.vn/tong-quan-ve-selenium-va-vai-tro-cua-cac-thanh-phan-74a12/)
- [Những lý do các QA xuất phát từ developer frontend như ReactJs hay VueJs nên sử dụng công cụ kiểm thử cypress cho website thay vì selenium.](https://viblo.asia/p/nhung-ly-do-cac-qa-xuat-phat-tu-developer-frontend-nhu-reactjs-hay-vuejs-nen-su-dung-cong-cu-kiem-thu-cypress-cho-website-thay-vi-selenium-RnB5pyawKPG)
- [https://viblo.asia/tags/cypress](https://viblo.asia/tags/cypress)
- [https://viblo.asia/tags/jasmine](https://viblo.asia/tags/jasmine)
- [https://viblo.asia/tags/robot-framework](https://viblo.asia/tags/robot-framework)
- [https://viblo.asia/tags/selenium](https://viblo.asia/tags/selenium)
- [https://viblo.asia/tags/selenium-ide](https://viblo.asia/tags/selenium-ide)
- [https://viblo.asia/tags/selenium-webdriver](https://viblo.asia/tags/selenium-webdriver)

-----

- [Tìm hiểu về test plan](https://viblo.asia/p/tim-hieu-ve-test-plan-naQZReO0Kvx)
- [Test Strategy](https://viblo.asia/p/test-strategy-YWOZreRNKQ0)
- [Kỹ thuật kiểm thử - Kiểm thử hộp đen(Black box testing)](https://viblo.asia/p/ky-thuat-kiem-thu-kiem-thu-hop-denblack-box-testing1-V3m5WQEwZO7)
- [QA Engineer là gì? QC Engineer là gì?](https://isocert.org.vn/qa-engineer-la-gi-qc-engineer-la-gi-tim-hieu-ve-qa-engineer-va-qc-engineer)
- [Tất tần tật về QA - All about QA job Description, Roles, Duties and Career path.](https://viblo.asia/p/tat-tan-tat-ve-qa-all-about-qa-job-description-roles-duties-and-career-path-Az45byvqlxY)
- [How to Write Test Cases ( Hướng dẫn cách viết Testcases)](https://viblo.asia/p/how-to-write-test-cases-huong-dan-cach-viet-testcases-eW65GRY9lDO)
- [Làm thế nào để viết testcase cho người mới bắt đầu - Khái niệm và các loại test case](https://viblo.asia/p/lam-the-nao-de-viet-testcase-cho-nguoi-moi-bat-dau-khai-niem-va-cac-loai-test-case-V3m5Wj6WlO7)
- [Cách viết test case cho phần mềm](https://viblo.asia/p/cach-viet-test-case-cho-phan-mem-LzD5dx1w5jY)
- [Cách viết test case cho phần mềm - Viết Test Case từ User Story & Acceptance Criteria](https://viblo.asia/p/cach-viet-test-case-cho-phan-mem-viet-test-case-tu-user-story-acceptance-criteria-yMnKMMeNK7P)
- [Làm thế nào để quản lý test case tốt](https://viblo.asia/p/lam-the-nao-de-quan-ly-test-case-tot-gDVK23z0ZLj)
- [Mẫu Test Case tốt nhất kèm ví dụ](https://viblo.asia/p/mau-test-case-tot-nhat-kem-vi-du-bWrZnvnwZxw)
- [Kiểm thử độ bền là gì?](https://viblo.asia/p/kiem-thu-do-ben-la-gi-ORNZqbMMl0n)
- [Software Testing Metric - Chìa khoá để giải quyết mọi bài toán của Test Leaders](https://viblo.asia/p/software-testing-metric-chia-khoa-de-giai-quyet-moi-bai-toan-cua-test-leaders-naQZRREQZvx)
- [Test API sử dụng Pytest (Phần 1: Kiến thức cơ bản)](https://viblo.asia/p/test-api-su-dung-pytest-phan-1-kien-thuc-co-ban-GrLZDr435k0)
- [Test API sử dụng Pytest (Phần 2: Testcase Template và Dynamic Testing Function)](https://viblo.asia/p/test-api-su-dung-pytest-phan-2-testcase-template-va-dynamic-testing-function-1VgZvAvMKAw)
- [Sự khác nhau giữa Sanity Testing và Smoke Testing](https://viblo.asia/p/su-khac-nhau-giua-sanity-testing-va-smoke-testing-4dbZNJRLZYM)
- [Góc nhìn của một Tester về các dự án Agile](https://viblo.asia/p/goc-nhin-cua-mot-tester-ve-cac-du-an-agile-bWrZn4zO5xw)
- [Agile & Scrum](https://viblo.asia/p/agile-scrum-3Q75w8PQKWb)
- [Một "chớt" tâm sự của một Tester quèn gửi tới Dev team, PM, DM, PO,...](https://viblo.asia/p/mot-chot-tam-su-cua-mot-tester-quen-gui-toi-dev-team-pm-dm-po-ORNZqnXrl0n)
- [https://viblo.asia/tags/testcase](https://viblo.asia/tags/testcase)
- [https://viblo.asia/tags/cypress](https://viblo.asia/tags/cypress)
- [https://viblo.asia/u/oanhnguyen2403](https://viblo.asia/u/oanhnguyen2403)
- [https://viblo.asia/u/nguyen.hong.minh](https://viblo.asia/u/nguyen.hong.minh)
- [https://viblo.asia/u/tran.thi.tra.giang](https://viblo.asia/u/tran.thi.tra.giang)
- [https://viblo.asia/u/ngocyanl2k1](https://viblo.asia/u/ngocyanl2k1)
- [https://viblo.asia/u/thaoltp](https://viblo.asia/u/thaoltp)
- [NHỮNG CÂU HỎI PHỎNG VẤN QC // MANUAL TESTER // FRESHER](https://viblo.asia/p/nhung-cau-hoi-phong-van-qc-manual-tester-fresher-ddtcmt-n1j4l3vlVwl)
- [Bộ câu hỏi phỏng vấn tuyển dụng Tester](https://viblo.asia/p/bo-cau-hoi-phong-van-tuyen-dung-tester-vyDZOkEkZwj)
- [Top 10 Benefits of Automated Testing](https://testinium.com/blog/top-10-benefits-of-automated-testing-2/)
- [Test automation 101](https://bootcamp.uxdesign.cc/test-automation-264d219ac83)
- [What Is Full Stack QA or Tester? 4 Steps Guide For Beginners](https://www.opencodez.com/software-testing/become-full-stack-qa-engineer.htm)
- [ROADMAP TO QA AUTOMATION ENGINEER](https://synapse-qa.com/2020/11/15/roadmap-to-qa-automation-engineer/)
- [https://toolsqa.com/](https://toolsqa.com/)
- [QA Engineer](https://roadmap.sh/qa/)