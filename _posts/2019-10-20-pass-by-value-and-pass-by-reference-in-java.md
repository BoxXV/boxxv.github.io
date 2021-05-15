---
layout: post
title: Pass by Value và Pass by Reference trong Java
subtitle: Vì một tương lai lương Java cao ngất
tags:
- Java
- Interview
---

Hôm trước có bắt gặp cuộc tranh luận nảy lửa trên một group Skype về Java Developer. Nội dung tranh luận xoay quanh việc Java có `pass-by-reference` hay không.

Trước khi trả lời câu hỏi này, chúng ta cần hiểu sự khác biệt giữa `pass-by-value` (tham trị) và `pass-by-reference` (tham chiếu)


## Pass-by-value

`Pass-by-value` được hiểu là khi bạn pass biến vào làm argument cho một function, chương trình sẽ không dùng thẳng biến đó mà sao chép giá trị và đưa cho function, và hệ quả là dù bên trong function xảy ra chuyện gì thì biến thực tế vẫn được bảo toàn

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_gZpx1_-g6SNPmtjET0eHSQ.webp "Pass by Value và Pass by Reference trong Java")

Kết quả
![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_e0gq4JkM8xtF3vtKWm07EQ.webp "Pass by Value và Pass by Reference trong Java")


## Pass-by-reference

Ngược lại với `Pass-by-value`, khi bạn pass biến vào làm argument cho một function, chương trình sẽ đưa thẳng biến đó cho function tùy ý xử lý, và hệ quả là nếu bên trong function mà thay đổi giá trị của argument thì biến thực tế bên ngoài cũng bị thay đổi, vì trong trường hợp này biến bên ngoài và biến (argument) của function là một.

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_xw5E42tHZ_wzhsZ8m_2Owg.webp "Pass by Value và Pass by Reference trong Java")

Kết quả
![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_KMbGr6fotJljgvozD0tEQw.webp "Pass by Value và Pass by Reference trong Java")

Có thể xem hình minh họa bên dưới để hiểu rõ hơn
![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/0_q5Tkq9ctyYd0gd1F.gif "Pass by Value và Pass by Reference trong Java")

Vậy phần xử lý phía sau (behind the scenes) giữa Pass-by-value và Pass-by-reference thì ra sao. Để giải thích cho phần này, tôi tạm dùng cách C/C++ làm việc để diễn tả.

Dưới đây là mô hình hóa việc lưu trữ dữ liệu của các biến trên bộ nhớ. Ở đây ta có biến `myAge` có giá trị `14` được lưu ở bộ nhớ có địa chỉ `106`

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/0_qCyny98PQOQRdKiw.webp "Pass by Value và Pass by Reference trong Java")

Khi `Pass-by-value`, chương trình không pass thẳng biến myAge ở ô 106, mà nó sẽ sao chép giá trị (`14`) của ô `106` sang ô `152`, và function `calculateBirthYear` sẽ chỉnh sửa ô nhớ `152`, và ô `106` sẽ luôn được an toàn khỏi bàn tay của function `calculateBirthYear`.

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_CzGFzVyvkG7aqtHG_EOjOg.webp "Pass by Value và Pass by Reference trong Java")

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_yjz-HH8BeMBdqMCwHOP2XA.webp "Pass by Value và Pass by Reference trong Java")

Nhưng khi `Pass-by-reference`, chương trình sẽ truyền thẳng địa chỉ ô nhớ vào function, bạn sẽ phải có kiến thức về Pointer trong C/C++ để hiểu cú pháp

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_3qB64nCUhml-zw53Smntgw.webp "Pass by Value và Pass by Reference trong Java")

Kiến thức về `Pass-by-value` và `Pass-by-reference` là kiến thức chung, không riêng ngôn ngữ nào, nhưng ở đây tôi chọn C/C++ vì các thuật ngữ của nó dễ hiểu nhất, không gây nhầm lẫn cho người đọc. Với các ngôn ngữ bậc cao như Python, Java, C#,… thì khái niệm Pointer không còn, nhưng `Pass-y-reference` vẫn được một số ngôn ngữ thể hiện ở mức đơn giản và đỡ hack não hơn Pointer.

Dưới đây là ví dụ trong C# với từ khóa `ref` để `Pass-by-reference`

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_-BOPimXU_UopYjl50-vRow.webp "Pass by Value và Pass by Reference trong Java")


## Vậy với Java thì sao?

Theo một cách hiểu nhất định và là cách hiểu mà đa phần đồng ý, thì Java không có `Pass-by-reference !`

Đâu đó các bạn sẽ đọc được những bài như https://viettuts.vn/java/truyen-gia-tri-va-tham-chieu-pass-value-va-pass-reference-trong-java, họ cho rằng khi bạn truyền giá trị kiểu Primitive vào function thì nó sẽ là Pass-by-value và khi truyền giá trị kiểu Reference thì nó sẽ là Pass-by-reference.

Để hiểu hơn sự khác nhau giữa Primitive Type và Reference Type, các bạn có thể đọc ở link sau https://javarevisited.blogspot.com/2015/09/difference-between-primitive-and-reference-variable-java.html

Vế thứ nhất, khi bạn truyền giá trị kiểu Primitive vào function thì nó sẽ là Pass-by-value thì không có gì bàn cãi, Java không có pointer như C/C++, cũng chẳng có `ref` như C#, vậy nên bạn không thể `Pass-by-reference` với Primitive type.

Nhưng vế thứ hai, khi truyền giá trị kiểu Reference thì nó sẽ là `Pass-by-reference` có đúng hay không, nó còn tùy thuộc cách hiểu của các bạn về từ `Reference` trong `Reference` type với từ `Reference` trong `Pass-by-reference`, nếu bạn cho rằng 2 từ là một, OK, you WIN, thì đúng là bạn đang pass “Reference” mà.

