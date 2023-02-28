---
layout: post
title: Tìm hiểu mô hình TDD (Test - Driven Development) và cách áp dụng
subtitle: Lập trình TDD, có nên hay không?
image: "img/tdd.png"
tags:
- Automation
- Testing
- Driven
- TDD
---

![Automation Testing](https://boxxv.github.io/img/test/0_f2vFclaitRRo1w2i.webp "Automation Testing")

Gần đây, mô hình phát triển TDD (Test Driven Development) đang trở nên hot, được áp dụng nhiều. Mô hình này dựa trên khái niệm: Với mỗi chức năng, ta viết Unit Test trước, sau đó viết hàm hiện thực chức năng để unit test pass. Một số công ty ở Việt Nam cũng đang áp dụng mô hình này, trong khi phỏng vấn xin việc cũng có.


## I. Unit testing

![Unit Testing](https://boxxv.github.io/img/test/sketch.png "Unit Testing")

### Tại sao bắt đầu viết unit test lại khó đến vậy?

Cách đây khoảng 6 năm, tôi muốn viết unit test để tự động hóa việc kiểm thử ứng dụng mà tôi đang tham gia xây dựng. Đó là những gì một nhà phát triển giỏi làm và tôi mong muốn trở thành một nhà phát triển giỏi.

**Nhưng bằng cách nào?**

Ứng dụng mà tôi tham gia xây dựng không có bất kỳ bài kiểm tra unit test nào để tự động hóa việc kiểm thử. Chúng tôi phải kiểm tra các chức năng hoàn toàn bằng cơm, đây là một công việc lặp đi lặp lại rất nhàm chán và bỏ sót nhiều bug (QC rất thích điều này, còn tôi thì không).

Tôi muốn thay đổi điều này và đã tìm thấy giải pháp là sử dụng unit test sau khi lang thang trên Google. Tôi đã thử làm theo ví dụ trong các hướng dẫn này và các ví dụ này chạy ngon lành. Tôi nghĩ rằng mình đã tìm thấy kim chỉ nam và suýt nữa đã làm như Acsimet đã từng làm cách đây hơn 2000 năm.

Tuy nhiên khi tôi muốn viết unit test cho dự án thực tế của tôi thì không áp dụng được. Các ví dụ mà tôi làm theo thường rất đơn giản, chẳng hạn như một chương trình cho phép cộng, trừ, nhân, chia hai số nguyên.

Trong khi ứng dụng mà tôi muốn viết unit test khá phức tạp: có giao diện Frontend và Backend, có các API xử lý business ở đằng sau và hầu hết thực hiện các thao tác CRUD (Create, Read, Update, Delete) với cơ sở dữ liệu.

Vấn đề ở đây là tôi cần viết unit test cho cái gì? Vì ứng dụng có rất nhiều thành phần khác nhau, từ UI đến API, business logic tới repository, database, ...

Một vấn đề khác là mọi người luôn nói, "các bài kiểm tra unit test là quan trọng. Bạn phải làm chúng!" và sau đó không bao giờ nói cho tôi biết _làm thế nào_  để viết chúng và làm thế nào để viết chúng thật tốt.

Loạt bài này trình bày một số thứ tôi đã học được và sử dụng trong công việc của tôi. Tôi đã học được rất nhiều về kiểm thử và đặc biệt là kiểm thử đơn vị tự động, và tôi hy vọng rằng một số điều tôi học được sẽ hữu ích cho độc giả của tôi.

**Có nên viết unit test cho mọi thứ không?**

Câu trả lời ngắn gọn là `KHÔNG`

Không phải tất cả mọi thứ đều cần phải được kiểm tra bằng unit test. Các đoạn mã có thể không bao giờ thay đổi, hoặc không quan trọng đối với chức năng chính của hệ thống, hoặc rất khó để viết unit test hoặc đơn giản là quá lãng phí khi viết unit test, ...

Ngoài ra, chính xác khi nào và tại sao một thứ gì đó cần được viết unit test. Không có một kế hoạch kiểm thử nào phù hợp với tất cả. Mọi hệ thống đều khác nhau, mọi nhu cầu đều khác nhau, và bạn phải đánh giá phạm vi kiểm thử cần thiết dựa trên thiết kế và độ phức tạp của hệ thống bạn đang xây dựng, chưa kể thời gian thực hiện các kiểm tra đó.

**Vậy chúng ta nên viết unit test cho cái gì?**

Chúng ta nên viết unit test cho bất cứ điều gì là:
- Quan trọng đối với toàn bộ chức năng của ứng dụng.
- Đã biết hoặc có khả năng hỏng hóc cao.
- Có khả năng thay đổi trong tương lai.

Nói cách khác: bạn nên kiểm tra mã nào quan trọng, dễ hỏng hoặc có khả năng thay đổi.

Nói một cách đơn giản và dễ hiểu nhất thì nên viết unit test cho:
- Các lớp thư viện, lớp hạ tầng dùng chung cho nhiều project.
- Các lớp tầng business logic.
- Các lớp controller của Web UI và Web API.


## II. Unit testing C#

**Làm thế nào để chúng tôi viết unit test trong C#?**

Tôi rất vui vì bạn đã hỏi điều đó. Chính xác thì chúng ta phải viết unit test như thế nào?

Có rất nhiều thư viện cho unit test có sẵn trong thế giới .NET như [MSTest](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest), [NUnit](https://nunit.org), [XUnit](https://xunit.net) và các thư viện khác.
- `msTest`: mature, slow. Là khung kiểm thử của Microsoft cho tất cả các ngôn ngữ .NET. Nó có thể mở rộng và hoạt động với cả .NET CLI và Visual Studio.
- `NUnit`: mature, feature packed, fast. Là một khuôn khổ kiểm tra đơn vị cho tất cả các ngôn ngữ .NET. Ban đầu được chuyển từ JUnit, bản phát hành sản xuất hiện tại đã được viết lại với nhiều tính năng mới và hỗ trợ cho một loạt các nền tảng .NET. NUnit cũng là một dự án của .NET Foundation.
- `xUnit.net`: new, fast. Là một công cụ kiểm thử đơn vị miễn phí, mã nguồn mở, tập trung vào cộng đồng cho .NET. Được viết bởi nhà phát triển ban đầu NUnit v2, xUnit.net là công nghệ mới nhất để kiểm tra đơn vị các ứng dụng .NET. xUnit.net hoạt động với ReSharper, CodeRush, TestDriven.NET và Xamarin. Đây là một dự án thuộc .NET Foundation và hoạt động theo quy tắc ứng xử của .NET Foundation.

Đây là những thứ phổ biến nhất và chúng hoạt động theo những cách tương tự nhau. Tuy nhiên, theo ý kiến ​​của tôi xUnit mang lại sự dễ sử dụng và khả năng tái sử dụng tốt nhất.

![Unit Testing](https://boxxv.github.io/img/test/01_24.06.jpg "Unit Testing")

> [Bảng Cheat-Sheet tham khảo cho Unit Test dễ dàng hơn](https://viblo.asia/p/bang-cheat-sheet-tham-khao-cho-unit-test-de-dang-hon-aWj53vR8l6m)

### 1. Unit Test trong C# với MSTest

![Unit Testing](https://boxxv.github.io/img/test/test-project.webp "Unit Testing")

![Unit Testing](https://boxxv.github.io/img/test/test-explorer-toolbar-diagram-17-0.png "Unit Testing")

> [Walkthrough: Create and run unit tests for managed code](https://msdn.microsoft.com/en-us/library/ms182532.aspx)  
> [Phần 1: Cách viết Unit Test trong C#](http://duyanhpham.com/phan-1-cach-viet-unit-test-trong-c-sharp/)  
> [Phần 2: Sử dụng Unit Test để cải thiện code](http://duyanhpham.com/phan-2-su-dung-unit-test-de-cai-thien-code/)


### 2. Unit Test trong C# với NUnit

Trước đây, để viết Unit Test trong C#, ta thường phải tạo một project test riêng, sử dụng thư viện MSTest của Microsoft. MSTest hỗ trợ khá nhiều chức năng: Test dữ liệu từ database, đo performance hệ thống, xuất dữ liệu report. Tuy nhiên, do MSTest đi kèm với Visual Studio, không thể chạy riêng rẽ, lại khá nặng nề, do đó NUnit được nhiều người ưa thích hơn. NUnit có 1 bộ runner riêng, có thể chạy UnitTest độc lập không cần VisualStudio, ngoài ra nó cũng hỗ trợ một số tính năng mà MSTest không có (parameter test, Assert Throw).

> [[TUTORIAL] VIẾT UNIT TEST TRONG C# VỚI NUNIT](https://toidicodedao.com/2015/08/25/tutorial-viet-unit-test-trong-c-voi-nunit/)


### 3. Unit Test trong C# với [xUnit](xunit.net)

XUnit là một framework unit test cho .NET cung cấp một cách dễ dàng để viết code, chạy và debug các bài kiểm tra unit test.

Trong xUnit, một bài kiểm tra cơ bản là một phương thức trong lớp công khai, không có tham số hoặc giá trị trả về, được gắn nhãn bằng thuộc tính Fact, như sau:

```cs
public class TestCases
{
    [Fact]
    public void ClassName_MethodName_ExpectedResult() 
    {
        // Arrange
        
        // Fact
        
        // Assert
    }
}
```

Tại thời điểm này, bài kiểm tra trên chính xác là không có gì. Để điền vào những gì bài kiểm tra nên làm, chúng ta có thể làm theo phương pháp "Arrange, Act, Assert."

> LƯU Ý: Bạn có thể thiết lập xUnit để chạy các bài kiểm tra với đầu vào và đầu ra bằng thuộc tính`Theory]`, hãy xem bài viết ["Sử dụng xUnit để kiểm tra mã C# của bạn"](https://comdy.vn/unit-test/su-dung-xunit-de-kiem-tra-ma-c-sharp-cua-ban/#tao-theory-trong-xunit-7) để biết một ví dụ tuyệt vời. Chúng ta sẽ tìm hiểu kỹ hơn về vấn đề này trong phần sau của loạt bài này.

**Arrange, Act, Assert (AAA)**
Cụm từ "Arrange, Act, Assert" hay AAA là một cách hay để ghi nhớ cấu trúc của một bài kiểm tra unit test.
- `Arrange`:  có nghĩa là để thiết lập môi trường thử nghiệm cần thiết và các phụ thuộc. Điều này có thể có nghĩa là tạo một tập hợp dữ liệu thử nghiệm tốt đã biết hoặc tạo mock của một phần phụ thuộc mà chúng ta không muốn kiểm tra. Tóm lại, "Arrange" có nghĩa là "tạo ra những gì bài kiểm tra cần để chạy."
- `Act`:  có nghĩa là thực thi mã cần được kiểm tra, đã được thiết lập trong bước Arrange.
- `Assert`:  có nghĩa là kiểm tra kết quả và đầu ra và xác nhận rằng chúng là những gì chúng ta mong đợi.

Ví dụ dưới đây là một bài kiểm tra unit test có sử dụng mock:

```cs
[Fact]
public void PlayerService_GetAllPlayers_InvalidLeague()
{
    //Arrange
    var mockLeagueRepo = new MockLeagueRepository().MockIsValid(false);

    var playerService = new PlayerService(new MockPlayerRepository().Object,
        new MockTeamRepository().Object,
        mockLeagueRepo.Object);

    //Act
    var allPlayers = playerService.GetForLeague(1);

    //Assert
    Assert.Empty(allPlayers);
    mockLeagueRepo.VerifyIsValid(Times.Once());
}
```

Đừng lo lắng về đoạn mã này; bây giờ, tất cả những gì bạn cần nhớ là mô hình "Arrange, Act, Assert". Chúng ta sẽ xem xét chính xác đoạn mã này làm gì trong phần tiếp theo của loạt bài này.

Ở phần tiếp theo, chúng tôi sẽ trình bày cách sử dụng "mock" cho phép chúng ta dễ dàng tạo và thiết lập các lớp giả lập để thử nghiệm (cũng như tìm hiểu chính xác "mock" là gì).

> [Sử dụng Moq để viết unit test trong ASP.NET Core](https://comdy.vn/unit-test/su-dung-moq-de-viet-unit-test-trong-asp-net-core/)
> [TDD VỚI XUNIT TRÊN DỰ ÁN .NET](https://sinhnx.dev/lap-trinh/tdd-xunit-dotnet)


![Unit Testing](https://boxxv.github.io/img/test/unit-testing-framework-17-2048.webp "Unit Testing")


## III. Mô hình TDD (Test - Driven Development)

Phát triển hướng kiểm thử TDD (Test-Driven Development) là một phương pháp tiếp cận cải tiến để phát triển phần mềm trong đó kết hợp phương pháp Phát triển kiểm thử trước (Test First Development) và phương pháp Điều chỉnh lại mã nguồn (Refactoring).

Mục tiêu quan trọng nhất của TDD là hãy nghĩ về thiết kế của bạn trước khi viết mã nguồn cho chức năng. Một quan điểm khác lại cho rằng TDD là một kỹ thuật lập trình. Nhưng nhìn chung, mục tiêu của TDD là viết mã nguồn sáng sủa, rõ ràng và có thể chạy được.

### 1.TDD là gì?
TDD (Test Driven Development) là một phương thức làm việc, hay một quy trình viết mã hiện đại. Lập trình viên sẽ thực hiện thông qua các bước nhỏ (BabyStep) và tiến độ được đảm bảo liên tục bằng cách viết và chạy các bài test tự động (automated tests). Quá trình lập trình trong TDD cực kỳ chú trọng vào các bước liên tục sau:

1. Viết 1 test cho hàm mới. Đảm bảo rằng test sẽ fail.
2. Chuyển qua viết code sơ khai nhất cho hàm đó để test có thể pass.
3. Tối ưu hóa đoạn code của hàm vừa viết sao cho đảm bảo test vẫn pass và tối ưu nhất cho việc lập trình kế tiếp
4. Lặp lại cho các hàm khác từ bước 1

Thực tế, nên sử dụng UnitTestFramework cho TDD (như JUnit trong Java), chúng ta có thể có được môi trường hiệu quả vì các test được thông báo rõ rang thông qua màu sắc:
- Đỏ: test fail, chuyển sang viết function cho test pass
- Xanh lá: viết một test mới hoặc tối ưu code đã viết trong màu đỏ.

### 2. 3 điều luật khi áp dụng TDD
1. Không cho phép viết bất kỳ một mã chương trình nào cho tới khi nó làm một test bị fail trở nên pass.
2. Không cho phép viết nhiều hơn một unit test mà nếu chỉ cần 1 unit test cung đã đủ để fail. Hãy chuyển sang viết code function để pass test đó trước.
3. Không cho phép viết nhiều hơn 1 mã chương trình mà nó đã đủ làm một test bị fail chuyển sang pass.

### 3. Mô hình chu trình TDD


### 4. Các cấp độ TDD
1. Mức chấp nhận (Acceptance TDD (ATDD)): với ATDD thì bạn viết một test chấp nhận đơn (single acceptance test) hoặc một đặc tả hành vi (behavioral specification) tùy theo cách gọi của bạn; mà test đó chỉ cần đủ cho các mã chường trình sản phẩm thực hiện (pass or fail) được test đó. Acceptance TDD còn được gọi là Behavior Driven Development (BDD).
2. Mức lập trình (Developer TDD): với mức này bạn cần viết một test lập trình đơn (single developer test) đôi khi được gọi là unit test mà test đó chỉ cần đủ cho các mã chường trình sản phẩm thực hiện (pass or fail) được test đó. Developer TDD thông thường được gọi là TDD.

### 5. Các lỗi thường gặp khi áp dụng TDD
- Không quan tâm đến các test bị fail
- Quên đi thao tác tối ưu sau khi viết code cho test pass
- Thực hiện tối ưu code trong lúc viết code cho test pass => không nên như vậy
- Đặt tên các test khó hiểu và tối nghĩa
- Không bắt đầu từ các test đơn giản nhất và không theo các baby step.
- Chỉ chạy mỗi test đang bị fail hiện tại
- Viết một test với kịch bản quá phức tạp

### 6. Các ví dụ tham khảo về TDD

- Ngắn:
  * Chapter 6 – Agile principles, patterns, and practices in C# – by Martin C. Robert, Martin Micah. Khá thú vị. Xem online tại đây.
  * Phần 3, 4, 5 của Craftsman.
- Trung bình:
  * Part I – Test-Driven Development by example – Kent Beck.
  * Part III – Test-Driven Development: A practical guide – David Astels.
  * Phần 6, 7, 8, 9, 10 của Craftsman.
- Dài:
  * Part II – Test-Driven Development in Microsoft .NET – James W. Newkirk, Alexei A. Vorontsov.
  * Part III – Growing object-oriented software, guided by test – Steve Freeman, Nat Pryce.

### 7. Các công cụ hỗ trợ
Các công cụ phục vụ cho TDD, thường là các nền tảng cho kiểm thử mã nguồn mức đơn vị (unit test): 

- [`JUnit`](https://junit.org) & [`TestNG`](https://testng.org) cho **Java**
- [`MSTest`](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest), [`NUnit`](https://nunit.org) & [`xUnit`](https://xunit.net) cho **C#**
- [`Unittest`](https://docs.python.org/3/library/unittest.html) & [`pytest`](https://pytest.org) cho **Python**
- [`PHPUnit`](https://phpunit.de) & [`Codeception`](https://codeception.com), Storyplayer, SeleniumHQ, Behat, Atoum, SimpleTest
, PhpSpec, Peridot, Kahlan cho **PHP**
- [`Mocha`](https://mochajs.org), [`Jasmine`](https://jasmine.github.io) hoặc [`Chai`](https://www.chaijs.com) cho **JavaScripts**
- [`Jest`](https://github.com/facebook/jest), [`Mocha`](https://github.com/mochajs/mocha), [`Chai`](https://github.com/chaijs/chai), [`Karma`](https://github.com/karma-runner/karma), [`Jasmine`](https://github.com/jasmine/jasmine), [`Enzyme`](https://github.com/enzymejs/enzyme), [`React-testing-library`](https://github.com/testing-library/react-testing-library), [`React test utils and test renderer`](https://reactjs.org/docs/test-utils.html), [`Cypress IO`](https://github.com/cypress-io/cypress), [`Pupeeter`](https://github.com/puppeteer/puppeteer), [`Bit`](https://bit.dev) cho **React**


-----
Tham khảo:

- [Các Tester liên quan như thế nào trong các kỹ thuật TDD, BDD & ATDD](https://viblo.asia/p/cac-tester-lien-quan-nhu-the-nao-trong-cac-ky-thuat-tdd-bdd-atdd-m68Z0V8X5kG)
- [The Evolution of the Testing Pyramid](https://www.james-willett.com/the-evolution-of-the-testing-pyramid/)
- [Test Pyramid In Practice](https://www.pgs-soft.com/blog/test-pyramid-in-practice/)
- [Restructuring Frontend Testing Pyramid: alternative to Unit/Integration/E2E approach](https://dev.to/hiroyone/frontend-testing-no-more-unitintegratione2e-categorizations-and-priorities-5358)
- [The Testing Pyramid](https://www.devopsgroup.com/insights/resources/diagrams/all/the-testing-pyramid/)
- [The Agile Testing Pyramid](https://www.agilecoachjournal.com/2014-01-28/the-agile-testing-pyramid)
- [System tests: an objective look at the product](https://blog.atinternet.com/en/system-tests-an-objective-look-at-the-product/)
- [Total Test Best Practices](https://devops.api.bmc.com/guidelines/ttt/ttt_best_practices.html)
- [Test Automation Pyramid: 2021 Version](https://medium.com/software-qe/test-automation-pyramid-2021-version-c299cb224c80)
- [Test Approach](https://www.you-getapptester.com/home/features-benefits/test-approach/)
- [Unit Testing Tutorial – What is, Types & Test Example](https://www.guru99.com/unit-testing-guide.html)

-----
- [Tổng quan về unit test với ASP.NET Core, xUnit và Moq](https://comdy.vn/unit-test/tong-quan-ve-unit-test-voi-asp-net-core-xunit-va-moq/)
- [Viết unit test sử dụng xUnit](https://www.dotnetcoban.com/2019/07/unit-test-in-csharp-using-xunit.html)
- [Unit Test with .Net 6 with xUnit and MOQ](https://dev.to/moe23/learn-unit-test-with-net-6-with-xunit-and-moq-k9i)
- [Unit Testing ứng dụng C# dùng .NET Core và Visual Studio Code](https://techmaster.vn/posts/34532/unit-testing-csharp-net-core-visual-studio-code)
- [Viết unit test sử dụng xUnit](https://www.dotnetcoban.com/2019/07/unit-test-in-csharp-using-xunit.html)
- [[TUTORIAL] VIẾT UNIT TEST TRONG C# VỚI NUNIT](https://toidicodedao.com/2015/08/25/tutorial-viet-unit-test-trong-c-voi-nunit/)
- [Nhập môn Unit Testing trong .NET](https://ngocminhtran.com/2019/09/06/nhap-mon-unit-testing-trong-net/)
- [How To Create Selenium Test using NUnit Framework](https://learn-automation.com/selenium-test-using-nunit-framework/)
- [Tìm hiểu về IOT testing](https://viblo.asia/p/tim-hieu-ve-iot-testing-gDVK29Bw5Lj)
- [Tạo và chạy unit test trong Visual studio](https://viblo.asia/p/tao-va-chay-unit-test-trong-visual-studio-wpVYRPNzG4ng)
- [5 cách để mock DateTime.Now cho Unit Test trong C#](https://viblo.asia/p/5-cach-de-mock-datetimenow-cho-unit-test-trong-c-vyDZOnV7Kwj)
- [Most Complete MSTest Unit Testing Framework Cheat Sheet](https://www.automatetheplanet.com/mstest-cheat-sheet/)
- [Unit testing framework](https://www.slideshare.net/igorvavrish/unit-testing-framework)
- [ASP.NET MVC Tip #20 – Sử dụng Unit Test Data Access](https://viblo.asia/p/aspnet-mvc-tip-20-su-dung-unit-test-data-access-OeVKBxOdlkW)
- [Cache trang web ASP.NET](https://viblo.asia/p/cache-trang-web-aspnet-7prv3Pb9RKod)
- [Làm quen với Unit Testing, các tool và framework phụ trợ](https://viblo.asia/p/lam-quen-voi-unit-testing-cac-tool-va-framework-phu-tro-Zzb7vD1kRjKd)
- [ASP.NET MVC Tip #2 - Tạo custom Action Result trả về Microsoft Excel Documents](https://viblo.asia/p/aspnet-mvc-tip-2-tao-custom-action-result-tra-ve-microsoft-excel-documents-ORNZq31L50n)
- [ASP.NET MVC Tip #3 – Provide Explicit View Names khi Unit Testing](https://viblo.asia/p/aspnet-mvc-tip-3-provide-explicit-view-names-khi-unit-testing-m68Z0mWQlkG)
- [ASP.NET MVC Tip #13 – Unit Test Custom Routes](https://viblo.asia/p/aspnet-mvc-tip-13-unit-test-custom-routes-vyDZOzvdKwj)
- [ASP.NET MVC Tip #20 – Sử dụng Unit Test Data Access](https://viblo.asia/p/aspnet-mvc-tip-20-su-dung-unit-test-data-access-OeVKBxOdlkW)
- [ASP.NET MVC Tip #25 – Unit Test Views không cần Web Server (p1)](https://viblo.asia/p/aspnet-mvc-tip-25-unit-test-views-khong-can-web-server-p1-4P8563RGKY3)
- [ASP.NET MVC Tip #25 – Unit Test Views không cần Web Server (p2)](https://viblo.asia/p/aspnet-mvc-tip-25-unit-test-views-khong-can-web-server-p2-WAyK8Q6WZxX)
- [ASP.NET MVC Tip #28 – Test Nếu Caching được kích hoạt](https://viblo.asia/p/aspnet-mvc-tip-28-test-neu-caching-duoc-kich-hoat-gDVK2GnjZLj)
- [ASP.NET MVC Tip #33 – Unit Test LINQ to SQL (p1)](https://viblo.asia/p/aspnet-mvc-tip-33-unit-test-linq-to-sql-p1-LzD5dMzYKjY)
- [Điều khiển thời gian trong unit test C#](https://duongnt.com/time-dependent-unit-testing-vie/)
- [Cách viết các loại Unit Tests trong ASP.NET Core Web API có ví dụ](https://minhphien.com/cach-viet-cac-loai-unit-tests-trong-asp-net-core-web-api-co-vi-du/)
- [Unit Testing Web API dùng .NET Core](https://vtitech.vn/unit-testing-web-api-dung-net-core/)
- [How to unit test private methods in .NET Core applications (C#)](https://www.tannv.dev/2020/10/how-to-unit-test-private-methods-in-net-core-c-csharp.html)
- [Professional Test Driven Development with C#: Developing Real World Applications with TDD](https://www.amazon.com/Professional-Test-Driven-Development-Applications-ebook/dp/B004X75OGG/)
- [C# and .NET Core Test-Driven Development: Dive into TDD to create flexible, maintainable, and production-ready .NET Core applications](https://www.amazon.com/NET-Core-Test-Driven-Development-production-ready-ebook/dp/B0772S8R7Q/)
- [C# and .NET Core Test-Driven Development: Dive into TDD to create flexible, maintainable, and production-ready .NET Core applications](https://github.com/PacktPublishing/CSharp-and-.NET-Core-Test-Driven-Development)
- [Practical Test-Driven Development using C# 7: Unleash the power of TDD by implementing real world examples under .NET environment and JavaScript](https://www.amazon.com/Practical-Test-Driven-Development-using-implementing-ebook/dp/B078K959HT/)

-----
- [QUAN ĐIỂM TEST ĐỐI VỚI CHỨC NĂNG IMPORT/UPLOAD CSV](https://co-well.vn/nhat-ky-cong-nghe/quan-diem-test-doi-voi-chuc-nang-import-upload-csv-p1/)
- [UNIT TESTING TUTORIAL: VIẾT MỘT KIỂM THỬ CÓ ÍCH VÀ @dataprovider](https://co-well.vn/nhat-ky-cong-nghe/unit-testing-tutorial-viet-mot-kiem-thu-co-ich-va-dataprovider/)
- [UNIT TESTING TUTORIAL: PRIVATE/PROTECTED METHODS, COVERAGE REPORTS VÀ C.R.A.P](https://co-well.vn/nhat-ky-cong-nghe/unit-testing-tutorial-private-protected-methods-coverage-reports-va-crap/)
- [Đọc file csv bằng JUnit5](https://giangtester.com/doc-file-csv-bang-junit5/)
- [Test Automation IDE - JetBrains Aqua](https://anhtester.com/blog/test-automation-ide-jetbrains-aqua-b496.html)

-----
- [Telegram Automation Testing](https://t.me/+kSUGJ3pVvxkyZWU1)
- [Telegram Manual Testing](https://t.me/+8eChRz7OVqliZWRl)
- [Testing Strategies For Microservices](https://semaphoreci.com/blog/test-microservices)
- [The 5 Main Strategies for Testing a Microservices App](https://www.teaminternational.com/5-main-strategies-testing-microservices-app/)
- [Microservices Testing Strategies, Types & Tools: A Complete Guide](https://www.simform.com/blog/microservice-testing-strategies/)
- [Testing a Spring Boot Microservices: Tools and Techniques](https://medium.com/kth-distributed-systems/testing-microservices-in-spring-boot-applications-tools-and-techniques-b9c27d865f88)
- [Acceptance test with gauge and spring boot](https://mesutyakut.medium.com/acceptance-test-with-gauge-and-spring-boot-f675655d8e)
- [Tìm hiểu mô hình IoC](https://dotnetguru.org/tim-hieu-mo-hinh-ioc/)