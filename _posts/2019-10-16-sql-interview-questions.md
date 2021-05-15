---
layout: post
title: Tổng hợp những câu hỏi phỏng vấn SQL
subtitle: Vì một tương lai lương cao ngất
tags:
- SQL
- Interview
- Questions
- Answers
---
Trong bài viết này, tôi sẽ tổng hợp lại những kiến thức về SQL, mà có thể các bạn sẽ được hỏi khi đi phỏng vấn.

## 50 câu hỏi phỏng vấn về SQL thường gặp

Ngôn ngữ truy vấn SQL luôn là một kiến thức quan trọng đối với các lập trình viên, tester, BA hay QA,… Vì thế các nhà tuyển dụng luôn mong muốn nhân sự của mình có hiểu biết rõ ràng về lĩnh vực này. Qua nhiều khảo sát, dưới đây sẽ là tổng hợp 50 câu hỏi phỏng vấn thường gặp dành cho các ứng viên khi ứng tuyển vào các vị trí như trên.

#### 1. SQL là gì?
Viết tắt của Structured Query Language – ngôn ngữ truy vấn cấu trúc. Nó được thiết kế để quản lý dữ liệu trong một hệ thống quản lý cơ sở dữ liệu quan hệ (RDBMS - Relational Database Management System). SQL là ngôn ngữ cơ sở dữ liệu, được dùng để tạo, xóa, lấy các hàng và sửa đổi các hàng.

Tham khảo thêm: SQL là gì? Công việc của SQL Developer?

#### 2. Câu lệnh để chọn tất cả bản ghi từ table?
Cú pháp: `Select * from table_name`

#### 3. Định nghĩa JOIN và các loại JOIN

Từ khóa JOIN được dùng để nạp dữ liệu từ 2 hay nhiều bảng liên quan. Sử dụng từ khóa JOIN khi cần truy vấn các cột dữ liệu từ nhiều bảng khác nhau để trả về trong cùng một tập kết quả.

Các loại JOIN:
    INNER JOIN
    LEFT OUTER JOIN
    RIGHT OUTER JOIN
    FULL OUTER JOIN
    CROSS JOIN
    SELF JOIN

#### 4. Cú pháp để thêm bản ghi vào 1 bảng là gì?
Sử dụng cú pháp INSERT để thêm bản ghi vào 1 bảng

Ví dụ: `INSERT` into table_name `VALUES` (value1, value2,…)

#### 5. Làm thế nào để bạn thêm 1 cột vào 1 bảng?
Để thêm một cột khác vào bảng, sử dụng cú pháp:

`ALTER TABLE` table_name `ADD` (column_name)

#### 6. Xác định câu lệnh Delete SQL
Câu lệnh này được sử dụng để xóa hàng hoặc các hàng từ một bảng dựa trên điều kiện được chỉ định.

Cú pháp:

`DELETE FROM` table_name<br>`WHERE`<Condition>

#### 7. Xác định COMMIT
COMMIT lưu lại tất cả các thay đổi được thực hiện bởi các câu lệnh DML. DML cho phép thực hiện các truy vấn, bao gồm cú pháp để cập nhật, sửa đổi, chèn thêm và xóa các mẫu tin.

#### 8. Khóa chính (PRIMARY KEY) là gì?
Khóa chính là cột có các giá trị xác định `duy nhất` mỗi hàng trong một bảng. Giá trị khóa chính không bao giờ được sử dụng lại.

Một cột là PRIMARY KEY thì không được phép có giá trị NULL. Mỗi bảng chỉ cho phép tối đa một PRIMARY KEY. Mỗi bảng đều cần có khóa chính

#### 9. Khóa ngoại (FOREIGN KEY) là gì?
Khi một trường khóa chính của một bảng được thêm vào các bảng có liên quan để tạo ra trường phổ biến có liên quan đến 2 bảng, nó được gọi là khóa ngoại trong các bảng khác. Các ràng buộc khóa ngoại thực thi toàn vẹn tham chiếu.

