---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: "Dùng Claude Code với các tệp MD bắt buộc: PRD, Architecture, Design, RULES, TASKS, PROGRESS"
subtitle: "Claude Code and the mandatory MD files for vibe coding"
date: 2026-11-13 09:00:00 +0700
tags:
- Claude
- Claude Code
- Vibe Coding
- AI
- CLAUDE.md
---

> Bài viết tham khảo ý tưởng từ [The Beginning of Vibe Coding — 6 Mandatory MD Files](https://www.kazi-rahamatullah.com/blog/vibe-coding-md-files) của Kazi Rahamatullah (13/07/2026) và tài liệu chính thức của Claude Code. Bài gốc dùng tên `Rules.md`, `Phases.md`, `Memory.md`; ở đây mình dùng `RULES.md`, `TASKS.md`, `PROGRESS.md` cho cùng vai trò.

- [Vì sao cần các tệp MD?](#vì-sao-cần-các-tệp-md)
- [Giá trị của PRD.md, Architecture.md, Design.md, RULES.md, TASKS.md, PROGRESS.md](#giá-trị-của-prdmd-architecturemd-designmd-rulesmd-tasksmd-progressmd)
  - [Thứ tự ưu tiên cho dự án mới](#thứ-tự-ưu-tiên-cho-dự-án-mới)
  - [Để các file hoạt động hiệu quả](#để-các-file-hoạt-động-hiệu-quả)
- [Reset Mức sử dụng](#reset-mức-sử-dụng)
  - [1. Phiên tự đặt lại (5 giờ)](#1-phiên-tự-đặt-lại-5-giờ)
  - [2. Giới hạn tuần tự đặt lại](#2-giới-hạn-tuần-tự-đặt-lại)
  - [3. Nút "Đặt lại miễn phí" (Đặt lại toàn bộ)](#3-nút-đặt-lại-miễn-phí-đặt-lại-toàn-bộ)
  - [4. Tối đa bao nhiêu tokens?](#4-tối-đa-bao-nhiêu-tokens)

# Vì sao cần các tệp MD?

"Vibe coding" là cách làm phần mềm cùng AI: bạn mô tả, AI viết code, bạn định hướng. Nếu không có cấu trúc, dự án dễ "trôi": AI chọn sai thư viện, mỗi phiên tổ chức thư mục một kiểu, tính năng làm dở, và không có nguồn sự thật chung. Một cửa sổ chat không thể giữ hết ngữ cảnh, nên cách khắc phục là đặt sẵn vài tệp Markdown ở gốc dự án (hoặc thư mục `docs/`) trước khi bắt đầu ra lệnh.

Tóm tắt nội dung từng tệp theo bài gốc:

| File | Trả lời câu hỏi | Nội dung chính | Tạo khi nào |
|---|---|---|---|
| **PRD.md** | Làm gì, cho ai? | Tóm tắt sản phẩm 1 đoạn, vấn đề cốt lõi, tiêu chí thành công, người dùng mục tiêu, tính năng MVP, những gì **không** làm | Ngày đầu tiên |
| **Architecture.md** | Tổ chức hệ thống thế nào? | Luồng người dùng, sơ đồ tầng (UI → API → service → data), xác thực, quản lý state, cây thư mục, quy ước đặt tên, stack và lý do chọn | Ngày đầu tiên |
| **RULES.md** | AI được/không được làm gì? | Thư viện và pattern được dùng, cái bị cấm, không commit khi chưa được yêu cầu, không thêm dependency khi chưa duyệt, diff nhỏ nhất | Ngày đầu tiên |
| **TASKS.md** (Phases.md) | Làm theo thứ tự nào? | Các giai đoạn nhỏ, mỗi giai đoạn có checklist và tiêu chí "Xong khi…", phụ thuộc giữa các giai đoạn | Sau khi PRD rõ |
| **Design.md** | Giao diện trông ra sao? | Bảng màu (mã hex), token sáng/tối, font, thang chữ | Trước khi làm UI |
| **PROGRESS.md** (Memory.md) | Đang ở đâu? | Việc đã xong kèm ngày, quyết định và lý do, task hiện tại, vướng mắc | Khi bắt đầu code |

Lời khuyên của tác giả: dành khoảng 30 phút cho 5 file đầu trước prompt code đầu tiên, giữ các giai đoạn nhỏ (1–2 phiên làm việc), và cập nhật Memory/PROGRESS cuối mỗi phiên. Không có tài liệu, "vibe coding" sẽ thành "vibe drifting".

# Giá trị của PRD.md, Architecture.md, Design.md, RULES.md, TASKS.md, PROGRESS.md

**Trả lời ngắn:** Có giá trị, nhưng chỉ hiệu quả khi Claude biết lúc nào cần đọc file nào. Claude Code chỉ tự động nạp **CLAUDE.md** khi mở phiên; 6 file kia sẽ không được đọc trừ khi bạn nhắc, hoặc CLAUDE.md trỏ tới chúng. Nếu không có CLAUDE.md, các file này gần như "vô hình" với Claude cho đến khi bạn bảo nó đọc.

## Thứ tự ưu tiên cho dự án mới

| # | File | Giá trị | Cần khi nào | Ghi chú |
|---|---|---|---|---|
| 0 | **CLAUDE.md** (không có trong danh sách nhưng nên có) | Rất cao | Ngay từ đầu | File "trung tâm", trỏ tới các file còn lại |
| 1 | **PRD.md** | Rất cao | Trước khi viết dòng code đầu tiên | Làm gì, cho ai, phạm vi, cái gì *không* làm. Thiếu file này Claude dễ tự thêm tính năng không ai yêu cầu |
| 2 | **Architecture.md** | Rất cao | Sau PRD, trước khi code | Stack, cấu trúc thư mục, luồng dữ liệu, các quyết định kỹ thuật. Giúp Claude không tự bịa cấu trúc khác nhau giữa các phiên |
| 3 | **TASKS.md** | Cao | Khi bắt đầu code | Chia việc nhỏ, có checkbox. Rất hợp với cách Claude Code làm việc: mỗi phiên làm một vài task |
| 4 | **RULES.md** | Trung bình | Khi bắt đầu code, bổ sung dần | Quy ước code, cách đặt tên, lệnh test/lint. **Nên gộp vào CLAUDE.md** vì đây đúng là chức năng của CLAUDE.md và được nạp tự động |
| 5 | **Design.md** | Trung bình (chỉ khi có UI) | Trước khi làm giao diện | Màu, font, component, layout. Dự án không có UI thì bỏ |
| 6 | **PROGRESS.md** | Thấp đến trung bình | Khi dự án kéo dài nhiều phiên | Trùng nhiều với TASKS.md và git log. **Có thể gộp vào TASKS.md** (thêm mục "Đã xong / Đang làm / Vướng mắc") |

Như vậy, bộ tối thiểu hiệu quả nhất là 4 file: **CLAUDE.md** (có luôn rules), **PRD.md**, **Architecture.md**, **TASKS.md**. Design.md thêm vào nếu có UI.

## Để các file hoạt động hiệu quả

**Đừng nạp tất cả vào mọi phiên.** Claude Code hỗ trợ import kiểu `@PRD.md` trong CLAUDE.md, nhưng import nghĩa là file được nạp toàn bộ mỗi phiên, tốn ngữ cảnh và hạn mức sử dụng. Cách tốt hơn là ghi rõ trong CLAUDE.md *khi nào* đọc file nào, ví dụ:

```markdown
## Tài liệu dự án
- docs/PRD.md: đọc khi thêm/sửa tính năng, để kiểm tra phạm vi
- docs/Architecture.md: đọc trước khi tạo file/module mới
- docs/Design.md: đọc khi làm giao diện
- docs/TASKS.md: đọc đầu mỗi phiên; cập nhật checkbox khi xong task

## Quy tắc
- Không làm ngoài phạm vi PRD; nếu cần, hỏi trước
- Đổi kiến trúc thì cập nhật Architecture.md
```

**Giữ file ngắn và đúng sự thật.** Tài liệu lỗi thời còn tệ hơn không có, vì Claude sẽ tin và làm theo. Viết gạch đầu dòng, quyết định cụ thể, tránh văn dài.

**Bảo Claude cập nhật.** Claude không tự sửa TASKS.md hay Architecture.md trừ khi được dặn. Thêm quy tắc "cập nhật TASKS.md sau mỗi task" vào CLAUDE.md, và cuối phiên nhắc nó ghi lại tiến độ.

**Để Claude viết nháp giúp.** Với dự án mới, bạn có thể mô tả ý tưởng rồi bảo Claude soạn PRD.md, sau đó Architecture.md, rồi TASKS.md, và bạn duyệt từng file trước khi chuyển sang file tiếp theo. Lệnh `/init` cũng tạo sẵn một CLAUDE.md, nhưng nó hữu ích hơn khi repo đã có code.

# Reset Mức sử dụng

Trang **Cài đặt → Mức sử dụng** của Claude hiển thị giới hạn phiên (5 giờ), giới hạn tuần (Tất cả mô hình, Fable) và có thể có nút **"Đặt lại miễn phí"**. Ví dụ dưới đây giả sử phiên đặt lại lúc 19:00, phiên hiện tại và tuần đều đang ở 64%.

## 1. Phiên tự đặt lại (5 giờ)

Mỗi phiên kéo dài 5 giờ, tính từ lúc bạn bắt đầu dùng. Giới hạn phiên đặt lại mỗi năm giờ trên cả gói Free và gói trả phí. Vì vậy, nếu dùng liên tục không nghỉ:

* 1 ngày: tối đa khoảng 4–5 lần (24 ÷ 5 = 4,8).
* 1 tuần: tối đa khoảng 33–34 lần (168 ÷ 5 = 33,6).

Nhưng thực tế bạn không dùng hết được chừng đó phiên, vì giới hạn tuần (Tất cả mô hình, Fable) sẽ chặn trước. Trong ví dụ, phiên hiện tại và tuần đều đang ở 64%, nghĩa là giới hạn tuần mới là thứ quyết định bạn dùng được bao nhiêu.

## 2. Giới hạn tuần tự đặt lại

* 1 tuần: 1 lần, vào 00:00 Thứ 4 (cả "Tất cả mô hình" và "Fable").
* 1 ngày: 0 lần (trừ đúng ngày Thứ 4).

## 3. Nút "Đặt lại miễn phí" (Đặt lại toàn bộ)

Đây không phải quota cố định theo ngày hay tuần. Lượt đặt lại được tặng thỉnh thoảng cho các gói đủ điều kiện. Ví dụ bạn có 1 lượt, hết hạn lúc 05:00 ngày 11/12, và chỉ dùng được 1 lần. Một số điểm cần biết:

* Tuỳ loại, nó đưa giới hạn 5 giờ hoặc giới hạn tuần về đầy ngay lập tức; lịch đặt lại hằng tuần vẫn giữ nguyên ngày giờ cũ; không cần đợi chạm giới hạn mới dùng; dùng rồi thì không hoàn tác được.
* Nếu bạn hạ gói hoặc huỷ trước khi dùng thì lượt này mất.

**Mẹo:** nên để dành lượt này đến khi giới hạn tuần gần 100% mà còn vài ngày mới tới Thứ 4, như vậy mới tận dụng được nhiều nhất. Dùng lúc tuần mới 64% là lãng phí 64% đó.

## 4. Tối đa bao nhiêu tokens?

Anthropic không công bố con số token cho gói Team hay các gói khác, nên không thể đưa ra một con số chính xác. Claude hiển thị mức dùng bằng phần trăm thay vì số tin nhắn, vì chi phí mỗi tin nhắn phụ thuộc vào độ dài, file đính kèm và mô hình. Dùng Fable hay Opus sẽ tốn nhanh hơn Sonnet hay Haiku, và hội thoại càng dài thì mỗi tin nhắn càng tốn nhiều (vì Claude phải đọc lại toàn bộ ngữ cảnh). Các con số token bạn có thể thấy trên mạng chỉ là ước tính của người dùng, không phải số chính thức.

-----
Tham khảo:
- [Claude Code – Manage memory (CLAUDE.md)](https://docs.claude.com/en/docs/claude-code/memory)
- [What is a limit reset? – Claude Help Center](https://support.claude.com/en/articles/17007452-what-is-a-limit-reset)
- [The Beginning of Vibe Coding — 6 Mandatory MD Files](https://www.kazi-rahamatullah.com/blog/vibe-coding-md-files)
- []()