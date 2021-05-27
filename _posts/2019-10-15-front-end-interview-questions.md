---
layout: post
title: Tổng hợp những câu hỏi phỏng vấn Front-end
subtitle: Vì một tương lai lương cao ngất
tags:
- Front-end
- HTML
- CSS
- Javascript
- Interview
- Questions
- Answers
---
Trong bài viết này, tôi sẽ tổng hợp lại những kiến thức về Front-end, mà có thể các bạn sẽ được hỏi khi đi phỏng vấn.

## 61 câu hỏi phỏng vấn Html/CSS
    1. Thẻ Meta được dùng để làm gì trong hmtl?
    2. Iframe là gì và nó hoạt động như thế nào?
    3. Giới thiệu sơ về thẻ meta trong HTML?
    4. Mục đích của thuộc tính alt trong thẻ img?
    5. Khai báo “DOCTYPE” dùng để làm gì?
    6. Liệt kê 3 cách để định nghĩa 1 color trong html?
    7. Giải thích ý nghĩa các CSS selectors dưới đây?
    8. Giải thích các đơn vị độ dài trong css dưới đây?
    9. CSS có phân biệt hoa thường không?
    10. Thuộc tính float trong CSS thường dùng để làm gì?
    11. Margin và padding khác nhau thế nào?
    12. Display:inline và display:block khác nhau thể nào?
    13. Làm sao để add 1 comments trong CSS?
    14. Điểm khác nhau giữa CSS và CSS3?
    15. Thuộc tính “opacity” được dùng làm gì?
    16. Điểm khác biệt giữa “width: auto” và “width: 100%” trong CSS?
    17. Thẻ “div” và thẻ “span” khác nhau thế nào?
    18. Giải thích các giá trị của thuộc tính position: Fixed, Absolute, Relative, Static.
    19. Làm cách nào để có có thứ hạng tốt hơn trong SEO bởi Search Engines (ví dụ Google)?
    20. Mô tả các tính năng chính của HTML5?
    21. Làm sao để làm nổi bật (highlight) text trong HTML?
    22. Mô tả ngắn gọn cách sử dụng chính xác các phần tử ngữ nghĩa HTML5 sau: <header>, <article>, <section>, <footer>
    23. Character Encoding là gì?
    24. Thẻ tự đóng (self closing tag) là gì?
    25. Sự khác biệt giữa "attribute" (thuộc tính) và "property" (đặc tính) trong HTML?
    26. Khi nào thì thích hợp để sử dụng thẻ small?
    27. Giải thích sự khác biệt giữa các phần tử <block> và các phần tử <inline> ?
    28. Giải thích 3 mode trong html: almost standard, full standard và quirks?
    29. Bạn đặt chế độ tương thích với IE như thế nào?
    30. Có gì mới trong html5?
    31. Bạn đã từng sử dụng ngôn ngữ nào khác HTML chưa?
    32. Làm sao để thực hiện 1 nội dung bằng đa ngôn ngữ trong 1 website?
    33. Làm thế nào để bạn thay đổi hướng của văn bản html?
    34. Thẻ optional là gì?
    35. Sự khác nhau giữa <section> và <div>?
    36. Thuộc tính defer và async trên thẻ <script> là gì?
    37. Mục đích của chặn bộ nhớ cache (Cache busting) là gì và làm thế nào bạn có thể thực hiện nó?
    38. Một số khác biệt mà XHTML có so với HTML?
    39. Web Workers là gì?
    40. Thuộc tính rel="noopener" được sử dụng ở đâu và tại sao?
    41. WebSQL là gì?
    42. DOCTYPE làm gì?
    43. DOM là gì?
    44. Giải thích sự khác biệt giữa Cookie, Session Storage và Local Storage?
    45. HTML5 Web Storage là gì? Giải thích sự khác nhau giữa localStorage và sessionStorage?
    46. Một trang web có thể chứa nhiều thẻ <header> hay thẻ <footer> không?
    47. Các thuộc tính "data-" có lợi cho việc gì?
    48. WebSQL là gì?
    49. Mục đích của thẻ <main> là gì?
    50. Các khối xây dựng (building blocks) của HTML5 là gì?
    51. Tại sao sử dụng thẻ ngữ nghĩa (semantic) HTML5?
    52. HTML Preprocessor là gì và bạn có đang dùng chúng không?
    53. Progressive rendering là gì?
    54. Tại sao bạn sử dụng thuộc tính “srcset” trong thẻ <img>? Giải thích quy trình mà trình duyệt sử dụng khi đánh giá nội dung của thuộc tính này. 
    55. Bạn phải lưu ý những điều gì khi phát triển các trang web đa ngôn ngữ?
    56. WebP là gì?
    57. Bạn sẽ chọn sử dụng svg hay canvas cho trang web của mình?
    58. Làm thế nào để tạo khoá công khai (public key) trong HTML?
    59. IndexedDB là gì?
    60. Accessibility và ARIA role có ý nghĩa gì trong một ứng dụng web?
    61. Web Components là gì?