#### 10. CHECK Constraint – Ràng buộc CHECK là gì?
Một ràng buộc CHECK được sử dụng để giới hạn các giá trị hoặc loại dữ liệu có thể được lưu trữ trong một cột. Nếu bản ghi không đáp ứng được điều kiện này, thì sẽ không được lưu trữ vào trong bảng.

#### 11. Một bảng có thể có nhiều hơn một khóa ngoại không?
Một bảng có thể có nhiều hơn một khóa ngoại nhưng chỉ có một khóa chính.

#### 12. Trường dữ liệu BOOLEAN có giá trị nào?
Đối với trường dữ liệu BOOLEAN, có 2 giá trị: -1 (TRUE) và 0 (FALSE)

#### 13. Thủ tục lưu trữ (stored procedure) là gì?
Một thủ tục lưu trữ là một tập hợp các truy vấn SQL có thể lấy đầu vào và gửi lại đầu ra.

#### 14. IDENTITY trong SQL là gì?
Một cột IDENTITY trong SQL sẽ tự động sinh ra các giá trị số tự tăng. Có thể định nghĩa giá trị bắt đầu và gia tăng của cột nhận dạng.

#### 15. NOMALIZATION – Chuẩn hóa là gì?
Quá trình thiết kế bảng để giảm thiểu sự thừa số liệu được gọi là chuẩn hóa. Chúng ta cần chia một cơ sở dữ liệu thành hai hay nhiều bảng và xác định các mối quan hệ giữa chúng.

#### 16. Trigger là gì?
Trigger là một thủ tục được thực thi từ phía máy chủ cơ sở dữ liệu khi một sự kiện bảng xảy ra (chèn, cập nhật, xóa lệnh thực hiện đối với một bảng cụ thể).

#### 17. Làm thế nào để lấy ra các hàng ngẫu nhiên từ một bảng?
Sử dụng câu lệnh SAMPLE chúng ta có thể chọn các hàng ngẫu nhiên. Ví dụ:

`SELECT*FROM` table_name `SAMPLE(10)`

#### 18. Cổng TCP/IP nào mà SQL server chạy?
Mặc định SQL Server chạy trên cổng 1433

#### 19. Viết một truy vấn SELECT SQL để trả về mỗi bản ghi chỉ một lần từ một bảng?
Để có được mỗi tên một lần duy nhất, chúng ta cần phải sử dụng từ khóa DISTINCT. Cú pháp: 

SELECT DISTINCT name FROM table_name

#### 20. DML và DDL là gì?
DML là viết tắt của Ngôn ngữ thao tác dữ liệu (Data Manipulation Language): INSERT, UPDATE và DELETE là các câu lệnh DML.

DDL là viết tắt của Ngôn ngữ định nghĩa dữ liệu (Data Definition Language): CREATE, ALTER, DROP, RENAME là các câu lệnh DDL.

#### 21. Lệnh nào để đổi tên một cột trong đầu ra của truy vấn SQL?
Sử dụng cú pháp: `SELECT` column_name `AS` new_name `FROM` table_name;

#### 22. Thứ tự của SQL SELECT?
Thứ tự các mệnh đề SQL SELECT là: SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY. Trong đó SELECT, FROM là bắt buộc.

#### 23. Giả sử một cột Student có 2 cột, Name và Marks. Làm thế nào để có được điểm của 3 sinh viên top đầu?
Câu lệnh: `SELECT` Name, Marks `FROM` Student s1 where 3 <= (`SELECT COUNT(*) FROM` Student s1.marks = s2.marks)

#### 24. SQL comments là gì?
Khi muốn thêm chú thích vào truy vấn SQL để rõ ràng, chi tiết hơn, người ta sử dụng SQL comment. SQL comment có thể được đặt bởi 2 dấu nối liên tiếp (-) hoặc /*….*/.

Khi câu truy vấn được thực hiện thì trình biên dịch sẽ tự động bỏ qua những dòng có comment.

