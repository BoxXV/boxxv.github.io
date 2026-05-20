---
layout: post
title: Encoding Tiếng Nhật
subtitle: "Traditional Japanese Encoding: Hiragana, Katakana, Kanji"
date: 2026-05-19 10:11:12
tags:
- Encoding
- Japanese
- Traditional
- Hiragana
- Katakana
- Kanji
---

![Japanese Encoding](https://boxxv.github.io/img/2026/encoding_japanese_table.png "Japanese Encoding")


- [Encoding Nhật Bản truyền thống](#encoding-nhật-bản-truyền-thống)
- [Encoding Unicode (hỗ trợ đa ngôn ngữ)](#encoding-unicode-hỗ-trợ-đa-ngôn-ngữ)
- [Encoding Đông Á khác (tham khảo)](#encoding-đông-á-khác-tham-khảo)
- [Kết luận](#kết-luận)


Đây là tổng quan các encoding hỗ trợ chữ Nhật (Hiragana/Katakana):

## Encoding Nhật Bản truyền thống

| Encoding | Hiragana | Katakana | Kanji | Tiếng Việt | Ghi chú |
|---|:---:|:---:|:---:|:---:|---|
| `Shift-JIS (CP932)` | ✓ | ✓ | ✓ | ✗ | Chuẩn phổ biến nhất ở Nhật. Không hỗ trợ ký tự có dấu tiếng Việt (ă, ơ, ư, đ…). Windows/Excel Nhật dùng mặc định. |
| `EUC-JP` | ✓ | ✓ | ✓ | ✗ | Phổ biến trên Unix/Linux Nhật. Không hỗ trợ tiếng Việt có dấu. |
| `ISO-2022-JP` | ✓ | △ | ✓ | ✗ | Dùng escape sequence để chuyển đổi bộ ký tự. Katakana hỗ trợ hạn chế. Dùng trong email cũ. |

## Encoding Unicode (hỗ trợ đa ngôn ngữ)

| Encoding | Hiragana | Katakana | Kanji | Tiếng Việt | Ghi chú |
|---|:---:|:---:|:---:|:---:|---|
| `UTF-8` ⭐ Khuyến nghị | ✓ | ✓ | ✓ | ✓ | Hỗ trợ toàn bộ Unicode. Tiêu chuẩn web/API hiện đại. Dùng BOM (`utf-8-sig`) để Excel nhận dạng đúng. |
| `UTF-8 BOM (utf-8-sig)` 📊 Excel-friendly | ✓ | ✓ | ✓ | ✓ | Thêm BOM `\xEF\xBB\xBF` ở đầu file. Excel tự nhận dạng UTF-8 và hiển thị đúng cả tiếng Nhật lẫn tiếng Việt. |
| `UTF-16 LE` | ✓ | ✓ | ✓ | ✓ | Mỗi ký tự 2 byte. Tương thích tốt với Windows. File to hơn UTF-8 nhưng đọc nhanh hơn với ký tự CJK. |
| `UTF-32` | ✓ | ✓ | ✓ | ✓ | Mỗi ký tự cố định 4 byte. Ít dùng vì lãng phí bộ nhớ. Xử lý đơn giản nhất về mặt lập trình. |

## Encoding Đông Á khác (tham khảo)

| Encoding | Hiragana | Katakana | Kanji | Tiếng Việt | Ghi chú |
|---|:---:|:---:|:---:|:---:|---|
| `Big5` | ✗ | ✗ | △ | ✗ | Tiếng Trung phồn thể (Đài Loan). Không hỗ trợ Hiragana/Katakana. |
| `GB2312 / GBK` | ✗ | ✗ | △ | ✗ | Tiếng Trung giản thể (Đại lục). Một số Kanji trùng nhưng không hỗ trợ Kana. |

---

**Chú thích:**
- ✓ Hỗ trợ đầy đủ
- △ Hỗ trợ một phần
- ✗ Không hỗ trợ

---

## Kết luận

Trên đây là các So sánh khả năng hỗ trợ ký tự Nhật và tiếng Việt của các encoding phổ biến.

Nếu cần kết hợp **tiếng Nhật và tiếng Việt** trong cùng một file, hãy dùng **`UTF-8 BOM (utf-8-sig)`** — hỗ trợ toàn bộ Unicode và Excel mở đúng encoding tự động, không cần cấu hình thêm.


-----
Tham khảo:
- [Japanese Character Encodings](https://docs.tailor.tech/reference/concepts/character-encodings.html)
- [Character encoding](https://nozer0.github.io/en/technology/system/character-encoding/)
- []()
- [Convert legacy Japanese encoding by Red](https://dev.to/kobayu/my-red-story-3-converting-legacy-japanese-encoding-to-utf-8-31d6)
- []()
