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

![Unit Testing](https://boxxv.github.io/img/test/sketch.png "Unit Testing")


## I. Unit testing C#

![Unit Testing](https://boxxv.github.io/img/test/01_24.06.jpg "Unit Testing")

### Tại sao bắt đầu viết unit test lại khó đến vậy?

Cách đây khoảng 6 năm, tôi muốn viết unit test để tự động hóa việc kiểm thử ứng dụng mà tôi đang tham gia xây dựng. Đó là những gì một nhà phát triển giỏi làm và tôi mong muốn trở thành một nhà phát triển giỏi.

Nhưng bằng cách nào?

Ứng dụng mà tôi tham gia xây dựng không có bất kỳ bài kiểm tra unit test nào để tự động hóa việc kiểm thử. Chúng tôi phải kiểm tra các chức năng hoàn toàn bằng cơm, đây là một công việc lặp đi lặp lại rất nhàm chán và bỏ sót nhiều bug (QC rất thích điều này, còn tôi thì không).

Tôi muốn thay đổi điều này và đã tìm thấy giải pháp là sử dụng unit test sau khi lang thang trên Google. Tôi đã thử làm theo ví dụ trong các hướng dẫn này và các ví dụ này chạy ngon lành. Tôi nghĩ rằng mình đã tìm thấy kim chỉ nam và suýt nữa đã làm như Acsimet đã từng làm cách đây hơn 2000 năm.

Tuy nhiên khi tôi muốn viết unit test cho dự án thực tế của tôi thì không áp dụng được. Các ví dụ mà tôi làm theo thường rất đơn giản, chẳng hạn như một chương trình cho phép cộng, trừ, nhân, chia hai số nguyên.

Trong khi ứng dụng mà tôi muốn viết unit test khá phức tạp: có giao diện Frontend và Backend, có các API xử lý business ở đằng sau và hầu hết thực hiện các thao tác CRUD (Create, Read, Update, Delete) với cơ sở dữ liệu.

Vấn đề ở đây là tôi cần viết unit test cho cái gì? Vì ứng dụng có rất nhiều thành phần khác nhau, từ UI đến API, business logic tới repository, database, ...

Một vấn đề khác là mọi người luôn nói, "các bài kiểm tra unit test là quan trọng. Bạn phải làm chúng!" và sau đó không bao giờ nói cho tôi biết _làm thế nào_  để viết chúng và làm thế nào để viết chúng thật tốt.

Loạt bài này trình bày một số thứ tôi đã học được và sử dụng trong công việc của tôi. Tôi đã học được rất nhiều về kiểm thử và đặc biệt là kiểm thử đơn vị tự động, và tôi hy vọng rằng một số điều tôi học được sẽ hữu ích cho độc giả của tôi.

> [Bảng Cheat-Sheet tham khảo cho Unit Test dễ dàng hơn](https://viblo.asia/p/bang-cheat-sheet-tham-khao-cho-unit-test-de-dang-hon-aWj53vR8l6m)

### Unit Test trong C# với MSTest


### Unit Test trong C# với NUnit

Trước đây, để viết Unit Test trong C#, ta thường phải tạo một project test riêng, sử dụng thư viện MSTest của Microsoft. MSTest hỗ trợ khá nhiều chức năng: Test dữ liệu từ database, đo performance hệ thống, xuất dữ liệu report. Tuy nhiên, do MSTest đi kèm với Visual Studio, không thể chạy riêng rẽ, lại khá nặng nề, do đó NUnit được nhiều người ưa thích hơn. NUnit có 1 bộ runner riêng, có thể chạy UnitTest độc lập không cần VisualStudio, ngoài ra nó cũng hỗ trợ một số tính năng mà MSTest không có (parameter test, Assert Throw).

### Unit Test trong C# với [xUnit](xunit.net)

![Unit Testing](https://boxxv.github.io/img/test/unit-testing-framework-17-2048.webp "Unit Testing")


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
- [Testing Strategies For Microservices](https://semaphoreci.com/blog/test-microservices)
- [The 5 Main Strategies for Testing a Microservices App](https://www.teaminternational.com/5-main-strategies-testing-microservices-app/)
- [Microservices Testing Strategies, Types & Tools: A Complete Guide](https://www.simform.com/blog/microservice-testing-strategies/)
- [Testing a Spring Boot Microservices: Tools and Techniques](https://medium.com/kth-distributed-systems/testing-microservices-in-spring-boot-applications-tools-and-techniques-b9c27d865f88)
- [Acceptance test with gauge and spring boot](https://mesutyakut.medium.com/acceptance-test-with-gauge-and-spring-boot-f675655d8e)
- [Unit Testing Tutorial – What is, Types & Test Example](https://www.guru99.com/unit-testing-guide.html)
- [[TUTORIAL] VIẾT UNIT TEST TRONG C# VỚI NUNIT](https://toidicodedao.com/2015/08/25/tutorial-viet-unit-test-trong-c-voi-nunit/)
- [How To Create Selenium Test using NUnit Framework](https://learn-automation.com/selenium-test-using-nunit-framework/)
- [Tìm hiểu về IOT testing](https://viblo.asia/p/tim-hieu-ve-iot-testing-gDVK29Bw5Lj)
- [Tạo và chạy unit test trong Visual studio](https://viblo.asia/p/tao-va-chay-unit-test-trong-visual-studio-wpVYRPNzG4ng)
- [Cách viết Unit Test trong C#](http://duyanhpham.com/phan-1-cach-viet-unit-test-trong-c-sharp/)
- [Unit Testing ứng dụng C# dùng .NET Core và Visual Studio Code](https://techmaster.vn/posts/34532/unit-testing-csharp-net-core-visual-studio-code)
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