#### 25. Sự khác biệt giữa các lệnh TRUNCATE, DELETE và DROP?
    DELETE: xóa một hoặc tất cả các hàng từ một bảng dựa trên điều kiện và có thể phục hồi
    TRUNCATE: xóa tất cả các hàng từ một bảng bằng cách phân bổ các trang bộ nhớ và không thể phục hồi
    DROP: xóa hoàn toàn một bảng từ cơ sở dữ liệu

#### 26. Các thuộc tính của một giao dịch là gì?
Các thuộc tính này được gọi là ACID, bao gồm:

    Tính nguyên tử (Atomicity)
    Tính nhất quán (Consistency)
    Cô lập (Isolation)
    Độ bền (Durability)

#### 27. ROWID nghĩa là gì?
Đó là một cột giả dài 18 ký tự gắn liền với mỗi hàng của một bảng.

#### 28. Xác định UNION, MINUS, UNION ALL, INTERSECT?
MINUS được sử dụng để kết hợp 2 câu lệnh SELECT, nó trả về tất cả các bản ghi chỉ thuộc bảng của câu truy vấn SELECT đầu tiên, những bản ghi giao nhau hoặc thuộc câu truy vấn SELECT thứ 2 không được lấy vào kết quả.

UNION được dùng khi viết nhiều truy vấn SELECT khác nhau nhưng để trả về một danh sách kết quả duy nhất

UNION ALL cho kết quả trả về tất cả các hàng được chọn bởi một trong hai truy vấn, giữ lại các kết quả trùng.

INTERSECT cho kết quả là những bản ghi đều có trong cả 2 bảng.

#### 29. Giao dịch (transaction) là gì?
Mỗi giao dịch là một dãy mã chạy trên cơ sở dữ liệu.

#### 30. Sự khác nhau giữa UNIQUE và PRIMARY KEY constraints là gì?
Một chỉ có thể có 1 PRIMARY KEY nhưng có thể không có hoặc có nhiều UNIQUE KEY.

PRIMARY KEY không thể chứa giá trị NULL, UNIQUE thì có thể có giá trị NULL

#### 31. Khóa tổng hợp (Composite primary key) là gì?
Khóa chính được tạo trên nhiều cột được gọi là khóa chính tổng hợp.

#### 32. Index là gì?
Index (Chỉ mục) là bảng tra cứu đặc biệt mà Database Search Engine có thể sử dụng để giảm thời gian và tăng hiệu suất thực hiện các truy vấn. Index có thể được tạo trên một hoặc nhiều cột của một bảng.

#### 33. Subquery là gì?
Truy vấn con (còn được gọi là truy vấn phụ hay truy vấn lồng nhau) là một truy vấn bên trong truy vấn SQL khác và được nhúng bên trong mệnh đề WHERE.

#### 35. Tối ưu hóa truy vấn là gì?
Là một quá trình, trong đó hệ thống cơ sở dữ liệu so sánh các chiến lược truy vấn khác nhau và chọn truy vấn với chi phí thấp nhất.

#### 36. Collation là gì?
Bộ quy tắc định nghĩa cách dữ liệu được lưu trữ, cách phân biệt chữ hoa, chữ thường và ký tự Kana có thể được xử lý như thế nào.

#### 37. Tính toàn vẹn tham chiếu là gì?
Tập các quy tắc hạn chế giá trị của một hoặc nhiều cột của các bảng dựa trên các giá trị của khóa chính hoặc khóa duy nhất của bảng tham chiếu.

#### 38. Hàm Case là gì?
Trường hợp tạo logic kiểu if-then-else trong SQL. Nó đánh giá một danh sách có điều kiện và trả về một trong nhiều biểu thức kết quả tốt.

#### 39. Xác định một bảng tạm thời?
Một bảng tạm thời là một cấu trúc lưu trữ tạm thời để lưu trữ dữ liệu

