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
- Thẻ meta luôn đi bên trong phần tử <head> và thường được sử dụng để chỉ định bộ ký tự, mô tả trang, từ khóa, tác giả của tài liệu và cài đặt chế độ xem.
- Thẻ meta luôn có cặp tên/giá trị.
- Dữ liệu meta sẽ không được hiển thị trên trang nhưng có thể phân tích cú pháp bằng máy.
- Thẻ meta được sử dụng bởi các trình duyệt (cách hiển thị nội dung hoặc tải lại trang), công cụ tìm kiếm (từ khóa) và các dịch vụ web khác.
```html
<!DOCTYPE html>
<html>
    <head>
        <meta name="description" content="I am a web page with description" />
        <title>Home Page</title>
    </head>
    <body></body>
</html>
```

### 4. Mục đích của thuộc tính alt trong thẻ img?
Thuộc tính alt cung cấp thông tin về hình ảnh trong trường hợp người dùng không xem được ảnh (sai đường dẫn hoặc ảnh không tìm thấy).

Thuộc tính alt thường được dùng để mô tả thông tin hình ảnh , một số trường hợp thuộc tính alt được dùng trong mục đích trang trí, một số trường hợp thuộc tính alt có thể bị bỏ trống.

### 5. Khai báo `DOCTYPE` dùng để làm gì?
Để trình duyệt nhận biết trang html đó được viết ở phiên bản nào.

### 6. Liệt kê 3 cách để định nghĩa 1 color trong html?
- Hex (color: #FFFFFF) 
- Name (color: red) 
- RGB(0,0,225)

### 7. Giải thích ý nghĩa các CSS selectors dưới đây?
“div, p”: chọn tất cả các thẻ div và tất cả các thẻ p.
“div p”: chọn tất cả các thẻ p nằm trong thẻ div.
“div > p”: chọn tất cả thẻ p có thẻ cha trực tiếp là thẻ div.
“div + p”: chọn tất cả thẻ p được đặt trực tiếp sau thẻ div.
“div ~ p”: chọn tất cả thẻ p đứng trước nó là thẻ div.

### 8. Giải thích các đơn vị độ dài trong css dưới đây?
- Cm: centimeters.
- Em: elements, ví dụ 2 em = 2 lần font-size của thẻ đó.
- In: inches. - Mm: millimeters.
- Pc: picas ( 1pc = 12pt = 1/6 in)
- Pt: points ( 1pt = 1/72 in) - Px: pixels ( 1/96 in)

### 9. CSS có phân biệt hoa thường không?
Không phân biệt.

### 10. Thuộc tính float trong CSS thường dùng để làm gì?
Dùng để đặt các thẻ HTML theo hướng nằm ngang, float thường dùng 2 giá trị left và right.

### 11. Margin và padding khác nhau thế nào?
Hiểu đơn giản thì margin căn lề ngoài và padding căn lề trong của thẻ đó.

### 12. Display:inline và display:block khác nhau thể nào?
Block sẽ làm thẻ đó có space trước và sau nó, và space đó sẽ chiếm hết các width có sẵn. Inline thì chỉ xài đủ width yêu cầu.

### 13. Làm sao để add 1 comments trong CSS?
Dùng cặp dấu /* comments */.

### 14. Điểm khác nhau giữa CSS và CSS3?
Một số tính năng nổi bật được bổ sung thêm trong CSS3:
    animation: Xác định chuyển động của một thành phần
    appearance: Định dạng cho thành phần trông như giao diện chuẩn gần với người dùng.
    backface-visibility: Xác định bề mặt sau của thành phần khi thực hiện một chuyển động xoay.
    background-clip: Xác định vùng background được cắt bớt theo vùng được giới hạn.
    background-origin: Xác định giá trị tương đối của background giới hạn theo vùng giới hạn.
    background gradient: Tạo màu sắc cho background theo biên độ giảm dần đều.
    multiple background: Sử dụng để khai báo nhiều background khác nhau trong cùng một tag.
    border-image: Dùng để định dạng các border bằng hình ảnh.
    border-radius: Dùng để định dạng các dạng bo góc của border.
    box-align: Xác định vị trí cho thành phần thoe chiều dọc hoặc theo chiều thẳng đứng.
    box-direction: Xác định hướng cho thành phần.
    box-flex: Xác định sự ưu tiên linh hoạt theo các thành phần khác.
    box-ordinal-group: Cho biết thứ tự ưu tiên của các thành phần.
    box-orient: Xác định thành phần theo mép rìa của thành phần.
    box-sizing: Xác định lại chiều rộng và chiều cao của thành phần.
    box-shadow: Định dạng bóng cho thành phần.
    column: Dùng để chia nội dung thành phần thành nhiều cột khác nhau.
    @font-face: Định dạng các dạng font chữ khác nhau theo các dạng font riêng.
    font-size-adjust: Dùng để định dạng điều chỉnh cho font chữ, độ lớn của chữ được thể hiện bởi phép nhân.
    @keyframes: Dùng để điều khiển diễn biến một hoạt động của thành phần, được dùng kèm với thuộc tính animation
    nav: Di chuyển qua lại giữa các thành phần điều hướng (navigate) bằng ác di chuyển các phím mũi tên
    opacity: Hiển thị cấp độ trong suốt cho thành phần.
    perspective: Cho ta thấy được chiều sâu của thành phần trong khai báo 3D.
    perspective-origin: Định nghĩa trục quay cho thành phần sử dụng perspective.
    resize: Định dạng cho vùng nội dung mà người dụng có thể thay đổi được kích thước.
    text-justify: Tăng hoặc giảm khoảng cách giữa các từ và giữa các ký tự sao cho dàn đều thành phần.
    text-overflow: Xác định vùng text được cắt bớt.
    text-shadow: Xác định đổ bóng cho text.
    transform: Xác định một quá trình chuyển đổi khi có một hành động.
    word-break: Sẽ làm cho những hữ trong một từ không còn là một thể thống nhất, nghĩa là có thể xuống dòng bất cứ vị trí nào trong từ.
    word-wrap: Sẽ làm cho những từ dài xuống hàng mà không làm vỡ layout.

### 15. Thuộc tính “opacity” được dùng làm gì?
Nó thể hiện như thuộc tính visibility và nó mờ dần từ 1-> 0 ( 1 -> 0.9 -> 0.8 …)

### 16. Điểm khác biệt giữa “width: auto” và “width: 100%” trong CSS?
- Auto sẽ đạt điểm độ rộng đầy đủ và sẽ trừ đi độ rộng của border, margin, padding,…
- 100% sẽ buộc thẻ đó bằng độ rộng của thẻ cha và tự động nới rộng ra them nếu có them các border, padding, margin,… điều đó sẽ gây ra một số vấn đề không mong muốn)

