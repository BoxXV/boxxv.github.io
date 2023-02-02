---
layout: post
title: Tìm hiểu về Kiểm Thử Tự Động
subtitle: 7 bước để trở thành một Automation Testing Engineer
image: "img/tdd.png"
tags:
- Automation
- Testing
- PerformanceTest
---

![Automation Testing](https://boxxv.github.io/img/test/1-2.png "Automation Testing")

Làm thế nào để trở thành một Automation Testing Engineer? Như mọi người đều biết răng, kiểm thử tự động đang dần trở thành một xu hướng HOT để các bạn tìm hiểu, cũng như thị trường việc làm của công việc này ngày càng tăng. Vậy thì các bạn cần tìm hiểu những kiến thức gì, và cần có những kỹ năng gì để bước vào lĩnh vực này.

## Automation Test là gì? Khi nào nên sử dụng Automation Test?

Khi khái niệm Automation Test (kiểm tra tự động) ra đời, Tester chỉ cần viết một đoạn code hoặc sử dụng một số công cụ như Selenium, Test Complete, Jmetter… để chạy tự động tất cả các bước bao gồm nhập thông tin, click, kiểm tra kết quả, so sánh kết quả thực tế với kết quả giả định.

Nhiều loại test có thể làm auto, ví dụ như functional testing, performance/load testing, unit testing.

### Ưu điểm của Automation Test

![Automation Testing](https://boxxv.github.io/img/test/MVP.png "Automation Testing")

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

![Automation Testing](https://boxxv.github.io/img/test/624462bdfaecc44bc3dd0c9d_testing-diagram.png "Automation Testing")

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

![Automation Testing](https://boxxv.github.io/img/test/board.png "Automation Testing")

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


## Unit Testing Frameworks

- [`JUnit`](https://junit.org) & [`TestNG`](https://testng.org) cho **Java**
- [`MSTest`](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest), [`NUnit`](https://nunit.org) & [`xUnit`](https://xunit.net) cho C#
- [`Unittest`](https://docs.python.org/3/library/unittest.html) & [`pytest`](https://pytest.org) cho **Python**
- [`Mocha`](https://mochajs.org), [`Jasmine`](https://jasmine.github.io) hoặc [`Chai`](https://www.chaijs.com) cho **JavaScripts**
- [`Jest`](https://github.com/facebook/jest), [`Mocha`](https://github.com/mochajs/mocha), [`Chai`](https://github.com/chaijs/chai), [`Karma`](https://github.com/karma-runner/karma), [`Jasmine`](https://github.com/jasmine/jasmine), [`Enzyme`](https://github.com/enzymejs/enzyme), [`React-testing-library`](https://github.com/testing-library/react-testing-library), [`React test utils and test renderer`](https://reactjs.org/docs/test-utils.html), [`Cypress IO`](https://github.com/cypress-io/cypress), [`Pupeeter`](https://github.com/puppeteer/puppeteer), [`Bit`](https://bit.dev) cho **React**


## Test-driven Development (TDD) Tool

- [`Jest`](https://jestjs.io) cho unit tests
- [`ESLint`](https://eslint.org) cho linting
- [`Prettier`](https://prettier.io) cho formatting
- `Husky` và [`lint-staged`](https://www.npmjs.com/package/lint-staged?activeTab=dependencies) để pre-commit Git hooks

![Test-driven Development](https://boxxv.github.io/img/test/5y1ipmh3te6h6pqvwcop.png "TDD")

> [Công cụ và Thư viện cần thiết cho Fullstack](https://boxxv.github.io/2022/01/01/tools-and-library-for-js-development/)  
> [Top Visual Studio Extensions for Developers](https://boxxv.github.io/2020/01/08/top-visual-studio-extensions/)  
> [Thư Viện Và Framework quan trọng bạn cần biết 2022](https://boxxv.github.io/2022/08/20/essential-libraries-and-frameworks-you-should-know-about/)  


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
- [Tìm hiểu sơ lược về kiểm thử tự động](https://viblo.asia/p/tim-hieu-so-luoc-ve-kiem-thu-tu-dong-oOVlYwbVK8W)
- [AUTOMATION: A GUIDE TO TESTING](https://www.reply.com/net-reply-uk/en/content/automation-a-guide-to-testing)
- [7 bước để trở thành một Automation Testing Engineer](https://viblo.asia/p/7-buoc-de-tro-thanh-mot-automation-testing-engineer-4P856XBGZY3)
- [Automation Test là gì? Khi nào nên sử dụng Automation Test?](https://itviec.com/blog/automation-test/)
- [Đánh giá 100 công cụ kiểm thử phần mềm tốt nhất (Phần I)](https://viblo.asia/p/danh-gia-100-cong-cu-kiem-thu-phan-mem-tot-nhat-phan-i-4dbZNqgkKYM)
- [Đánh giá 100 công cụ kiểm thử phần mềm tốt nhất (Phần II)](https://viblo.asia/p/danh-gia-100-cong-cu-kiem-thu-phan-mem-tot-nhat-phan-ii-3P0lP9G85ox)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần I](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-i-RQqKLMjbZ7z)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần II](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-ii-GrLZDVDB5k0)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần III](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-iii-YWOZrM4RKQ0)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần IV](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-iv-Ljy5VrDo5ra)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần V](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-v-jvElaXxoZkw)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần VI](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-vi-oOVlY1d4l8W)
- [100+ Công Cụ Kiểm Thử Phần Mềm - Phần VII](https://viblo.asia/p/100-cong-cu-kiem-thu-phan-mem-phan-vii-3P0lPyab5ox)
- [Công cụ Automation Testing tốt nhất](https://www.tma.vn/Hoi-dap/Cam-nang-nghe-nghiep/Cong-cu-Automation-Testing-tot-nhat-nam-2018/21596)
- [The Top 4 Open Source Tools That Make Appium Easier to Use](https://digital.ai/catalyst-blog/the-top-4-open-source-tools-that-make-appium-easier-to-use/)
- [Top 10 Automation Testing frameworks](https://www.testrigtechnologies.com/top-10-automation-testing-frameworks/)
- [Top 11 open-source test automation frameworks](https://techbeacon.com/app-dev-testing/top-11-open-source-testing-automation-frameworks-how-choose)
- [13 Best Test Automation Frameworks](https://www.lambdatest.com/blog/best-test-automation-frameworks-2021/)
- [18 BEST Automation Testing Tools](https://www.guru99.com/automated-testing-tools.html)
- [Những công cụ kiểm thử tự động phổ biến năm 2020](https://viblo.asia/p/nhung-cong-cu-kiem-thu-tu-dong-pho-bien-nam-2020-LzD5dgrYljY)
- [Top 5 công cụ kiểm thử API](https://viblo.asia/p/top-5-cong-cu-kiem-thu-api-RQqKLOXz57z)
- [21 Công cụ kiểm tra API tốt nhất (Part1)](https://viblo.asia/p/21-cong-cu-kiem-tra-api-tot-nhat-part1-Qpmle1LNlrd)
- [21 Công cụ kiểm tra API tốt nhất (Part2)](https://viblo.asia/p/21-cong-cu-kiem-tra-api-tot-nhat-part2-Eb85oOAj52G)
- [Phân biệt các role của QA Engineering: Skills, Tools, và Responsibilities trong một Testing Team](https://viblo.asia/p/phan-biet-cac-role-cua-qa-engineering-skills-tools-va-responsibilities-trong-mot-testing-team-Qpmleawnlrd)
- [Giới thiệu về WebDriverIO](https://viblo.asia/p/gioi-thieu-ve-webdriverio-gGJ59GN9ZX2)
- [VIẾT UNIT TEST CHO JAVASCRIPT VỚI JASMINE](https://toidicodedao.com/2015/04/02/viet-unit-test-cho-javascript-voi-jasmine/)
- [VIẾT UNIT TEST CHO JAVASCRIPT VỚI JASMINE – PHẦN 2](https://toidicodedao.com/2015/04/07/viet-unit-test-cho-javascript-voi-jasmine-phan-2/)
- [Sử dụng Jasmine và Karma với AngularJS](https://viblo.asia/p/su-dung-jasmine-va-karma-voi-angularjs-73KbvZzzvmWB)
- [Angular Unit Testing](https://viblo.asia/p/angular-unit-testing-l5XRBV1kRqPe)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 1: Unit Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-1-unit-test-ByEZk96E5Q0)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 2: Integration Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-2-integration-test-bWrZn1ObKxw)
- [Tự động test (Automation Testing) cho trang web ASP.NET Core 2.0 (Phần 3: End-to-End Test)](https://viblo.asia/p/tu-dong-test-automation-testing-cho-trang-web-aspnet-core-20-phan-3-end-to-end-test-aWj53kD156m)
- [Automated testing for Terraform](https://viblo.asia/p/automated-testing-for-terraform-Ljy5V7O9Kra)
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
- [ROADMAP TO QA AUTOMATION ENGINEER](https://synapse-qa.com/2020/11/15/roadmap-to-qa-automation-engineer/)
- [https://toolsqa.com/](https://toolsqa.com/)
- [Roadmap QA Engineer](https://roadmap.sh/qa/)