Nhưng nếu so sánh với C/C++ hay C# ở trên, nó thực sự có khác biệt.


## Chuyện gì xảy ra khi bạn pass một Reference Type vào một function?

Trước tiên, bạn cần hiểu reference(không phải Reference Type) trong Java.

Ví dụ ta khai báo biến `f`, có type là Foo như sau

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_KpbpKPXBYZLHSPHXS_qcFQ.webp "Pass by Value và Pass by Reference trong Java")

Đoạn trên có thể giải thích như sau:

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_FGK0ujspvCiX4kDs8F9flQ.webp "Pass by Value và Pass by Reference trong Java")

Biến `f` mà chúng ta luôn nghĩ là đối tượng thực trong bộ nhớ thực ra không phải, nó chỉ là tham chiếu đến đối tượng ở bên trong ô nhớ.

Và trên thực tế là khi bạn pass một Reference Type vào một function, ta ví dụ là ta truyền f vào thì chương trình sẽ tạo ra một reference khác (tạm gọi là `a`)và link nó đến cùng đối tượng mà `f` trỏ vào, hay nói cách khác, nó copy reference `f`

Ví dụ ta có hàm

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_pfblaAFQQzQ-xdZ0BVlzuA.webp "Pass by Value và Pass by Reference trong Java")

thì có thể được hiểu là

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_yk_S4f2BzZhjEZ5yyQgMHw.webp "Pass by Value và Pass by Reference trong Java")

lúc này sẽ có 2 reference `a` và `f` cùng trỏ đến một object, khi ta thay đổi bất kỳ reference nào thì object cũng được thay đổi theo

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/0_Gxe_biEDnue3p8V0.webp "Pass by Value và Pass by Reference trong Java")

và khi function `modifyReference` chạy xong

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_GiGaLyDTz3_MnwByNfkKpw.webp "Pass by Value và Pass by Reference trong Java")

reference `a` (clone từ `f`) tạm coi là biến mất do đã ra ngoài function, lúc này chỉ còn `f` và đối tượng Foo đã được thay đổi

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_3GZz2MqGquGf4Lp1zPKJxA.webp "Pass by Value và Pass by Reference trong Java")

Nghe có vẻ giống `Pass-by-reference`, nhưng sự thật là không. Phương pháp này của Java không phải `Pass-by-reference`, nó nên được hiểu là `Pass-by-value` reference, chương trình không thực sự pass chính xác reference `f` vào function `modifyReference`, mà chương trình chỉ pass cái clone của nó(reference `a`) vào mà thôi. Giờ thì nghe giống `Pass-by-value` chưa!

Để dễ hình dung, ta có ví dụ sau:

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_WQfe7G4OpO19AgMofjf2XA.webp "Pass by Value và Pass by Reference trong Java")

Trước tiên, khi pass `f` vào `changeReference`, ta vẫn được kết quả như trên đã mô tả, chương trình sẽ clone reference `f` ra một reference khác và tất nhiên là cùng trỏ đến đối tượng Foo của `f`

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1__s873yVnTlttWGEQ1xNDaQ.webp "Pass by Value và Pass by Reference trong Java")

Nhưng, Java không làm việc như vậy, khi bạn sẩy chân gán lại reference `a` sang một đối tượng Foo khác, bạn sẽ không thể nào quay đầu được.

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_mokO7hm-OBN6LBg7i8b_IA.webp "Pass by Value và Pass by Reference trong Java")

khi thay đổi `a`, đổi attribute từ “b” sang “c”

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_G3StemGqY2y41sCwMU7f8w.webp "Pass by Value và Pass by Reference trong Java")

Vấn đề trên tưởng như đơn giản nhưng rất nhiều người không biết và vẫn “ngã ngựa”

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_18FR4EFkumI_DQKuK8LxCA.webp "Pass by Value và Pass by Reference trong Java")

Đó cũng là lý do vì sao các linter trong các ngôn ngữ như Java, Python, Javascript,… đều warning mỗi khi bạn gán lại argument của function và việc thay đổi attribute của đối tượng bên trong function cũng là cực kỳ nên tránh

Nên tránh

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_zdheUcSsqR8ASerhdp6B5A.webp "Pass by Value và Pass by Reference trong Java")

Thay vào đó nên tạo ra một list mới và tránh thay đổi list cũ

![Pass by Value và Pass by Reference trong Java](https://boxxv.github.io/img/posts/1_7Lrhfw4Hlz5cEZLmC6JW6g.webp "Pass by Value và Pass by Reference trong Java")


## Kết luận

Có thể bạn nghĩ rằng khi đổi attribute của reference thì đối tượng thực tế cũng đổi, nó chính là `Pass-by-reference`, vậy Java có nó. Thật ra điều đó không quan trọng. Java có `Pass-by-reference` hay không? Câu này đối với dev, nó cũng vô nghĩa như câu Java có phải ngôn ngữ thuần hướng đối tượng(purely Object-Oriented Language) hay không! Vì khái niệm vẫn chỉ là khái niệm, học thuộc khái niệm không giúp bạn code tốt hơn, hãy hiểu bản chất, hiểu cú pháp hơn là tranh cãi mấy điều vô bổ.



Reference:
- [Passing by Value vs. by Reference Visual Explanation](https://blog.penjee.com/passing-by-value-vs-by-reference-java-graphical/)
- [Pass by Value và Pass by Reference trong Java](https://luanvv.com/blog/pass-by-value-va-pass-by-reference-trong-java/)
- [Does Java pass by reference or pass by value?](https://www.infoworld.com/article/3512039/does-java-pass-by-reference-or-pass-by-value.html)