### 17. Thẻ “div” và thẻ “span” khác nhau thế nào?
- Thẻ “span” với thuộc tính “display: inline” và thẻ “div” với thuộc tính “display:block”.
- Chúng ta thường dùng thẻ “span” khi muốn các element nằm trên cùng 1 line.
- Không được đặt thẻ block vào trong thẻ inline được, nhưng ngược lại có thể đặt thẻ inline trong thẻ block.
```html
<div>
   <span>inline content</span>
</div>
```
Thẻ div có thể có một thẻ p và thẻ p có thể có 1 thẻ span.
```html
<span>
   <div>content</div>
</span>
```
Thẻ span không thể có thẻ div hoặc thẻ p ở bên trong.

### 18. Giải thích các giá trị của thuộc tính position: Fixed, Absolute, Relative, Static.


### 19. Làm cách nào để có có thứ hạng tốt hơn trong SEO bởi Search Engines (ví dụ Google)?


### 20. Mô tả các tính năng chính của HTML5?


### 21. Làm sao để làm nổi bật (highlight) text trong HTML?


### 22. Mô tả ngắn gọn cách sử dụng chính xác các phần tử ngữ nghĩa HTML5 sau: <header>, <article>, <section>, <footer>


### 23. Character Encoding là gì?


### 24. Thẻ tự đóng (self closing tag) là gì?


### 25. Sự khác biệt giữa "attribute" (thuộc tính) và "property" (đặc tính) trong HTML?


### 26. Khi nào thì thích hợp để sử dụng thẻ small?


### 27. Giải thích sự khác biệt giữa các phần tử <block> và các phần tử <inline> ?


### 28. Giải thích 3 mode trong html: almost standard, full standard và quirks?


### 29. Bạn đặt chế độ tương thích với IE như thế nào?


### 30. Có gì mới trong html5?


### 31. Bạn đã từng sử dụng ngôn ngữ nào khác HTML chưa?


### 32. Làm sao để thực hiện 1 nội dung bằng đa ngôn ngữ trong 1 website?


### 33. Làm thế nào để bạn thay đổi hướng của văn bản html?


### 34. Thẻ optional là gì?


### 35. Sự khác nhau giữa <section> và <div>?


### 36. Thuộc tính defer và async trên thẻ <script> là gì?


### 37. Mục đích của chặn bộ nhớ cache (Cache busting) là gì và làm thế nào bạn có thể thực hiện nó?


### 38. Một số khác biệt mà XHTML có so với HTML?


### 39. Web Workers là gì?


### 40. Thuộc tính rel="noopener" được sử dụng ở đâu và tại sao?


### 41. WebSQL là gì?


### 42. DOCTYPE làm gì?


### 43. DOM là gì?


### 44. Giải thích sự khác biệt giữa Cookie, Session Storage và Local Storage?


### 45. HTML5 Web Storage là gì? Giải thích sự khác nhau giữa localStorage và sessionStorage?


### 46. Một trang web có thể chứa nhiều thẻ <header> hay thẻ <footer> không?


### 47. Các thuộc tính "data-" có lợi cho việc gì?


### 48. WebSQL là gì?


### 49. Mục đích của thẻ <main> là gì?


### 50. Các khối xây dựng (building blocks) của HTML5 là gì?


### 51. Tại sao sử dụng thẻ ngữ nghĩa (semantic) HTML5?


### 52. HTML Preprocessor là gì và bạn có đang dùng chúng không?


### 53. Progressive rendering là gì?


### 54. Tại sao bạn sử dụng thuộc tính “srcset” trong thẻ <img>? Giải thích quy trình mà trình duyệt sử dụng khi đánh giá nội dung của thuộc tính này.


### 55. Bạn phải lưu ý những điều gì khi phát triển các trang web đa ngôn ngữ?


### 56. WebP là gì?


### 57. Bạn sẽ chọn sử dụng svg hay canvas cho trang web của mình?


### 58. Làm thế nào để tạo khoá công khai (public key) trong HTML?


### 59. IndexedDB là gì?


### 60. Accessibility và ARIA role có ý nghĩa gì trong một ứng dụng web?


### 61. Web Components là gì?








Tham khảo:
- [61 câu hỏi phỏng vấn Html/CSS](https://www.phongvanit.com/ky-nang/htmlcss-1007)
- [42 câu hỏi phỏng vấn Javascript](https://www.phongvanit.com/ky-nang/javascript-1000)

