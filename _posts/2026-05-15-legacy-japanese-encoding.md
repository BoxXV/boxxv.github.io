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
- [Cách đọc file CSV có encoding hỗn hợp (Shift-JIS và UTF-8)](#cách-đọc-file-csv-có-encoding-hỗn-hợp-shift-jis-và-utf-8)
  - [Phương pháp 1 — Tự động phát hiện encoding](#phương-pháp-1--tự-động-phát-hiện-encoding)
  - [Phương pháp 2 — Đọc CSV với encoding đã xác định](#phương-pháp-2--đọc-csv-với-encoding-đã-xác-định)
  - [Phương pháp 3 — Dùng thư viện CharsetDetector (chính xác hơn)](#phương-pháp-3--dùng-thư-viện-charsetdetector-chính-xác-hơn)
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

## Cách đọc file CSV có encoding hỗn hợp (Shift-JIS và UTF-8)

![CSV Encoding](https://boxxv.github.io/img/2026/csv_encoding_detection_flow.svg "CSV Encoding")

### Phương pháp 1 — Tự động phát hiện encoding

```csharp
using System;
using System.IO;
using System.Text;
using Microsoft.VisualBasic.FileIO; // cần thêm reference

// Đăng ký encoding provider để dùng Shift-JIS (CP932)
Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);

public static Encoding DetectEncoding(string filePath)
{
    byte[] buffer = new byte[4];
    using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
    int bytesRead = fs.Read(buffer, 0, 4);

    // UTF-8 BOM: EF BB BF
    if (bytesRead >= 3 && buffer[0] == 0xEF && buffer[1] == 0xBB && buffer[2] == 0xBF)
        return new UTF8Encoding(true); // có BOM

    // Kiểm tra pattern Shift-JIS: byte đầu trong vùng 0x81–0x9F hoặc 0xE0–0xFC
    if (bytesRead >= 2)
    {
        byte b = buffer[0];
        if ((b >= 0x81 && b <= 0x9F) || (b >= 0xE0 && b <= 0xFC))
            return Encoding.GetEncoding(932); // Shift-JIS
    }

    return new UTF8Encoding(false); // fallback UTF-8 không BOM
}
```

### Phương pháp 2 — Đọc CSV với encoding đã xác định

```csharp
public static List<string[]> ReadCsv(string filePath)
{
    Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);

    var encoding = DetectEncoding(filePath);
    var rows = new List<string[]>();

    using var reader = new StreamReader(filePath, encoding);
    using var parser = new TextFieldParser(reader)
    {
        TextFieldType = FieldType.Delimited,
        HasFieldsEnclosedInQuotes = true
    };
    parser.SetDelimiters(",");

    while (!parser.EndOfData)
    {
        string[]? fields = parser.ReadFields();
        if (fields != null)
            rows.Add(fields);
    }

    return rows;
}
```

### Phương pháp 3 — Dùng thư viện CharsetDetector (chính xác hơn)

Khi file không có BOM và khó đoán, dùng `ude` (Universal Charset Detector):

```bash
dotnet add package UDE.NetStandard
```

```csharp
using UDE.Core;

public static Encoding DetectEncodingAuto(string filePath)
{
    Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);

    using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
    var detector = new CharsetDetector();
    detector.Feed(fs);
    detector.DataEnd();

    string charset = detector.Charset ?? "utf-8";
    Console.WriteLine($"Detected: {charset} (confidence: {detector.Confidence:P0})");

    return Encoding.GetEncoding(charset);
}
```

Ví dụ sử dụng tổng hợp

```csharp
var rows = ReadCsv("data.csv");

foreach (var row in rows)
{
    foreach (var field in row)
        Console.Write($"{field}\t");
    Console.WriteLine();
}
```

Lưu ý quan trọng
- **Đăng ký encoding provider**: `Encoding.RegisterProvider(CodePagesEncodingProvider.Instance)` bắt buộc phải gọi một lần trước khi dùng `Encoding.GetEncoding(932)` trên .NET Core / .NET 5+. .NET Framework không cần bước này.
- **NuGet cần thiết**: `Microsoft.VisualBasic` (nếu dùng `TextFieldParser` trên .NET Core), và `UDE.NetStandard` nếu muốn auto-detect chính xác hơn.
- **Shift-JIS vs CP932**: Trong thực tế file Nhật thường là CP932 (Windows code page 932) — là superset của Shift-JIS chuẩn, nên dùng `GetEncoding(932)` thay vì `"shift_jis"`.


## Kết luận

Trên đây là các So sánh khả năng hỗ trợ ký tự Nhật và tiếng Việt của các encoding phổ biến.

Nếu cần kết hợp **tiếng Nhật và tiếng Việt** trong cùng một file, hãy dùng **`UTF-8 BOM (utf-8-sig)`** — hỗ trợ toàn bộ Unicode và Excel mở đúng encoding tự động, không cần cấu hình thêm.


-----
Tham khảo:
- [Japanese Character Encodings](https://docs.tailor.tech/reference/concepts/character-encodings.html)
- [Character encoding](https://nozer0.github.io/en/technology/system/character-encoding/)
- [Convert legacy Japanese encoding by Red](https://dev.to/kobayu/my-red-story-3-converting-legacy-japanese-encoding-to-utf-8-31d6)