#### 40. Làm thế nào chúng ta có thể tránh trùng lặp hồ sơ trong một truy vấn?
Sử dụng từ khóa INSTINCT thì việc sao chép hồ sơ trong một truy vấn có thể tránh được.

#### 41. Giải thích sự khac nhau giữa đổi tên (Rename) và Bí danh (Alias)?
Đổi tên là một tên thường xuyên cho một bảng hoặc cột. Bí danh là tên tạm thời cho một bảng hoặc cột.

#### 42. View là gì?
Một khung nhìn là một bảng ảo chứa dữ liệu từ một hoặc nhiều bảng. Lượt xem hạn chế quyền truy cập dữ liệu của bảng bằng cách chỉ chọn các giá trị được yêu cầu và thực hiện các truy vấn phức tạp.

Chế độ xem (view) không có chứa dữ liệu vì View là một cấu trúc ảo.

#### 43. Lợi ích của View
Chế độ xem hạn chế quyền truy cập vào dữ liệu vì có thể hiển thị các cột được chọn từ bảng

Có thể sử dụng chế độ xem để truy vấn các kết quả tìm kiếm phức tạp.

#### 44. Liệt kê các đặc quyền khác nhau mà người dùng có thể cấp cho người dùng khác
Đó là SELECT, CONNECT, RESOURCES

#### 45. Schema là gì?
Biểu đồ là tập hợp các đối tượng cơ sở dữ liệu của người dùng

#### 46. Bảng là gì?
Một bảng là đơn vị cơ bản của lưu trữ dữ liệu trong hệ thống quản lý cơ sở dữ liệu. Dữ liệu bảng được lưu trữ trong hàng và cột.

#### 47. Chế độ xem có thể dựa trên một chế độ xem khác không?
Chế độ xem dựa trên một chế độ xem khác

#### 48. Sự khác nhau giữa mệnh đề Having và mệnh đề Where?
Cả hai mệnh đề đều chỉ định điều kiện tìm kiếm nhưng mệnh đề Having chỉ được sử dụng với câu lệnh SELECT và thường được sử dụng với mệnh đề GROUP BY. Nếu không có mệnh đề GROUP BY thì Having sử dụng giống mệnh đề WHERE.

#### 49. Sự khác nhau giữa bảng tạm cục bộ (Local) và bảng tạm toàn cầu (Global) là gì?
Một bảng tạm cục bộ tồn tại trong một kết nối. Khi kết thúc kết nối thì bảng tạm này tự động được xóa. Tên của bảng tạm Local được bắt đầu bằng ký tự #

Một bảng tạm toàn cầu tồn tại vĩnh viễn trong db nhưng các hàng của nó biến mất khi kết nối đóng lại. Tên bảng tạm Global được bắt đầu bằng ##

#### 50. CTE là gì?
Biểu thức bảng CTE (Common Table Expression) hoặc bảng chung là một biểu thức có chứa tập kết quả tạm thời được định nghĩa trong câu lệnh SQL.
Để hiểu rõ hơn và có được những kiến thức nền tảng về SQL và phân tích dữ liệu. Bạn có thể tham gia khóa học phân tích dữ liệu với SQL và Google data studio do BAC tổ chức. Khóa học được xây dựng trên kiến thức nền tảng, ví dụ thực tế trực quan, kinh nghiệm thực tế của giảng viên. Sau khóa học, học viên sẽ áp dụng được những kiến thức đã học vào quá trình phỏng vấn và áp dụng công việc. 


Tham khảo:
- [50 câu hỏi phỏng vấn về SQL thường gặp](https://www.bacs.vn/vi/blog/kien-thuc/50-cau-hoi-phong-van-ve-sql-thuong-gap-8778.html)
- [SQL Interview Questions](https://www.interviewbit.com/sql-interview-questions/)
- [Top 50 SQL Interview Questions and Answers (2021 Update)](https://www.guru99.com/sql-interview-questions-answers.html)
- [Top 65 SQL Interview Questions You Must Prepare In 2021](https://www.edureka.co/blog/interview-questions/sql-interview-questions)

