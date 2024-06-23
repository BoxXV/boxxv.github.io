---
layout: post
title: Lựa chọn thay thế GitHub Copilot miễn phí cho VS Code
subtitle: Công cụ AI hỗ trợ lập trình
image: "img/2024/f915c918009ca0c2f98d.jpg"
tags:
- Mạt Code
- lập trình
---

## Mục lục

- [Mục lục](#mục-lục)
- [🎯Feature Guides](#feature-guides)
	- [Codeium](#codeium)
	- [Cody](#cody)
	- [Bito](#bito)
- [So sánh](#so-sánh)
	- [1. GitHub Copilot](#1-github-copilot)
	- [2. Bito](#2-bito)
	- [3. Tabnine](#3-tabnine)
	- [4. Amazon CodeWhisperer](#4-amazon-codewhisperer)
	- [5. Codiumate](#5-codiumate)
	- [6. Codeium](#6-codeium)
	- [7. Cody](#7-cody)
	- [8. FauxPilot](#8-fauxpilot)
	- [9. Tabby](#9-tabby)
	- [10. CodeGeeX](#10-codegeex)
	- [11. AskCodi](#11-askcodi)
	- [12. Blackbox AI](#12-blackbox-ai)
	- [13. Replit AI](#13-replit-ai)
	- [14. Cursor](#14-cursor)
	- [15. SQLAI](#15-sqlai)
	- [16. Snyk powered by DeepCode AI](#16-snyk-powered-by-deepcode-ai)
	- [17. Gemini in Android Studio](#17-gemini-in-android-studio)
- [Testing LLMs on Solving Leetcode Problems](#testing-llms-on-solving-leetcode-problems)
	- [Datasets](#datasets)
	- [Prompts and code generation](#prompts-and-code-generation)
	- [Results](#results)
	- [Future considerations](#future-considerations)
- [Kết luận](#kết-luận)


Trong bài viết này, tôi đã biên soạn một danh sách về các lựa chọn thay thế GitHub Copilot miễn phí cho Visual Studio Code. Một số công cụ này thậm chí còn là nguồn mở.

![AI](https://boxxv.github.io/img/ai/7e04cd1f179bb4c5ed8a.jpg "AI")

## 🎯Feature Guides

### Codeium

![Codeium](https://boxxv.github.io/img/ai/Codeium Context Menus.jpg "Codeium")

**Function:**
- Refactor Selected Code Block
- Explain Slected Code Block

- Add `comments` and `docstrings` to the code
- Add `logging` statements so that it can be easily debugged
- `Clean` up this code
- `Check` for bugs and null pointers
- `Implement` the code for the `TODO comment`
- Generate `unit tests`
- Make this code strongly typed
- Make this faster and more efficient
- Verbosely comment this code so that I can understand what's going on

![Codeium](https://boxxv.github.io/img/ai/Codeium Context Menus.png "Codeium")

**Feature:**
- Rapid code autocomplete
- In-editor AI chat assistant
- `Unlimited usage`
- Trained on permissive data
- Support via Discord
- Encryption in transit
- Supports 21+ Programming Languages: Visual Studio Code, JetBrain IDEs, Vim/Neovim, `Visual Studio`, Emacs, Chrome Extension, Jupyter Notebooks, Google Colab, Deepnote, Databricks, `Xcode`, `Sublime Text`, `Eclipse`, IntelliJ, PyCharm, WebStorm, GoLand, PhpStorm, CLion, `Android Studio`
- Supports 70+ Programming Languages (JS, Go, C++, SQL, etc)
- Coding: Viết mã lập trình
- Multilingual: Xử lý ngôn ngữ đa ngữ
- Creative writing: N/A
- Unit Test: `Xunit` for C#

### Cody

![Cody](https://boxxv.github.io/img/ai/Cody Context Menus.jpg "Cody")

**Function:**
- Edit Code
- New Chat
- Document Code
- Explain Code
- Find Code Smells
- Generate Unit Tests
- Custom Commands

![Cody](https://boxxv.github.io/img/ai/Cody Context Menus.png "Cody")

**Feature:**
- AI models: Free for `Claude 3 Sonnet`
- `500 Autocompletions` per month
- `20 Messages and commands` per month
- Coding: Viết mã lập trình
- Multilingual: Xử lý ngôn ngữ đa ngữ
- Creative writing: Viết sáng tạo
- Unit Test: `MSTest` for C#

### Bito

![Bito](https://boxxv.github.io/img/ai/Bito Context Menus.jpg "Bito")

**Function:**
- Insert code into Bito
- `Explain` this Code
- Generate `Comment`
- `Performance` Check
- `Security` Check
- `Style` Check
- Improve Readablity
- `Clean` Code
- Generate `Unit Test`
- Run Custom Prompt Template

![Bito](https://boxxv.github.io/img/ai/Bito Context Menus.png "Bito")

**Feature:**
- AI models: GPT 3.5, Chat-bison from Google and other similar models
- Limited usage on chat and CLI: `20 AI requests per day`, One-click pre-defined and custom templates
- AI code completions: `100 per month`
- Max context length: `40,000 characters`
- Intelligent AI automation agents: Documentation, tests, etc
- Supports 4+ Programming Languages: Visual Studio Code, JetBrain IDEs, Chrome Extension, Vim/Neovim Plugin
- Supports 50+ Programming Languages (JS, Go, C++, SQL, etc)
- Supports 25 spoken languages (English, French, Chinese, etc)
- Coding: Viết mã lập trình
- Multilingual: Xử lý ngôn ngữ đa ngữ
- Creative writing: Viết sáng tạo
- Unit Test: `NUnit` for C#

## So sánh

![AI](https://boxxv.github.io/img/ai/54fae9f34711e44fbd00.jpg "AI")

### 1. GitHub Copilot

GitHub Copilot là một công cụ hoàn thiện mã được ra đời từ sự hợp tác giữa GitHub, OpenAI và Microsoft. Nó sử dụng AI tiên tiến để cung cấp hỗ trợ mã hóa, hiểu bối cảnh bạn đang viết mã. Được đào tạo về rất nhiều mã từ các dự án nguồn mở trên GitHub, Copilot nâng cao quá trình phát triển bằng cách cung cấp các giải thích và hoàn thành mã thông minh trực tiếp trong IDE.

Theo nghiên cứu , các nhà phát triển sử dụng Copilot nhận thấy mức độ hài lòng trong công việc tăng lên đáng kể - được báo cáo là cao hơn 75%. Họ cũng báo cáo mã hóa nhanh hơn tới 55%. Mặc dù điều này làm tăng năng suất của họ nhưng nó không ảnh hưởng đến chất lượng mã. Nó tương thích với các trình soạn thảo chính như Visual Studio Code , JetBrains IDE và Neovim . Hơn nữa, nó được tích hợp độc đáo vào hệ sinh thái của GitHub. Copilot đang nhanh chóng trở thành công cụ hoàn thiện mã AI được hàng triệu người dùng và doanh nghiệp sử dụng.

Mặc dù nó hỗ trợ hầu hết các ngôn ngữ lập trình có trong kho công cộng nhưng chất lượng đề xuất của nó lại khác nhau. Các ngôn ngữ như JavaScript nhận được sự hỗ trợ mạnh mẽ hơn do tính phổ biến của chúng trong dữ liệu đào tạo. Copilot có thể truy cập được thông qua nhiều tiện ích mở rộng IDE, GitHub CLI và sẽ sớm được tích hợp trực tiếp vào nền tảng web và di động của GitHub.

Các tính năng chính:
- Mức độ phổ biến cao và cộng đồng lớn.
- Tích hợp với nhiều IDE (Visual Studio Code, sản phẩm IntelliJ, Neovim).
- Hoàn thành mã thông minh và điều hướng dễ dàng thông qua nhiều đoạn mã.
- Hỗ trợ nhiều ngôn ngữ lập trình.
- Tham chiếu mã , tìm mã công khai phù hợp với đề xuất của trình tạo mã AI. Hiện đang ở phiên bản beta công khai và hiện chỉ có sẵn trong Visual Studio Code.
- Có thể chặn các đề xuất mã phù hợp với đoạn mã công khai. Điều này rất quan trọng để tránh vô tình vi phạm giấy phép nguồn mở.


### 2. [Bito](https://bito.ai)

Không giống như GitHub Copilot, Bito hiểu codebase cục bộ của bạn bên trong VS Code bằng cách tận dụng sức mạnh của các phần nhúng và cơ sở dữ liệu vectơ. Nó cung cấp khả năng hoàn thành mã AI có liên quan cao khi bạn nhập hoặc thông qua nhận xét mã. Nó có một chatbot được hỗ trợ bởi AI, nơi bạn có thể đặt câu hỏi liên quan đến toàn bộ codebase của mình. Nó cũng duy trì lịch sử các cuộc hội thoại của bạn, từ đó tạo ra các câu trả lời nhận biết ngữ cảnh tốt hơn.

Ngoài ra, còn có [Bito CLI](https://bito.ai/product/cli-ai-chat/) có thể tự động hóa các tác vụ lặp đi lặp lại của bạn bằng AI. Một số công cụ tự động hóa AI thông minh được tạo bằng Bito CLI bao gồm Trình tạo tài liệu AI và Trình tạo trường hợp thử nghiệm AI.

Bito là ứng dụng AI được đánh giá cao nhất trên thị trường Visual Studio Code (với xếp hạng 4,9 trên 5). Nó có hơn 100.000 người dùng hoạt động hàng tháng nên có vẻ như nó được các nhà phát triển yêu thích.

Vì Bito đang sử dụng các mô hình phức tạp từ OpenAI (GPT-4, GPT-3.5 Turbo) và Anthropic (Claude 2, Claude Instant) nên nó rất linh hoạt. Bạn có thể yêu cầu nó tạo mã, cải thiện hiệu suất mã, giải thích một khái niệm, v.v.

Dưới đây là một số [ví dụ sử dụng khác của Bito](https://docs.bito.ai/getting-started/bito-ai-examples).

> [Install](https://marketplace.visualstudio.com/items?itemName=Bito.Bito)

### 3. [Tabnine](https://www.tabnine.com)

Tabnine là một trợ lý mã hóa AI đáng tin cậy được thiết kế tập trung vào quyền riêng tư và bảo mật. Nó được đào tạo về một loạt mã hiện có bằng cách sử dụng các giấy phép nguồn mở dễ dãi, giảm thiểu mọi lo ngại về quyền riêng tư, bảo mật và tuân thủ. May mắn thay, điều này cũng bao gồm các vấn đề về copyleft. Việc tuân thủ các phương pháp hay nhất này được củng cố hơn nữa nhờ việc tuân thủ SOC-2. Tabnine cung cấp khả năng phản ánh kiến ​​thức chung của tổ chức. Nó điều chỉnh hỗ trợ cho cơ sở mã cụ thể của bạn, phù hợp với phong cách mã hóa và các phương pháp hay nhất của nhóm bạn mà không làm lộ mã nhạy cảm.

Tabnine hoạt động ở chế độ cách ly hoàn toàn. Nó chạy trong môi trường bạn đã chọn – có thể là thiết lập SaaS bảo mật, tại chỗ hoặc trên VPC của bạn. Điều này đảm bảo rằng tài sản trí tuệ của bạn luôn nằm trong tầm kiểm soát của bạn. Tabnine chỉ học từ mã của bạn nếu bạn chọn kết nối cơ sở mã của mình. Thậm chí sau đó, mã của bạn sẽ không bao giờ rời khỏi môi trường của bạn, đảm bảo quyền riêng tư hoàn toàn. Đó là một sự lựa chọn tuyệt vời cho những người ưu tiên bảo mật.

Hơn nữa, Tabnine cho phép thực thi chính sách tập trung. Các tổ chức có thể chuẩn hóa cấu hình và cách sử dụng trợ lý AI giữa các nhóm. Cách tiếp cận tập trung này giúp đơn giản hóa việc quản lý và cung cấp cho các nhóm sự đảm bảo về khả năng kiểm soát quyền riêng tư và bảo mật hoàn toàn đối với các quy trình mã hóa của họ.

Hoạt động của Tabnine tương tự như Copilot. Tuy nhiên, một số ưu điểm của nó bao gồm các mô hình AI được cá nhân hóa, tự lưu trữ, truy cập ngoại tuyến và quyền riêng tư về mã.

Gói miễn phí của họ chỉ cung cấp tính năng hoàn thành mã cơ bản. Nó gợi ý từng dòng mã.

Để nhận được đề xuất tốt hơn từ Tabnine, bạn phải cung cấp cho tabnine một số ngữ cảnh bằng lời nhắc bằng ngôn ngữ tự nhiên và mã của riêng bạn.

Các tính năng chính:
- Mức độ riêng tư và bảo mật cao. Chỉ sử dụng đoạn mã từ các nguồn được phép.
- Có thể được triển khai tại chỗ và trên VPC.
- Tài liệu mã tự động.
- Tích hợp với nhiều IDE (Sản phẩm Neovim, IntelliJ, VS Code, Eclipse và Sublime).
- Coding: Viết mã lập trình
- Multilingual: Xử lý ngôn ngữ đa ngữ
- Creative writing: Viết sáng tạo
- Unit Test: `NUnit` for C#

> [Install](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode)

### 4. Amazon CodeWhisperer

Amazon CodeWhisperer là một công cụ tạo mã dựa trên máy học. Nó cung cấp các đề xuất mã hóa theo thời gian thực phù hợp với phong cách cá nhân và công việc hiện tại của bạn. Khi bạn nhập văn bản, CodeWhisperer sẽ đưa ra các đề xuất mã có liên quan. Chúng có thể bao gồm từ các đoạn mã đơn giản đến toàn bộ hàm, tùy thuộc vào ngữ cảnh của mã hiện tại và dữ liệu đầu vào trước đây của bạn. CodeWhisperer cũng có thể tạo nhận xét và tài liệu mã.

Tuy nhiên, tính năng nổi bật của nó là khả năng dự đoán và hoàn thành các khối mã hoặc chức năng khi bạn viết. Ngoài ra, bạn có thể ghép nối nó với các IDE như Visual Studio Code hoặc các sản phẩm JetBrains . CodeWhisperer hoạt động cùng với Amazon CodeGuru , nơi tiến hành quét bảo mật mã và các tệp liên quan của bạn, chủ động xác định các vấn đề bảo mật tiềm ẩn.

Amazon CodeWhisperer đề xuất toàn bộ chức năng và đoạn mã (tối đa 10–15 dòng mã) trong thời gian thực.

Nó được tối ưu hóa để sử dụng với các API AWS như Amazon EC2, AWS Lambda và Amazon S3.

Amazon CodeWhisperer cũng có thể quét mã nguồn của bạn để phát hiện các lỗ hổng bảo mật. Nó tuân theo các phương pháp thực hành tốt nhất được nêu ra bởi Dự án bảo mật ứng dụng toàn cầu mở (OWASP).

Các tính năng chính:
- Tích hợp với hệ sinh thái của Amazon.
- Đề xuất mã chính xác trong thời gian thực.
- Quét an ninh.

### 5. [Codiumate](https://www.codium.ai)


> [Install](https://marketplace.visualstudio.com/items?itemName=Codium.codium)

### 6. [Codeium](https://codeium.com)

Codeium là người bạn đồng hành mã hóa AI được hỗ trợ bởi các mô hình và cơ sở hạ tầng AI tổng hợp nội bộ. Các mô hình AI được đào tạo bằng hơn 70 ngôn ngữ lập trình phổ biến.

Nó cung cấp tính năng tự động hoàn thành mã, tìm kiếm thông minh (tìm tệp và mã trong thư mục dự án bằng lời nhắc ngôn ngữ tự nhiên) và Trò chuyện được hỗ trợ bởi AI.

Họ cũng có một sân chơi trực tuyến để kiểm tra chức năng của Codeium mà không cần đăng ký.

> [Install](https://marketplace.visualstudio.com/items?itemName=Codeium.codeium)

### 7. [Cody](https://sourcegraph.com/cody)

Cody là một trợ lý mã hóa AI được thiết kế để nâng cao tốc độ và khả năng hiểu biết về phát triển phần mềm. Với sự hiểu biết sâu sắc về cơ sở mã của bạn, nó cung cấp khả năng tự động hoàn thành tuyệt vời được hỗ trợ bởi AI. Đề xuất mã thông minh của nó không chỉ hoàn thiện các dòng mã mà còn toàn bộ chức năng. Tính năng này hoạt động trên nhiều ngôn ngữ, tệp cấu hình hoặc tài liệu.

Hơn nữa, nó còn có AI đàm thoại, trò chuyện Cody, được hỗ trợ bởi quá trình xử lý ngôn ngữ tự nhiên. Điều này phục vụ như một người bạn đồng hành tháo vát khi đi sâu vào các dự án xa lạ. Nó cũng giúp giải mã mã kế thừa và giải quyết các thách thức mã hóa phức tạp. Tuy nhiên, Cody vượt xa những gợi ý đơn thuần vì nó còn cho phép bạn tạo mã và viết bài kiểm tra. Nó có thể sửa mã nguồn bằng các lệnh bằng một cú nhấp chuột. Bạn có thể nhanh chóng tạo các bài kiểm tra đơn vị cũng như xác định và mô tả mùi mã để tối ưu hóa. Ngoài ra, thật dễ dàng để xác định các lệnh tùy chỉnh phù hợp với quy trình làm việc cụ thể của bạn. Cuối cùng, có sự tích hợp với Visual Studio Code, JetBrains IDE và Neovim.

Cody là một trợ lý mã hóa AI nguồn mở được tạo bởi Sourcegraph. Nó sử dụng Mô hình ngôn ngữ lớn với API đồ thị mã của Sourcegraph để cung cấp hỗ trợ mã hóa.

Chatbot của nó có thể trả lời các câu hỏi kỹ thuật của bạn ngay trong Mã VS. Cody cũng cung cấp tính năng tự động hoàn thành khi bạn nhập mã vào trình chỉnh sửa.

Cody có thể dễ dàng hiểu được các cơ sở mã phức tạp. Cho phép bạn đặt câu hỏi liên quan đến mã của bạn.

Các tính năng chính:
- Trò chuyện được hỗ trợ bởi AI để giải thích cấu trúc dự án và mục đích của từng tệp mã nguồn.
- Tạo mã dựa trên hướng dẫn.
- Hỗ trợ ngôn ngữ của con người bằng cách sử dụng xử lý ngôn ngữ tự nhiên.
- Free for [Claude 3 Sonnet](https://poe.com/Claude-3-Sonnet)

> [Install](https://marketplace.visualstudio.com/items?itemName=sourcegraph.cody-ai)

### 8. FauxPilot

FauxPilot là một giải pháp mã nguồn mở thay thế cho GitHub Copilot. Bạn có thể lưu trữ nó trên máy chủ của mình hoặc sử dụng nó ngoại tuyến trên máy tính.

Không giống như GitHub Copilot sử dụng OpenAI Codex, FauxPilot được hỗ trợ bởi các mô hình SalesForce CodeGen có tính cạnh tranh rất cao với OpenAI Codex.

Theo mặc định, FauxPilot không cung cấp tiện ích mở rộng cho Mã VS. Tuy nhiên, một nhà phát triển khác đã tạo [tiện ích mở rộng FauxPilot cho VS Code](https://github.com/Venthe/vscode-fauxpilot) và cũng biến nó thành nguồn mở.

Tôi chỉ khuyên bạn nên sử dụng tính năng này nếu bạn cảm thấy thoải mái khi làm việc với Docker vì các bước cài đặt của FauxPilot có thể hơi phức tạp.

Nếu bạn đang dùng Windows, hãy sử dụng [kho lưu trữ này](https://github.com/Frederisk/fauxpilot-windows) để cài đặt FauxPilot.

### 9. Tabby

Tabby là một trợ lý mã hóa AI tự lưu trữ mã nguồn mở. Nó có thể đề xuất toàn bộ chức năng hoặc đoạn mã nhiều dòng khi bạn nhập. Nó lấy bối cảnh từ mã và nhận xét của bạn.

Điều tốt nhất về Tabby là nó có thể được tinh chỉnh cho bất kỳ dự án nào. Để huấn luyện Tabby, bạn cần một PC có bộ tăng tốc GPU tốt (ví dụ RTX 3080). Quá trình đào tạo có thể được cấu hình bằng tệp YAML.

Bạn cũng có thể dùng thử Tabby trong trình duyệt mà không cần đăng ký.

### 10. CodeGeeX

CodeGeeX là mô hình tạo mã nguồn mở được đào tạo bằng hơn 20 ngôn ngữ lập trình (ví dụ: Python, JavaScript, Java, C++/C, Go, v.v.). Nó sử dụng 13 tỷ thông số và tạo ra kết quả chất lượng rất cao.

Nó có thể được sử dụng để gợi ý mã, dịch thuật, giải thích và tóm tắt.

Bạn cũng có thể [đọc tài liệu nghiên cứu CodeGeeX](https://arxiv.org/abs/2303.17568) để biết thêm thông tin kỹ thuật.

### 11. AskCodi

AskCodi là trợ lý mã hóa được hỗ trợ bởi AI dựa trên OpenAI GPT. Nó cung cấp một bộ chức năng, chẳng hạn như tạo mã, kiểm tra đơn vị, tài liệu và dịch ngôn ngữ. Khi nói đến môi trường phát triển, nó cũng hỗ trợ các tùy chọn phổ biến như Visual Studio Code, Sublime và bộ JetBrains. Với Codi Chat, các nhà phát triển có thể tham gia vào các cuộc đối thoại mã hóa được hỗ trợ bởi AI. Ứng dụng Dịch đơn giản hóa việc chuyển đổi giữa các ngôn ngữ lập trình khác nhau. Ngoài ra, AskCodi hỗ trợ nhiều ngôn ngữ lập trình chính.

Nền tảng AskCodi cũng có tính năng WorkBook ấn tượng. Đó là một không gian giao diện mang tính tương tác, kiểu Jupyter giúp nâng cao quá trình mã hóa. Tại đây, các nhà phát triển có thể tạo các đoạn mã và tìm kiếm lời giải thích dựa trên AI cho các đoạn mã cụ thể. WorkBook thậm chí có thể tự động hóa việc tạo tài liệu. Công cụ này đặc biệt có lợi cho những người mới bắt đầu muốn nắm bắt sự phức tạp của các ngôn ngữ lập trình mới.

AskCodi là một giải pháp thay thế miễn phí cho GitHub Copilot dành cho Mã VS. Nó sử dụng OpenAI Codex để thực hiện nhiều nhiệm vụ của trợ lý mã AI.

Ví dụ: nó có thể được sử dụng để đề xuất mã, tài liệu phần mềm, giải thích mã, kiểm tra, v.v. Bạn cũng có thể sử dụng tính năng trò chuyện của nó để bắt đầu cuộc trò chuyện với lập trình viên cặp AI của mình.

AskCodi ưu tiên quyền riêng tư của mã. Nó không lưu mã bạn truyền vào nó hoặc mã mà nó tạo ra.

Các tính năng chính:
- Tích hợp với các IDE phổ biến
- Dịch văn bản sang mã và chuyển mã sang văn bản qua WorkBook

### 12. Blackbox AI

Blackbox AI được tích hợp nhiều tính năng như tự động hoàn thành mã, tìm kiếm mã và tìm kiếm kho lưu trữ. Nó được tạo ra để tăng tốc độ phát triển phần mềm bằng cách tăng năng suất của các nhà phát triển.

Tính năng tự động hoàn thành mã cung cấp các đề xuất bằng hơn 20 ngôn ngữ lập trình dựa trên thông tin đầu vào của nhà phát triển. Tìm kiếm kho lưu trữ cho phép các nhà phát triển tìm kiếm trực tiếp qua hàng triệu tệp kho lưu trữ mã nguồn mở trong môi trường phát triển tích hợp (IDE) của họ. Tính năng tìm kiếm mã giúp nhà phát triển tìm đoạn mã cho dự án của họ bằng cách nhập câu hỏi hoặc truy vấn.

Những tính năng này cũng có sẵn trong Jupyter Lab và Jupyter Notebooks.

### 13. Replit AI

Replit AI là tập hợp các công cụ mã AI được thiết kế để nâng cao trải nghiệm mã hóa trên nền tảng của Replit. Bộ phần mềm này bao gồm một số tính năng, trong đó tính năng hoàn thành mã thông minh là chức năng hàng đầu của nó. Replit cũng có thể tạo mã giống như các công cụ mã AI khác trong danh sách này. Cuối cùng, nó cũng cung cấp giải thích về mã. Cần nhấn mạnh rằng tất cả các công cụ này đều hoạt động đồng bộ. Chúng không chỉ hợp lý hóa quá trình phát triển mà còn cung cấp những giải thích và sửa đổi sâu sắc cho mã.

AI lấy từ một nhóm mã có nguồn công khai, được tinh chỉnh bởi Replit. Nó viết mã bằng cách sử dụng các đề xuất và giải thích theo ngữ cảnh. Tất cả điều này được điều chỉnh theo ngôn ngữ và sắc thái cụ thể của dự án của bạn, cung cấp mã chất lượng cao và không có lỗi.

Mặc dù Replit AI thể hiện hiệu suất mạnh mẽ với JavaScript và Python, nhưng nó vẫn mở rộng khả năng của mình trên nhiều ngôn ngữ. Nó không chỉ bao gồm các ngôn ngữ lập trình mà còn cả SQL, HTML và CSS. Quyền truy cập vào các tính năng AI này được cung cấp miễn phí cho bất kỳ ai có tài khoản Replit. Chỉ có chức năng nâng cao, chẳng hạn như tin nhắn không giới hạn và quyền truy cập vào mô hình trò chuyện phức tạp hơn, mới yêu cầu gói trả phí.

Các tính năng chính:
- Rất nhiều chức năng có sẵn miễn phí.
- Gỡ lỗi mã chủ động. AI khắc phục sự cố cho bạn mà không cần phân tích thông báo lỗi theo cách thủ công.
- Trò chuyện AI trong IDE.

### 14. Cursor

Cursor là trình soạn thảo mã dành riêng cho việc lập trình ghép nối với AI. Nó hỗ trợ tạo mã và đề xuất tự động hoàn thành. Ngoài ra còn có một cuộc trò chuyện để nói chuyện với AI tính đến tệp hiện đang mở. Con trỏ có thể thu thập thông tin tài liệu của thư viện bên thứ ba.

Tính năng Tự động gỡ lỗi đề xuất các bản sửa lỗi trực tiếp trong cửa sổ terminal đang mở. Tương tự, có sẵn các bản sửa lỗi nhanh cho các sự cố được phát hiện bởi lint. Tính năng Terminal biến ngôn ngữ tiếng Anh thành các lệnh thích hợp. Con trỏ hỗ trợ hình ảnh trong lời nhắc.

Các tính năng chính:
- Ghép nối lập trình với AI.
- Khả năng sử dụng hình ảnh trong lời nhắc.

### 15. SQLAI

SQLAI là một công cụ tạo truy vấn cho cơ sở dữ liệu SQL và NoSQL. Nền tảng này mang lại kết quả ngay lập tức và cung cấp thư viện cá nhân để lưu trữ và chia sẻ các đoạn mã SQL và NoSQL tùy chỉnh. Nó tự hào có khả năng tích hợp dễ dàng chỉ bằng 1 cú nhấp chuột với các cơ sở dữ liệu phổ biến như MySQL, Postgres, Oracle, SQL Server và MongoDB. Tuy nhiên, nó cũng hỗ trợ các kết nối thủ công, bao gồm cả nhập CSV, để có khả năng tương thích rộng hơn.

Bằng cách đơn giản hóa quy trình thu thập thông tin chi tiết về dữ liệu theo thời gian thực, người dùng có thể chạy các truy vấn do AI tạo trực tiếp trên các nguồn dữ liệu được kết nối của họ, với kết quả được trình bày dưới dạng bảng hoặc được hiển thị trực quan thông qua biểu đồ do AI tạo ra. Công cụ này được thiết kế để giúp việc thu thập và hiển thị thông tin dữ liệu trở nên đơn giản nhất có thể.

Các tính năng chính:
- Công cụ dành cho cơ sở dữ liệu SQL và NoSQL, không dành cho ngôn ngữ lập trình.
- Tập trung vào kết quả nhanh chóng.

### 16. Snyk powered by DeepCode AI

DeepCode AI là một thành phần của nền tảng Snyk SAST . Nó được trang bị nhiều mô hình AI, mỗi mô hình được cung cấp thông tin bằng một bộ dữ liệu tập trung vào bảo mật mở rộng và chuyên môn của các nhà nghiên cứu bảo mật hàng đầu. DeepCode AI được thiết kế để xác định và khắc phục các lỗ hổng bảo mật cũng như quản lý nợ kỹ thuật một cách hiệu quả.

Trợ lý mã này sử dụng các dự án nguồn mở để đào tạo AI - với chính sách nghiêm ngặt là không sử dụng dữ liệu khách hàng. Không giống như các hệ thống mô hình đơn như ChatGPT, DeepCode AI áp dụng cách tiếp cận mô hình kết hợp, đảm bảo mức độ quét chính xác chưa từng có. Các nhà phát triển có khả năng tạo các truy vấn tùy chỉnh bằng logic của DeepCode AI.

Các tính năng chính:
- Tích hợp với hệ sinh thái Snyk.
- Tập trung vào kiểm tra an ninh.

### 17. Gemini in Android Studio

Gemini đóng vai trò là trợ lý hỗ trợ AI trong Android Studio. Nó được thiết kế để tăng năng suất thông qua khả năng diễn giải và đáp ứng các yêu cầu phát triển bằng ngôn ngữ tự nhiên. Điều này cho phép người dùng đặt câu hỏi bằng tiếng Anh đơn giản và nhận được hỗ trợ về việc tạo mã và vị trí tài nguyên. Nó cũng có thể hướng các nhà phát triển tới những phương pháp thực hành tốt nhất, tiết kiệm thời gian quý báu và giảm bớt sự thất vọng của họ.

Song Tử đôi khi có thể đưa ra những lời khuyên đầy tự tin nhưng không chính xác hoặc không đầy đủ. Điều quan trọng là phải xem xét kỹ lưỡng và kiểm tra nghiêm ngặt mã mà nó gợi ý. Mã được tạo có thể không đáp ứng được kết quả mong đợi hoặc không duy trì được tiêu chuẩn chất lượng.

Kết hợp việc hoàn thành mã do AI điều khiển, Gemini dự đoán và hiển thị khả năng tiếp tục mã. Nó đẩy nhanh quá trình mã hóa bằng cách đề xuất toàn bộ chức năng. Việc hoàn thiện mã AI này, khi được kích hoạt, có thể truyền các đoạn mã và các chi tiết liên quan khác để nâng cao ngữ cảnh mà mô hình ngôn ngữ cơ bản hiểu được, đảm bảo các đề xuất mã thích hợp hơn.

Các tính năng chính:
- Được phát triển bởi Google và được tích hợp vào Android Studio – một IDE chính thức để phát triển ứng dụng Android và Flutter gốc.
- Yêu cầu đăng nhập vào Tài khoản Google.

## Testing LLMs on Solving Leetcode Problems

Tôi chọn  Leetcode  làm nguồn gốc của các bài toán cho điểm chuẩn này vì một số lý do:

- Các bài toán Leetcode được sử dụng trong các cuộc phỏng vấn thực tế cho các vị trí kỹ sư phần mềm.
- Sinh viên khoa học máy tính học cách giải quyết các bài toán tương tự trong quá trình học tập của họ.
- Nó có một thẩm phán trực tuyến có thể kiểm tra xem giải pháp có đúng hay không chỉ sau vài giây.
- Hiệu suất của người dùng về bài toán này cũng có sẵn.

###  Datasets

Tôi muốn chạy LLM trên hai nhóm bài toán:
- những bài toán "`nổi tiếng`" không chỉ được xuất bản từ lâu mà còn được sử dụng thường xuyên nhất trong các cuộc phỏng vấn phần mềm—do đó, các giải pháp đều có sẵn rộng rãi.
- Các bài toán "`không thể nhìn thấy`" mà bản thân chúng không có trong dữ liệu LLM và giải pháp của chúng không được các LLM thử nghiệm quan sát được

![Datasets](https://boxxv.github.io/img/ai/tUyDy3WCvhMrS9XRgsoD10WmU5k2-mz932g0.jpeg "Datasets")

Việc truy xuất các báo cáo bài toán và đoạn mã từ Leetcode là một thách thức đáng chú ý nhưng cuối cùng mọi thứ cũng được giải quyết. Mã nguồn [công cụ kiểm tra của tôi có sẵn trên GitHub](https://github.com/whisk/leetgptsolver) cho bất kỳ ai quan tâm.

### Prompts and code generation

Hệ thống phán đoán trực tuyến của Leetcode hỗ trợ nhiều ngôn ngữ lập trình khác nhau, cho phép bạn chọn ngôn ngữ nào bạn thích. Không ngần ngại, tôi quyết định gắn bó với Python 3 vì mọi bài toán trên Leetcode đều có đoạn mã tương ứng. Cú pháp của nó thiên về giải quyết các bài toán thuật toán: không bắt buộc phải gõ, thao tác mảng và bản đồ dễ dàng (hoặc "danh sách" và "từ điển" theo thuật ngữ Python), và nó cũng là một trong những ngôn ngữ phổ biến nhất trên chính Leetcode. Vì vậy, những gì tốt cho con người phải phù hợp với một LLM giả vờ là một lập trình viên.

Tôi đã sử dụng cùng một lời nhắc cho mọi LLM và mọi bài toán:

```highlight
Hi, this is a coding interview. I will give you a problem statement with sample test cases and a code snippet. I expect you to write the most effective working code using C#. Here is the problem statement: 

<problem statement>

Please do not alter function signature(s) in the code snippet. Please output only valid source code which could be run as-is without any fixes, improvements or changes. Good luck!
```

Lời nhắc này không được tinh chỉnh bằng cách sử dụng bất kỳ kỹ thuật "kỹ thuật nhắc nhở" nào và cách diễn đạt của nó được cố ý tạo ra để phù hợp với một cuộc phỏng vấn viết mã trực tiếp ngoài đời thực.

Không giống như các cuộc phỏng vấn thực tế, điểm chuẩn được thiết kế theo cách này: LLM chỉ thực hiện một lần thử tạo mã mà không có bất kỳ thông tin nào trước đó về vấn đề và không biết các trường hợp thử nghiệm của nó. Không có cơ chế cung cấp phản hồi hoặc sửa mã sau khi được tạo.

Tôi đã sử dụng hạt giống ngẫu nhiên không đổi cho ChatGPT và thông số nhiệt độ thấp nhất có thể cho mô hình Gemini và Claude để làm cho đầu ra của mô hình mang tính xác định nhất có thể.

LLM được yêu cầu chỉ xuất mã đang hoạt động mà không có bất kỳ văn bản nào trước đó, điều này không đúng trong nhiều trường hợp. Một quá trình dọn dẹp cơ bản đã được triển khai và mọi thứ ngoài mã thực tế đều bị xóa và không được gửi.

###  Results

Tất cả các giải pháp được thu thập từ LLM và gửi đến hệ thống đánh giá trực tuyến Leetcode. Tôi tập hợp các kết quả lại với nhau trong một bảng duy nhất. Như đã đề cập trước đó, các bài toán về hình ảnh và nhiều chức năng cần triển khai đã được miễn trừ.

![Results](https://boxxv.github.io/img/ai/tUyDy3WCvhMrS9XRgsoD10WmU5k2-j39327u.png "Results")

Những phát hiện chính là:

- Có một khoảng cách đáng kể về hiệu suất của tất cả các LLM trên các tập hợp bài toán "nổi tiếng" và "không nhìn thấy".
- Tất cả các LLM đều có chung một mô hình hoạt động tương tự: chúng tạo ra kết quả tốt đối với các bài toán “nổi tiếng” nhưng lại gặp khó khăn với các bài toán “không nhìn thấy được”.
- ChatGPT-4, Claude Opus và Gemini 1.5 rất thân thiết với nhau; Gemini 1.0 Pro kém xa.
- Các bài toán "khó nhìn thấy" gần như không thể tiếp cận được đối với LLM: Claude 3 Opus chỉ giải quyết được một trong số chúng, còn những bài toán khác thì không giải quyết được.

Để chống lại giả thuyết cho rằng những bài toán “không nhìn thấy” phức tạp hơn những bài toán “nổi tiếng”, chúng ta nên đánh giá tỷ lệ chấp nhận của người dùng. Nó thấp hơn đối với các bài toán mới nhưng vẫn tương đối cao so với tỷ lệ chấp nhận của LLM. Tôi đưa ra giả thuyết rằng những bài toán phổ biến có tỷ lệ chấp nhận cao hơn bởi vì người dùng cố gắng hết sức để giải quyết chúng một cách xuất sắc để chuẩn bị cho các cuộc phỏng vấn xin việc.

### Future considerations

Mặc dù kết quả của LLM về các bài toán không nhìn thấy được nhìn chung là quá kém để được coi là kỹ năng kỹ thuật phần mềm vững chắc, nhưng chúng vẫn ở trên mức 0—một kết quả chưa từng có đối với bất kỳ công cụ phần mềm nào. Điều đáng nói là những kết quả đó đạt được nhanh hơn nhiều so với những gì con người có thể làm được. Có cách nào để cải thiện những bài toán chưa được nhìn thấy? Có lẽ là có, theo ba cách:

- Cải thiện lời nhắc ban đầu và điều chỉnh nó cho từng kiểu máy riêng biệt. Lời nhắc của tôi hoàn toàn chung chung và không có "kỹ thuật nhắc nhở" trong đó.
- Cung cấp phản hồi về những nỗ lực không thành công để cải thiện kết quả dần dần. Điều đó sẽ làm cho quá trình giải quyết trở nên gần gũi hơn với bối cảnh thực tế.
- Chuẩn bị các mô tả bài toán, làm cho chúng trở nên “phù hợp” hơn để các mô hình tiếp thu. Tôi không thích ý tưởng rằng LLM chỉ nên nhận các báo cáo bài toán được chuẩn bị đặc biệt; thay vào đó, họ nên xem một mô hình nhỏ hơn để cải thiện các mô tả để phù hợp hơn cho việc giải quyết. Một số mối lo ngại xuất phát từ thực tế là các bài toán Leetcode mới khiến các giải pháp được công bố nhanh chóng, do đó khiến chúng có sẵn cho LLM. Một cách giải quyết tiềm năng là sử dụng LLM để tạo ra các bài toán mới.

Những ý tưởng này cần được nghiên cứu sâu hơn và tôi hy vọng rằng ai đó hoặc tôi có thể tìm hiểu chúng.

![Claude Sonnet 3.5](https://boxxv.github.io/img/ai/UVMjGHgzyLTVNpe8tVLGDGlCYw52-us93q77.png "Claude Sonnet 3.5")

## Kết luận

Có nhiều lựa chọn thay thế miễn phí cho GitHub Copilot có thể được tích hợp với Visual Studio Code. Mỗi lựa chọn thay thế này đều cung cấp các tính năng và khả năng riêng biệt, đáp ứng các nhu cầu và sở thích mã hóa khác nhau. Cho dù bạn muốn có trợ lý mã hóa giống như chatbot, mô hình AI được cá nhân hóa, quyền truy cập ngoại tuyến, quyền riêng tư của mã hay hỗ trợ chuyên biệt cho API AWS, thì vẫn có một giải pháp thay thế phù hợp với yêu cầu của bạn.

Bây giờ là lúc thử nghiệm các trợ lý mã hóa AI khác nhau trong trình soạn thảo Visual Studio Code của bạn, tìm ra trợ lý phù hợp nhất với phong cách và quy trình mã hóa của bạn. Tận dụng sức mạnh của AI trong hành trình mã hóa của bạn và đưa quá trình phát triển của bạn lên một tầm cao mới.

Codeium nổi lên như một giải pháp thay thế miễn phí đáng chú ý cho GitHub Copilot, cung cấp cho các nhà phát triển một giải pháp mạnh mẽ và tiết kiệm chi phí để hoàn thiện và hỗ trợ mã. Với khả năng ấn tượng và giao diện thân thiện với người dùng, Codeium trao quyền cho các lập trình viên ở mọi cấp độ để hợp lý hóa quy trình công việc của họ, tăng năng suất và giải phóng tiềm năng mã hóa của họ mà không bị ràng buộc bởi đăng ký trả phí.

Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu hành trình viết mã, việc khám phá Codeium có thể là yếu tố thay đổi cuộc chơi cho quá trình phát triển của bạn. Khả năng hiểu ngữ cảnh và đưa ra các đề xuất thông minh của nó có thể giúp bạn tiết kiệm vô số giờ viết mã tẻ nhạt, cho phép bạn tập trung vào các khía cạnh sáng tạo hơn trong dự án của mình.

Để thực sự khai thác toàn bộ tiềm năng của Codeium và khám phá thêm các mẹo, thủ thuật và phương pháp hay nhất, chúng tôi mời bạn tìm hiểu sâu hơn về bộ sưu tập blog phong phú của chúng tôi. Hãy theo dõi các bài viết sâu sắc sẽ hướng dẫn bạn tận dụng các tính năng của Codeium, tích hợp nó một cách liền mạch vào quy trình làm việc của bạn và tối đa hóa tác động của nó đối với nỗ lực viết mã của bạn.

Tóm lại, tôi có thể nói rằng điều này khá tiện lợi trong việc tiết kiệm thời gian của bạn và chỉ tập trung vào phần logic. Nó cũng giúp bạn cập nhật những điều này, điều này sẽ giúp cuộc sống của Nhà phát triển hiệu quả hơn.

-----
- [10 Free GitHub Copilot Alternatives for VS Code 2024](https://bito.ai/blog/free-github-copilot-alternatives-for-vs-code/)
- [10 Best AI Coding Assistant Tools in 2024– Guide for Developers](https://www.thedroidsonroids.com/blog/best-ai-coding-assistant-tools)
- [AI Code Assistants: Head to Head](https://codeium.com/blog/code-assistant-comparison-copilot-tabnine-ghostwriter-codeium)
- [Codeium vs Amazon CodeWhisperer](https://codeium.com/compare/comparison-codewhisperer-codeium)
- [Testing LLMs on Solving Leetcode Problems](https://hackernoon.com/testing-llms-on-solving-leetcode-problems)
- [Testing LLMs on Code Generation with Varying Levels of Prompt Specificity](https://arxiv.org/pdf/2311.07599?ref=hackernoon.com)
- [An introduction to code LLM benchmarks for software engineers](https://blog.continue.dev/an-introduction-to-code-llm-benchmarks-for-software-engineers/)
- [LLM Benchmarks: Understanding Language Model Performance](https://humanloop.com/blog/llm-benchmarks)
- [My opinion after testing some AI code assistant](https://www.jujens.eu/posts/en/2023/Aug/21/ai-tests/)

-----
- [Discover the Ultimate Free Copilot Solution](https://www.valuebound.com/resources/blog/discover-ultimate-free-copilot-solution)
- [How is Codeium Free?](https://codeium.com/blog/how-is-codeium-free)
- [Bito](https://bito.ai) - [Become a 10X Dev with Bito](https://marketplace.visualstudio.com/items?itemName=Bito.Bito)
- [Codeium](https://codeium.com) - [Free AI Code Completion &amp; Chat](https://marketplace.visualstudio.com/items?itemName=Codeium.codeium)
- [Cody](https://sourcegraph.com/cody) - [AI coding assistant](https://github.com/sourcegraph/cody)
- [Tabnine](https://www.tabnine.com) - The AI code assistant that you control
- [Dùng AI để viết code không còn là viễn tưởng](https://viblo.asia/p/dung-ai-de-viet-code-khong-con-la-vien-tuong-LzD5d9q4KjY)
- AmazonQ
- [Copilot for Xcode lovers](https://viblo.asia/p/copilot-for-xcode-lovers-m2vJPk0n4eK)
- [Tổng hợp Visual Studio Code Extensions](https://viblo.asia/p/tong-hop-visual-studio-code-extensions-Ny0VGnwYLPA)

-----
- [Exploring the Claude 3 Opus, Sonnet, and Haiku Models](https://damiandabrowski.medium.com/exploring-the-claude-3-opus-sonnet-and-haiku-models-adbf9c74acaa)
- [So sánh 3 model mới nhất của Claude 3: Haiku vs Sonnet vs Opus](https://tenten.vn/ai/so-sanh-3-model-moi-nhat-cua-claude-3-haiku-vs-sonnet-vs-opus/)
- [Chấn động làng AI: Claude 3 ra mắt với hiệu suất vượt trội hơn cả Gemini và ChatGPT](https://www.thegioididong.com/tin-tuc/claude-3-ra-mat-voi-hieu-suat-vuot-troi-hon-ca-gemini-va-chatgpt-1562285)
- [Anthropic ra mắt Claude 3.5 Sonnet: Mô hình AI siêu nhanh, thông minh hơn cả GPT-4o](https://vnreview.vn/threads/anthropic-ra-mat-claude-3-5-sonnet-mo-hinh-ai-sieu-nhanh-thong-minh-hon-ca-gpt-4o.43393/)