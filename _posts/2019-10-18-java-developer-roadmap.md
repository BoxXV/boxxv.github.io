---
layout: post
title: Lộ trình học Java Web
subtitle: Vì một tương lai lương Java cao ngất
tags:
- Java
- Interview
---
Thấy khá nhiều bạn sinh viên mới ra trường hiện nay khá mù mờ về con đường học, vẫn mãi lẹt đẹt học nhỏ giọt, thiếu chọn lọc và hiệu quả. Với kinh nghiệm éo có nhiều (nên nghe thì nghe, ko nghe thì cũng không ảnh hưởng đến hòa bình thế giới ạ), theo mình thì Java Web Developer Starter pack nên như sau:

![Java Developer Roadmap](https://boxxv.github.io/img/posts/java-developer-roadmap.png "Java Developer Roadmap")_Java Developer Roadmap_

## 1. Java Core, OOP.
Java core gồm những gì? Các bạn cứ vô trang này check cho ngắn gọn. Cái này dành cho bạn nào chưa biết làm hoặc còn gà Java. Tất cả hoàn toàn là cơ bản, advance hơn tý thì có thể kể đến một số mẹo tăng Perfomance, sử dụng nhuần nhuyễn các loại Collection, khi nào dùng List, khi nào dùng Set, perfomance nó khác nhau ntn,... Mình đi phỏng vấn nhiều, thực sự người nắm tốt Java Core chỉ đếm trên đầu ngón tay(tay trái thôi đấy). Các bạn quá lười học, đâm đầu vào làm dự án mà không chịu học hỏi thêm. Không nói cái gì xa xôi, chính những thứ các bạn đó làm hằng ngày, nhưng do không chịu tìm hiểu, dẫn đến vận dụng sai lầm. Không biết đến Set thì khi cần một list không trùng lặp phải làm như thế nào? Không biết final class/method thì sao có thể code OOP tốt được? Không biết synchronized hay Immutable class thì code multi-thread sẽ ra sao. Đừng nói các bạn không dùng, chẳng qua các bạn không biết mà dùng thôi! Java core không khó, cứ code nhiều, ĐỌC SÁCH và học hỏi là lên trình, ko vấn đề.

## 2. Design Patterns(DP), Refactoring, các biện pháp clean code khác.
Nếu thuần thục được sẽ là điểm cộng cực lớn khi xin việc. Có thể chỉ cần thuần thục một số patterns: khi nào sử dụng, điểm mạnh, điểm yếu,... Đặc biệt chú ý là code theo cái này phải dụng não rất nhiều, ai ko có thói quen dùng thì ko nên. Refactoring hay clean code cũng khá là quan trọng. Đôi khi review code, nhìn vào là biết trình của dev. Nhưng chú ý là cái này ko có chuẩn chung như DP nên ko mang đi khè nhau khi phỏng vấn được. Để tập code clean, các bạn nên tập sử dụng các tool như SonarLint, SonarQube,... Tham khảo thêm sách và trên trang sourcemaking.com

## 3. JSP/Servlet, sau đó là Struts2, Spring, Hibernate....
Nhiều bạn mới ra trường hay nhảy sang học luôn những thứ cao siêu như Struts2, Spring MVC, JSF, chủ yếu phục vụ nhu cầu "mì ăn liền" của các cty. Điều này là hoàn toàn sai. Mình là người cực kỳ quan trọng việc học những cái căn bản. Nếu không hiểu JavaEE, JSP/Servlet, các bạn chỉ biết được bề nổi của các framework kia, bên trong xử lý như thế nào, request response được xử lý ra sao không hề hiểu. Ngoài ra, các bạn đừng đú theo phong trào nào đó nhảy vào học một số Framework thần thánh(theo QC) như Play, ZK, GWT,.... sau khi hiểu một chút về JavaEE, nên chuyển qua học cái các cty dùng nhiều như Struts2, Spring(Spring Boot, Spring MVC) hay JSF, đi phỏng vấn người ta còn có cái để hỏi.

## 4. Database.
Nhu cầu sử dụng Oracle db với Java Web chắc khỏi bàn. Mình code vài dự án rồi và chưa có dự án nào dùng db nào khác Oracle. Oracle thì có quá nhiều thứ để học: sequence, index, partitioning, PL/SQL,.... Càng biết nhiều điểm càng cao, không bao giờ sợ thừa. Đừng học kiểu chỉ ngồi viết vài ba câu SQL và viết vô CV vỗ ngực bảo "thành thạo Oracle DB", thực sự rất khó đấy. Ban đầu cố gắng viết SQL, PL/SQL; design database để hiểu hơn về các datatype và các thành phần quan trọng của table và schema trong Oracle. Ngoài Oracle thì MySQL, Postgresql cũng được sử dụng khá nhiều trong Java.

## 5. Javascript THUẦN sau đó mới đến Jquery, Angular, VueJs,...
JS có quá nhiều thứ phải học. Mình thấy hiện nay nhiều bạn, ngay cả đi làm nhiều năm nhưng về js cũng chỉ biết quanh quẩn dưới mức basic, có thể mấy người đó dùng JQuery thuần thục vãi ra, nhưng basic ko có, ko hiểu được Jquery nên nhiều khi vận dụng sai. Đặc biệt về DOM, Event, mình thấy ít người tìm hiểu.

## 6. CSS, Bootstrap
CSS thường ko phải là điểm cộng. Bootstrap cũng chỉ là optional. CSS thì lượn một vòng sách nào đó hoặc mần site nào đó là ra hết, không cần học quá cao siêu, cao siêu là cho Designer. Mình code nhiều năm nhưng trình CSS vẫn rất gà, không vấn đề gì.

## 7. Teamwork
Cách sử dụng Version Control Software(git, svn,...). Cách giao tiếp trong công việc, giao tiếp với dev, test, pm,... Cách xử lý xung đột trong công việc. Mình đã gặp một số người, kiểu "sinh ra đã bị cả team ghét", thở ra câu nào là bị cả team "bĩu môi", "đá đểu", dù đã nhiều năm kinh nghiệm. Teamwork là một yếu tốt cực kỳ quan trọng để đánh giá khả năng làm việc của một người. Nếu bạn chưa biết một teamwork tốt là ra sao, hãy lắng nghe, hãy có thái độ cầu thị, hãy hòa nhập với mọi người. Đừng bao giờ nghĩ "chỉ mình em làm cái này, các anh không biết gì đâu!", luôn tự cho mình là đúng chính là đi ngược lại teamwork.

## Kết luận
Muốn giỏi, phải liên tục trau dồi, luyện tập ở cty và ở nhà, chăm chỉ đọc sách hoặc các site đánh giá, phân tích chuyên sâu về các kỹ thuật lập trình,... nếu kiến thức bạn chỉ lẩn quẩn như mấy cái trang mức basic như tutorialspoint là chưa đủ. Mỗi khi học cái mới, mình cũng hay vào những trang đó để quan sát những cái nhìn ban đầu, sau đó mình thường tìm ebook trên mạng, tìm một loạt các bài viết phân tích về đọc, cuối cùng là thử làm một project nào đó, vừa làm vừa giải quyết vấn đề. Nói hươu nói vượn gì thì thành hay bại vẫn là ở chính các bạn. Đọc thật nhiều và code thật nhiều, đó chính là bí quyết


Tham khảo:
- [Luồng học cho Java web developer](https://luanvv.com/blog/luong-hoc-java-web/)
- [Java Developer Roadmap](https://github.com/s4kibs4mi/java-developer-roadmap)
- [The 2021 Java Developer RoadMap [UPDATED]](https://javarevisited.blogspot.com/2019/10/the-java-developer-roadmap.html)
- [Java Developer Road Map 2021 - How to Become a Java Developer](https://youtu.be/vK_-vld-tS4)