### 1. Thẻ Meta được dùng để làm gì trong hmtl?
Thẻ Meta trong html được các developer sử dụng để báo cho trình duyệt về mô tả trang, tác giả, tập ký tự, các từ khóa và nhiều thứ khác.

Thẻ Meta được sử dụng cho việc tối ưu hóa công cụ tìm kiếm để nói cho công cụ tìm kiếm về nội dung trang.
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale = 1.0">
<meta name="description" content="HTML interview questions">
<meta name="author" content="Author Name">
<meta name="copyright" content="All Rights Reserved">
```

### 2. Iframe là gì và nó hoạt động như thế nào?
Iframe là một văn bản HTML (HTML document) được nhúng vào một trang html khác.
```html
<iframe src="https://github.com" height="300px" width="300px"></iframe>
```

### 3. Giới thiệu sơ về thẻ meta trong HTML?


4. Mục đích của thuộc tính alt trong thẻ img?
5. Khai báo “DOCTYPE” dùng để làm gì?
6. Liệt kê 3 cách để định nghĩa 1 color trong html?
7. Giải thích ý nghĩa các CSS selectors dưới đây?
8. Giải thích các đơn vị độ dài trong css dưới đây?
9. CSS có phân biệt hoa thường không?
10. Thuộc tính float trong CSS thường dùng để làm gì?
11. Margin và padding khác nhau thế nào?
12. Display:inline và display:block khác nhau thể nào?
13. Làm sao để add 1 comments trong CSS?
14. Điểm khác nhau giữa CSS và CSS3?
15. Thuộc tính “opacity” được dùng làm gì?
16. Điểm khác biệt giữa “width: auto” và “width: 100%” trong CSS?
17. Thẻ “div” và thẻ “span” khác nhau thế nào?
18. Giải thích các giá trị của thuộc tính position: Fixed, Absolute, Relative, Static.
19. Làm cách nào để có có thứ hạng tốt hơn trong SEO bởi Search Engines (ví dụ Google)?
20. Mô tả các tính năng chính của HTML5?
21. Làm sao để làm nổi bật (highlight) text trong HTML?
22. Mô tả ngắn gọn cách sử dụng chính xác các phần tử ngữ nghĩa HTML5 sau: <header>, <article>, <section>, <footer>
23. Character Encoding là gì?
24. Thẻ tự đóng (self closing tag) là gì?
25. Sự khác biệt giữa "attribute" (thuộc tính) và "property" (đặc tính) trong HTML?
26. Khi nào thì thích hợp để sử dụng thẻ small?
27. Giải thích sự khác biệt giữa các phần tử <block> và các phần tử <inline> ?
28. Giải thích 3 mode trong html: almost standard, full standard và quirks?
29. Bạn đặt chế độ tương thích với IE như thế nào?
30. Có gì mới trong html5?
31. Bạn đã từng sử dụng ngôn ngữ nào khác HTML chưa?
32. Làm sao để thực hiện 1 nội dung bằng đa ngôn ngữ trong 1 website?
33. Làm thế nào để bạn thay đổi hướng của văn bản html?
34. Thẻ optional là gì?
35. Sự khác nhau giữa <section> và <div>?
36. Thuộc tính defer và async trên thẻ <script> là gì?
37. Mục đích của chặn bộ nhớ cache (Cache busting) là gì và làm thế nào bạn có thể thực hiện nó?
38. Một số khác biệt mà XHTML có so với HTML?
39. Web Workers là gì?
40. Thuộc tính rel="noopener" được sử dụng ở đâu và tại sao?
41. WebSQL là gì?
42. DOCTYPE làm gì?
43. DOM là gì?
44. Giải thích sự khác biệt giữa Cookie, Session Storage và Local Storage?
45. HTML5 Web Storage là gì? Giải thích sự khác nhau giữa localStorage và sessionStorage?
46. Một trang web có thể chứa nhiều thẻ <header> hay thẻ <footer> không?
47. Các thuộc tính "data-" có lợi cho việc gì?
48. WebSQL là gì?
49. Mục đích của thẻ <main> là gì?
50. Các khối xây dựng (building blocks) của HTML5 là gì?
51. Tại sao sử dụng thẻ ngữ nghĩa (semantic) HTML5?
52. HTML Preprocessor là gì và bạn có đang dùng chúng không?
53. Progressive rendering là gì?
54. Tại sao bạn sử dụng thuộc tính “srcset” trong thẻ <img>? Giải thích quy trình mà trình duyệt sử dụng khi đánh giá nội dung của thuộc tính này. 
55. Bạn phải lưu ý những điều gì khi phát triển các trang web đa ngôn ngữ?
56. WebP là gì?
57. Bạn sẽ chọn sử dụng svg hay canvas cho trang web của mình?
58. Làm thế nào để tạo khoá công khai (public key) trong HTML?
59. IndexedDB là gì?
60. Accessibility và ARIA role có ý nghĩa gì trong một ứng dụng web?
61. Web Components là gì?






Tham khảo:
- [61 câu hỏi phỏng vấn Html/CSS](https://www.phongvanit.com/ky-nang/htmlcss-1007)
- [42 câu hỏi phỏng vấn Javascript](https://www.phongvanit.com/ky-nang/javascript-1000)

