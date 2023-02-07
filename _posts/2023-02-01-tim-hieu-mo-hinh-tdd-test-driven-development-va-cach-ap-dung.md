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


## I. Unit testing C#

![Unit Testing](https://boxxv.github.io/img/test/sketch.png "Unit Testing")


### Unit Test trong C# với NUnit

Trước đây, để viết Unit Test trong C#, ta thường phải tạo một project test riêng, sử dụng thư viện MSTest của Microsoft. MSTest hỗ trợ khá nhiều chức năng: Test dữ liệu từ database, đo performance hệ thống, xuất dữ liệu report. Tuy nhiên, do MSTest đi kèm với Visual Studio, không thể chạy riêng rẽ, lại khá nặng nề, do đó NUnit được nhiều người ưa thích hơn. NUnit có 1 bộ runner riêng, có thể chạy UnitTest độc lập không cần VisualStudio, ngoài ra nó cũng hỗ trợ một số tính năng mà MSTest không có (parameter test, Assert Throw).




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
- [Tìm hiểu về IOT testing](https://viblo.asia/p/tim-hieu-ve-iot-testing-gDVK29Bw5Lj)