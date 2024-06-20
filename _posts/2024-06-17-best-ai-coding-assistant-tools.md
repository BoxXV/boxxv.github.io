---
layout: post
title: Lựa chọn thay thế GitHub Copilot miễn phí cho VS Code
subtitle: Công cụ AI hỗ trợ lập trình
image: "img/2024/f915c918009ca0c2f98d.jpg"
tags:
- Mạt Code
- lập trình
---

Trong bài viết này, tôi đã biên soạn một danh sách về các lựa chọn thay thế GitHub Copilot miễn phí cho Visual Studio Code. Một số công cụ này thậm chí còn là nguồn mở.

![AI](https://boxxv.github.io/img/ai/54fae9f34711e44fbd00.jpg "AI")

## Bito

Không giống như GitHub Copilot, Bito hiểu codebase cục bộ của bạn bên trong VS Code bằng cách tận dụng sức mạnh của các phần nhúng và cơ sở dữ liệu vectơ. Nó cung cấp khả năng hoàn thành mã AI có liên quan cao khi bạn nhập hoặc thông qua nhận xét mã. Nó có một chatbot được hỗ trợ bởi AI, nơi bạn có thể đặt câu hỏi liên quan đến toàn bộ codebase của mình. Nó cũng duy trì lịch sử các cuộc hội thoại của bạn, từ đó tạo ra các câu trả lời nhận biết ngữ cảnh tốt hơn.

Ngoài ra, còn có [Bito CLI](https://bito.ai/product/cli-ai-chat/) có thể tự động hóa các tác vụ lặp đi lặp lại của bạn bằng AI. Một số công cụ tự động hóa AI thông minh được tạo bằng Bito CLI bao gồm Trình tạo tài liệu AI và Trình tạo trường hợp thử nghiệm AI.

Bito là ứng dụng AI được đánh giá cao nhất trên thị trường Visual Studio Code (với xếp hạng 4,9 trên 5). Nó có hơn 100.000 người dùng hoạt động hàng tháng nên có vẻ như nó được các nhà phát triển yêu thích.

Vì Bito đang sử dụng các mô hình phức tạp từ OpenAI (GPT-4, GPT-3.5 Turbo) và Anthropic (Claude 2, Claude Instant) nên nó rất linh hoạt. Bạn có thể yêu cầu nó tạo mã, cải thiện hiệu suất mã, giải thích một khái niệm, v.v.

Dưới đây là một số [ví dụ sử dụng khác của Bito](https://docs.bito.ai/getting-started/bito-ai-examples).

> [Install](https://marketplace.visualstudio.com/items?itemName=Bito.Bito)

## Tabnine

Hoạt động của Tabnine tương tự như Copilot. Tuy nhiên, một số ưu điểm của nó bao gồm các mô hình AI được cá nhân hóa, tự lưu trữ, truy cập ngoại tuyến và quyền riêng tư về mã.

Gói miễn phí của họ chỉ cung cấp tính năng hoàn thành mã cơ bản. Nó gợi ý từng dòng mã.

Để nhận được đề xuất tốt hơn từ Tabnine, bạn phải cung cấp cho tabnine một số ngữ cảnh bằng lời nhắc bằng ngôn ngữ tự nhiên và mã của riêng bạn.

## Amazon CodeWhisperer

Amazon CodeWhisperer đề xuất toàn bộ chức năng và đoạn mã (tối đa 10–15 dòng mã) trong thời gian thực.

Nó được tối ưu hóa để sử dụng với các API AWS như Amazon EC2, AWS Lambda và Amazon S3.

Amazon CodeWhisperer cũng có thể quét mã nguồn của bạn để phát hiện các lỗ hổng bảo mật. Nó tuân theo các phương pháp thực hành tốt nhất được nêu ra bởi Dự án bảo mật ứng dụng toàn cầu mở (OWASP).

## Codeium

Codeium là người bạn đồng hành mã hóa AI được hỗ trợ bởi các mô hình và cơ sở hạ tầng AI tổng hợp nội bộ. Các mô hình AI được đào tạo bằng hơn 70 ngôn ngữ lập trình phổ biến.

Nó cung cấp tính năng tự động hoàn thành mã, tìm kiếm thông minh (tìm tệp và mã trong thư mục dự án bằng lời nhắc ngôn ngữ tự nhiên) và Trò chuyện được hỗ trợ bởi AI.

Họ cũng có một sân chơi trực tuyến để kiểm tra chức năng của Codeium mà không cần đăng ký.

## Cody

Cody là một trợ lý mã hóa AI nguồn mở được tạo bởi Sourcegraph. Nó sử dụng Mô hình ngôn ngữ lớn với API đồ thị mã của Sourcegraph để cung cấp hỗ trợ mã hóa.

Chatbot của nó có thể trả lời các câu hỏi kỹ thuật của bạn ngay trong Mã VS. Cody cũng cung cấp tính năng tự động hoàn thành khi bạn nhập mã vào trình chỉnh sửa.

Cody có thể dễ dàng hiểu được các cơ sở mã phức tạp. Cho phép bạn đặt câu hỏi liên quan đến mã của bạn.

## FauxPilot

FauxPilot là một giải pháp mã nguồn mở thay thế cho GitHub Copilot. Bạn có thể lưu trữ nó trên máy chủ của mình hoặc sử dụng nó ngoại tuyến trên máy tính.

Không giống như GitHub Copilot sử dụng OpenAI Codex, FauxPilot được hỗ trợ bởi các mô hình SalesForce CodeGen có tính cạnh tranh rất cao với OpenAI Codex.

Theo mặc định, FauxPilot không cung cấp tiện ích mở rộng cho Mã VS. Tuy nhiên, một nhà phát triển khác đã tạo [tiện ích mở rộng FauxPilot cho VS Code](https://github.com/Venthe/vscode-fauxpilot) và cũng biến nó thành nguồn mở.

Tôi chỉ khuyên bạn nên sử dụng tính năng này nếu bạn cảm thấy thoải mái khi làm việc với Docker vì các bước cài đặt của FauxPilot có thể hơi phức tạp.

Nếu bạn đang dùng Windows, hãy sử dụng [kho lưu trữ này](https://github.com/Frederisk/fauxpilot-windows) để cài đặt FauxPilot.

## Tabby

Tabby là một trợ lý mã hóa AI tự lưu trữ mã nguồn mở. Nó có thể đề xuất toàn bộ chức năng hoặc đoạn mã nhiều dòng khi bạn nhập. Nó lấy bối cảnh từ mã và nhận xét của bạn.

Điều tốt nhất về Tabby là nó có thể được tinh chỉnh cho bất kỳ dự án nào. Để huấn luyện Tabby, bạn cần một PC có bộ tăng tốc GPU tốt (ví dụ RTX 3080). Quá trình đào tạo có thể được cấu hình bằng tệp YAML.

Bạn cũng có thể dùng thử Tabby trong trình duyệt mà không cần đăng ký.

## CodeGeeX

CodeGeeX là mô hình tạo mã nguồn mở được đào tạo bằng hơn 20 ngôn ngữ lập trình (ví dụ: Python, JavaScript, Java, C++/C, Go, v.v.). Nó sử dụng 13 tỷ thông số và tạo ra kết quả chất lượng rất cao.

Nó có thể được sử dụng để gợi ý mã, dịch thuật, giải thích và tóm tắt.

Bạn cũng có thể [đọc tài liệu nghiên cứu CodeGeeX](https://arxiv.org/abs/2303.17568) để biết thêm thông tin kỹ thuật.

## AskCodi

AskCodi là một giải pháp thay thế miễn phí cho GitHub Copilot dành cho Mã VS. Nó sử dụng OpenAI Codex để thực hiện nhiều nhiệm vụ của trợ lý mã AI.

Ví dụ: nó có thể được sử dụng để đề xuất mã, tài liệu phần mềm, giải thích mã, kiểm tra, v.v. Bạn cũng có thể sử dụng tính năng trò chuyện của nó để bắt đầu cuộc trò chuyện với lập trình viên cặp AI của mình.

AskCodi ưu tiên quyền riêng tư của mã. Nó không lưu mã bạn truyền vào nó hoặc mã mà nó tạo ra.

## Blackbox AI

Blackbox AI được tích hợp nhiều tính năng như tự động hoàn thành mã, tìm kiếm mã và tìm kiếm kho lưu trữ. Nó được tạo ra để tăng tốc độ phát triển phần mềm bằng cách tăng năng suất của các nhà phát triển.

Tính năng tự động hoàn thành mã cung cấp các đề xuất bằng hơn 20 ngôn ngữ lập trình dựa trên thông tin đầu vào của nhà phát triển. Tìm kiếm kho lưu trữ cho phép các nhà phát triển tìm kiếm trực tiếp qua hàng triệu tệp kho lưu trữ mã nguồn mở trong môi trường phát triển tích hợp (IDE) của họ. Tính năng tìm kiếm mã giúp nhà phát triển tìm đoạn mã cho dự án của họ bằng cách nhập câu hỏi hoặc truy vấn.

Những tính năng này cũng có sẵn trong Jupyter Lab và Jupyter Notebooks.

## Kết luận

Có nhiều lựa chọn thay thế miễn phí cho GitHub Copilot có thể được tích hợp với Visual Studio Code. Mỗi lựa chọn thay thế này đều cung cấp các tính năng và khả năng riêng biệt, đáp ứng các nhu cầu và sở thích mã hóa khác nhau. Cho dù bạn muốn có trợ lý mã hóa giống như chatbot, mô hình AI được cá nhân hóa, quyền truy cập ngoại tuyến, quyền riêng tư của mã hay hỗ trợ chuyên biệt cho API AWS, thì vẫn có một giải pháp thay thế phù hợp với yêu cầu của bạn.

Bây giờ là lúc thử nghiệm các trợ lý mã hóa AI khác nhau trong trình soạn thảo Visual Studio Code của bạn, tìm ra trợ lý phù hợp nhất với phong cách và quy trình mã hóa của bạn. Tận dụng sức mạnh của AI trong hành trình mã hóa của bạn và đưa quá trình phát triển của bạn lên một tầm cao mới.

-----
- [10 Free GitHub Copilot Alternatives for VS Code 2024](https://bito.ai/blog/free-github-copilot-alternatives-for-vs-code/)
- [10 Best AI Coding Assistant Tools in 2024– Guide for Developers](https://www.thedroidsonroids.com/blog/best-ai-coding-assistant-tools)
- [Testing LLMs on Solving Leetcode Problems](https://hackernoon.com/testing-llms-on-solving-leetcode-problems)
- [My opinion after testing some AI code assistant](https://www.jujens.eu/posts/en/2023/Aug/21/ai-tests/)
- [Bito](https://bito.ai) - [Become a 10X Dev with Bito](https://marketplace.visualstudio.com/items?itemName=Bito.Bito)
- [Codeium](https://codeium.com) - [Free AI Code Completion &amp; Chat](https://marketplace.visualstudio.com/items?itemName=Codeium.codeium)
- [Cody](https://sourcegraph.com/cody) - [AI coding assistant](https://github.com/sourcegraph/cody)
- [Tabnine](https://www.tabnine.com) - The AI code assistant that you control
- Amazon CodeWhisperer
- FauxPilot
- Tabby
- CodeGeeX
- AskCodi
- Blackbox AI
- Replit AI
- Cursor
- SQLAI
- Snyk powered by DeepCode AI