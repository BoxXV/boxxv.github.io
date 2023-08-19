---
layout: post
title: Tổng hợp những câu hỏi phỏng vấn Java
subtitle: Vì một tương lai lương Java cao ngất
tags:
- Java
- Interview
- Questions
- Answers
---
Trong bài viết này, tôi sẽ tổng hợp lại những kiến thức về Spring Framework, mà có thể các bạn sẽ được hỏi khi đi phỏng vấn. Những chủ đề thường được hỏi sẽ về các vấn đề chính như sau.
- Spring overview
- Dependency Injection
- Spring Beans
- Spring Annotations
- Spring Data Access
- Aspect Oriented Programming (AOP)
- Spring MVC

## 69 câu hỏi phỏng vấn về Spring
#### Spring overview
1. Spring là gì?
2. Lợi ích mà Spring framework mang lại
3. Các module của Spring framework
4. Core container
5. BeanFactory
6. XmlBeanFactory
7. AOP module
8. JDBC abstraction và DAO module
9. Object relational mapping (ORM) module
10. Web module
11. Spring MVC module
12. Spring configuration file
13. Spring IoC container
14. Lợi ích của IoC
15. Implement Application context phổ biến
16. Điểm khác nhau giữa BeanFactory và Application context
17. Cấu trúc của Spring application
#### Dependency Injection
18. Dependency Injection trong Spring
19. Những kiểu khác nhau của IoC
20. Nên sử dụng Constructor-based hay setter-based DI
#### Spring Beans
21. Spring beans là gì?
22. Định nghĩa Spring bean gồm những gì?
23. Làm sao để cung cấp configuration metadata cho Spring Container?
24. Làm sao để định nghĩa scope của bean?
25. Các scope của bean
26. Singleton Bean có Thread safe trong Spring Framework?
27. Bean lifecycle trong Spring framework
28. Phương thức nào là quan trọng nhất trong Spring Bean lifecycle
29. Inner bean trong Spring
30. Làm sao để inject Java Collection trong Spring?
31. Bean wiring là gì?
32. Bean auto wiring là gì?
33. Các mode auto wiring
34. Hạn chế của autowiring
35. Có thể inject null hoặc empty String trong Spring hay không?
#### Spring Annotations
36. Java-based configuration
37. Annotation-based configuration
38. Làm sao cài đặt autowiring?
39. @Required annotation
40. @Autowired annotation
41. @Qualifier annotation
#### Spring Data Access
42. Sử dụng JDBC hiệu quả trong Spring framework
43. JdbcTemplate
44. Spring DAO support
45. Sử dụng Hibernate trong Spring
46. Spring hỗ trợ những ORM nào?
47. Tích hợp Hibernate với Spring sử dụng HibernateDAOSupport
48. Spring hỗ trợ những kiểu quản lý transaction nào?
49. Lợi ích của việc quản lý transaction bằng Spring Framework
50. Nên sử dụng kiểu quản lý transaction như thế nào?
#### Spring Aspect Oriented Programming (AOP)
51. AOP
52. Khía cạnh (Aspect)
53. Sự khác nhau giữa concern và cross-cutting concern trong Spring AOP
54. Join point
55. Advice
56. Pointcut
57. Introduction là gì?
58. Target object là gì?
59. Proxy là gì?
60. Các loại AutoProxying
61. Weaving là gì? 
62. XML Schema-based aspect implementation
63. Annotation-based (@AspectJ based) aspect implementation
#### Spring Model View Controller (MVC)
64. Spring MVC framework là gì?
65. DispatcherServlet
66. WebApplicationContext
67. Controller trong Spring MVC framework là cái gì?
68. @Controller annotation
69. @RequestMapping annotation


## Tổng hợp câu hỏi phỏng vấn JAVA
1. Lập trình hướng đối tượng là gì 
2. Các tính chất của lập trình hướng đối tượng trong Java?
3. Các kiểu dữ liệu nguyên thủy
4. Autoboxing và Unboxing trong Java là gì?
5. Phân biệt List và ArrayList?
6. Sự khác nhau giữa Array và ArrayList? 

Sự khác nhau cơ bản giữa SOAP và RESTful ?

- Liệt kê, giải thích 4 tính chất OOP
- MVVM, MVP, MVC là gì, khi nào dùng cái nào
- Singleton dùng để làm gì
- Khi nào dùng Interface hoặc Abstract Class
- Immutable và mutable là gì
- Tại sao Class String trong Java lại immutable
- Daemon Thread là gì
- Android Garbage collection hoạt động ntn
- Khi nào 1 object sẵn sàng for Garbage collection hốt
- StringBuilder vs String
- StringBuilder vs StringBuffer
- Liệt kê những trường hợp mà finally ko đc gọi
- Java dùng pass-by-value hay pass-by-reference
- Trình bày cách để break bên trong vòng lặp lòng nhau
- Cách hoán đổi 2 số a và b mà ko cần tạo thêm biến thứ 3

https://shareprogramming.net/co-che-pass-by-value-va-pass-by-reference-trong-java/  
https://kipalog.com/posts/Pass-by-reference-va-pass-by-value  
https://viettuts.vn/java/truyen-gia-tri-va-tham-chieu-pass-value-va-pass-reference-trong-java  
https://daynhauhoc.com/t/java-pass-by-value-or-pass-by-reference-d-chu-de-muon-thuo/23908  
https://luanvv.com/blog/pass-by-value-va-pass-by-reference-trong-java/  


## Top 10 câu hỏi phỏng vấn Java thường gặp
    1. Trên thang điểm 10 – Bạn đánh giá mình được bao nhiêu điểm?
    2. Bạn biết về những loại Collection nào?
    3. Liệt kê 5 đặc điểm bất kỳ của Java?
    4. Object Class có những Method nào?
    5. Tại sao String Object không thể thay đổi (Immutable) trong Java?
    6. Sự khác biệt giữa Final, Finally, và Finalize là gì?
    7. Vấn đề Diamond Problem là gì?
    8. Làm thế nào bạn có thể làm cho một class không thể thay đổi?
    9. Singleton có nghĩa là gì?
    10. Dependency Injection là gì?


## Một số câu hỏi hay gặp khi phỏng vấn vị trí lập trình Java

### Phỏng vấn thực tập, freshser

Với những bạn mới ra trường thì phỏng vấn sẽ nhẹ nhàng, chủ yếu đánh giá kiến thức nền tảng của các bạn.

#### 1. Lập trình hướng đối tượng là gì?
Trả lời: lập trình hướng đối tượng là 1 kỹ thuật lập trình, cho phép lập trình viên trừu tượng hóa các đối tượng thực tế thành các đối tượng trong code

#### 2. Các tính chất của lập trình hướng đối tượng trong Java?
Trả lời: Có 4 tính chất (tính trừu tượng, tính đóng gói, tính kế thừa, tính đa hình)  https://stackjava.com/oop/cac-tinh-chat-huong-doi-tuong-cua-java.html

#### 3. Hỏi về collection Framework (Cái này hầu như 100% ở đâu phỏng vấn cũng hỏi).
- Sự khác nhau giữa Set với Map
- Sự khác nhau giữa Linklist với Arraylist; Vector với Arraylist; HashTable với HashMap

#### 4. Sự khác nhau giữa Hashcode và Equals.
Trả lời: https://stackjava.com/java/hashcode-va-equals-trong-java.html

#### 5. Immutable là gì? Cách để tạo đối tượng immutable? 
Trả lời: https://stackjava.com/java/immuable-la-gi.html

#### 6. Sự khác nhau giữa abstract class và Interface.
Trả lời: https://stackjava.com/oop/su-khac-nhau-giua-abstract-class-voi-interface-trong-java.html
(* Chú ý: Từ Java 8 và Java 9, có khá nhiều thay đổi đối với Interface)

Phần này thường hỏi đối với người đã có kinh nghiệm đi làm.

#### 7. Khái niệm DI là gì?

#### 8. Hỏi về các design pattern (1 số design pattern quen thuộc).

#### 9. Hỏi về thuật toán.
1 số thuật toán quen thuộc như DFS, BFS, các thuật toán đồ thị, tìm kiếm…, thường thì phần này sẽ rơi vào phần làm bài test nhưng đôi khi cũng sẽ hỏi miệng chủ yếu để xác định bạn có biết tới những thuật toán đó không.

#### 10. Hỏi về các dự án bạn đã làm, nghiên cứu.
Dự án ở đây là các bài tập lớn bạn đã làm, đồ án tốt nghiệp.

Để tạo ấn tượng tốt bạn nên có 1 số project trên github đối với các bài tập lớn của mình hoặc tham gia viết bài trên một blog nào đó về lập trình.

#### 11. Hỏi về khả năng tự học, tiếp cận/giải quyết vấn đề.
Cái này chủ yếu về cách mà bạn giải quyết vấn đề, tiếp cận cái mới. Thí dụ cách mà bạn search google cũng được đánh giá khá cao.

Ví dụ: nhà tuyển dụng hỏi bạn: “em làm chức năng Login” hết bao lâu thời gian thì đừng trả lời mà phải hỏi lại là chức năng login như nào, áp dụng công nghệ nào, các role, permission ra sao…

Hỏi về những kỹ thuật, ngôn ngữ nào mà bạn tự học, tìm hiểu?

Đặc biệt nếu bạn đọc nhiều sách về lập trình thì sẽ được đánh giá rất cao. Một số sách hay về Java như: Sun Certified Programmer for Java®Platform; Clean Code, Java Effective.

### Phỏng vấn với vị trí có kinh nghiệm
Đối với vị trí yêu cầu kinh nghiệm thì yêu cầu cao hơn, các nhà phỏng vấn sẽ đánh giá nhiều về những gì bạn đã làm được.

Giả sử bạn giỏi, kinh nghiệm 2,3 năm nhưng bạn chỉ xào đi xào lại 1 dự án, chẳng có công nghệ, framework gì mới thì sẽ bị đánh giá rất thấp do đó những năm đầu đi xin việc mọi người đừng quá quan tâm vào lương mà hãy để ý xem nơi mình vào làm sẽ giúp mình học được gì, phát triển được gì.

Và thông thường nếu chỉ tầm 3 năm kinh nghiệm trở xuống thì bạn sẽ vẫn gặp những câu hỏi cơ bản giống như lúc tuyển fresher

#### 1. Bạn đã làm những dự án nào? dự án đó làm cái gì, kích thước dự án ra sao và đóng góp vào dự án của bạn là gì?

#### 2. Bạn biết những kỹ thuật, công nghệ, framework gì?
Cái này chủ yếu để xác định xem bạn có phù hợp với vị trí ứng tuyển không.

Ví dụ công ty đang làm về JSF và đang rất cần người biết về JSF nhưng bạn lại chỉ biết Spring thì sẽ không được ưu tiên bằng các ứng viên khác. Một số ít công ty thì chủ yếu maintain các dự án cũ nên sẽ làm nhiều về Struts (cái này giờ ít dùng), thậm chí có lần mình phỏng vấn 1 công ty mà sản phẩm của họ không hề dùng các công nghệ mới chỉ vì sản phẩm của họ đang ổn định.

#### 3. Hỏi sâu về kiến thức mà bạn bảo mình biết 🙂
Phần này sẽ là phần đánh giá chủ yếu về kỹ thuật, nó giúp nhà tuyển dụng đánh giá những gì bạn trình bày có đúng ko.
Ví dụ:
- Bạn bảo mình làm về Spring thì sẽ hỏi đại loại như Spring có những module nào? DI trong Spring như nào;
- Bạn bảo mình biết JSF thì sẽ hỏi JSF có những phase nào…
- Về Hibernate thì hỏi hibernat khác gì JPA, save – saveOrUpdate – merge khác gì nhau…
- Hỏi về REST, maven…

Nếu cái gì bạn không biết thì ko nên đề cập tới trong CV. Nếu có hỏi tới thì cứ thoải mái thừa nhận là phần đó em chưa làm nhiều.

#### 4. Ở các vị trí cao hơn
Với người có kinh nghiệm làm leader, hoặc kinh nghiệm lâu năm 8,9 năm gì đó thì sẽ hỏi nhiều về kiến trúc, pattern, cách lead team.

Chú ý lúc phỏng vấn cũng là lúc bạn phỏng vấn ngược lại để biết được mình sẽ làm việc với ai, làm về cái gì, khả năng phát triển/ học hỏi được ở công ty ra sao.
Và đừng ngại đi phỏng vấn, mình phỏng cũng có lần tạch, cũng nhận được khá nhiều lời mời. Sau mỗi lần như thế bạn sẽ thể hiện mình tốt hơn trước nhà phỏng vấn.
Chúc bạn tự tin khi đi phỏng vấn nha!


## 201 câu hỏi phỏng vấn java core

### Java Core - java cơ bản
    1. Sự khác nhau giữa JDK,JRE và JVM?
    2. Sự khác nhau giữa bộ nhớ heap và stack trong java?
    3. Trình biên dịch JIT là gì?
    4. Platform là gì?
    5. Sự khác nhau giữa Java platform và các platform khác?
    6. Tính chất "viết một lần chạy nhiều nơi" của java là gì?
    7. Classloader trong java là gì?
    8. File có tên trống ".java" có hợp lệ không?
    9. Các từ delete, next, main, exit và null có phải là từ khóa trong java không?
    10. Nếu không cung cấp bất kỳ đối số nào trên command line, thì mảng String của hàm main là empty hay null?
    11. Chuyện gì xảy ra nếu khai báo static public void thay vì public static void?
    12. Giá trị mặc định của các biến local là gì?

####  Java Core - các khái niệm về OPPs
    1. Sự khác biệt giữa ngôn ngữ lập trình hướng đối tượng và ngôn ngữ lập trình dựa trên đối tượng là gì?
    2. Giá trị khởi tạo của biến tham chiếu đối tượng được định nghĩa là biến instance là gì?

#### Java Core - các khái niệm về OPPs: Câu hỏi phỏng vấn Constructor
    1. Constructor là gì?
    2. Mục đích của constructor là gì?
    3. Constructor trả về kiểu giá trị gì?
    4. Constructor được kế thừa không?
    5. Có thể tạo constructor final không?

#### Java Core - các khái niệm về OPPs: Câu hỏi phỏng vấn từ khóa static
    1. Biến static là gì?
    2. Phương thức static là gì?
    3. Tại sao phương thức main là static?
    4. Khối static là gì?
    5. Chúng ta có thể thực thi một chương trình không có phương thức main() không?
    6. Chuyện gì xảy ra khi phương thức main không có static?
    7. Sự khác nhau giữa phương thức static và phương thức instance?

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn kế thừa
    1. this trong java là gì?
    2. Kế thừa là gì?
    3. Lớp nào là lớp cha cho tất cả các lớp.
    4. Tại sao đa kế thừa không được hỗ trợ trong java.
    5. Composition là gì?
    6. Sự khác nhau giữa aggregation và composition?
    7. Tại sao java không support con trỏ?
    8. super trong java là gì?
    9. Có thể sử dụng cả this() và super() trong một constructor?
    10. Object cloning là gì?

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn overloading phương thức
    11. Overloading (nạp chồng) phương thức là gì?
    12. Tại sao overloading phương thức không xảy ra khi thay đổi kiểu giá trị trả về?
    13. Có thể overload phương thúc main() không?

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn overriding phương thức
    1. Ghi đè (overriding) phương thức là gì?
    2. Có thể ghi đè phương thức static không?
    3. Tại sao không thể ghi đè phương thức static?
    4. Có thể ghi đè phương thức đã nạp chồng?
    5. Có thể ghi đè biến instance không?
    6. Sự khác nhau giữa nạp chồng và ghi đè là gì?
    7. Kiểu trả về hiệp biến là gì?

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn từ khóa final
    8. Biến final là gì?
    9. Phương thức final là gì?
    10. Lớp final là gì?
    11. Biến final blank là gì?
    12. Có thể khởi tạo giá trị cho biến final blank không?
    13. Có thể khai báo phương thức main là final không?

#### Java Core – các khái niệm về OPPs: Các câu hỏi phỏng vấn đa hình
    1. Đa hình tại runtime là gì?
    2. Có thể thực hiện đa hình lúc runtime với các thành viên dữ liệu không?
    3. Sự khác nhau giữa ràng buộc tĩnh và ràng buộc động là gì?

#### Java Core – các khái niệm về OPPs: Các câu hỏi phỏng vấn trừu tượng
    1.Trừu tượng là gì?
    2. Sự khác nhau giữa trừu tượng và đóng gói là gì?
    3. Lớp trừu tượng là gì?
    59. Có phương thức trừu tượng không nằm trong lớp trừu tượng không?
    4. Có thể sử dụng cả abstract và final cho một phương thức không?
    5. Có thể tạo thể hiện của lớp trừu tượng không?
    6. Interface là gì?
    7. Có thể khai báo một phương thức của interface với từ khóa static không?
    8. Một interface có thể là final không?
    9. Marker interface là gì?
    10. Sự khác nhau giữa lớp abstract và interface là gì?
    11. Có thẻ định nghĩa private hoặc protected cho các biến trong interface không?
    12. Khi nào một tham chiếu đối tượng có thể được ép sang kiểu interface tham chiếu?

#### Java Core – các khái niệm về OPPs: Các câu hỏi phỏng vấn package
    1. Package là gì?
    2. Có cần import package import java.lang không? tại sao?
    3. Có thể import package/lớp giống nhau hai lần không? JVM sẽ tải package hai lần khi chạy không?
    4. Static import là gì?

#### Câu hỏi phỏng vấn xử lý ngoại lệ trong java
    1. Xử lý ngoại lệ (handling exception) là gì?
    2. Sự khác biệt giữa checked exception và unchecked exception là gì?
    3. Có phải mỗi khối try phải đi kèm với một khối catch?
    4. Khối finally là gì?
    5. Khối finally có thể được sử dụng mà không cần khối catch không?
    6. Có trường hợp nào khối finally không được thực thi không?
    7. Sự khác nhau giữa throw và throws là gì?
    8. Có thể khai báo phương thức overriding của lớp con một ngoại lệ nếu phương thức của lớp cha không throw một ngoại lệ?
    9. Việc tuyên truyền ngoại lệ là gì?

#### Câu hỏi phỏng vấn String trong java
    1. Ý nghĩa của immutable (bất biến) trong String là gì?
    2. Tại sao các đối tượng String trong java là immutable?
    3. Có bao nhiêu cách để tạo ra một đối tượng String trong java?
    4. Có bao nhiêu đối tượng String được tạo ra trong đoạn code sau?
    5. Tại sao java sử dụng khái niệm string literal?
    6. Có bao nhiêu đối tượng được tạo ra trong đoạn code sau?
    8. Sự khác nhau giữa String và StringBuffer là gì?
    9. Sự khác nhau giữa StringBuffer và StringBuilder là gì?
    10. Làm thế nào để tạo lớp immutable trong java?
    11. Mục đích của phương thức toString() trong java là gì?

#### Câu hỏi phỏng vấn Nested class và Interface
    1. Nested class (lớp lồng nhau) là gì?
    2. Có sự khác nhau giữa nested class và inner class không?
    3. Nested interface là gì?
    4. Có thể khai báo interface trong class không?
    5. Có thể khai báo một class trong interface không?

#### Câu hỏi phỏng vấn Java Collection
    1. Sự khác nhau giữa ArrayList và Vector là gì? 
    2. Sự khác nhau giữa ArrayList và LinkedList là gì? 
    3. Sự khác nhau giữa Iterator và ListIterator là gì? 
    4. Sự khác biệt giữa Iterator và Enumeration là gì? 
    5. Sự khác nhau giữa List và Set là gì? 
    6. Sự khác nhau giữa HashSet và TreeSet là gì? 
    7. Sự khác nhau giữa Set và Map là gì? 
    8. Sự khác biệt giữa HashSet và HashMap là gì? 
    9. Sự khác nhau giữa HashMap và TreeMap là gì? 
    10. Sự khác nhau giữa HashMap và Hashtable là gì? 
    11. Sự khác nhau giữa Collection và Collections là gì? 
    12. Sự khác nhau giữa Comparable và Comparator là gì? 
    13. Lợi thế của Properties file là gì? 
    14. Phương thức hashCode() là gì? 
    15. Tại sao chúng ta phải nghi đè phương thức equals()? 
    16. Làm thế nào để đồng bộ List, Set và Map? 
    17. Lợi ích của generic collection là gì? 
    18. Hash-collision trong Hashtable là gì? Và nó được xử lý như thế nào? 
    19. Lớp Dictionary là gì? 
    20. Sự khác nhau giữa Array và ArrayList là gì? 

#### Câu hỏi phỏng vấn servlet
https://viettuts.vn/interview/list-cau-hoi-phong-van-servlet

#### Câu hỏi phỏng vấn JSP
https://viettuts.vn/interview/list-cau-hoi-phong-van-jsp

#### Câu hỏi phỏng vấn Hibernate
https://viettuts.vn/interview/list-cau-hoi-phong-van-hibernate


## 200 câu hỏi phỏng vấn Java hay thường gặp
    1. Bạn biết gì về Java?
    2. Các nền tảng được hỗ trợ bởi Ngôn ngữ lập trình Java?
    3. Liệt kê 5 đặc điểm bất kỳ của Java?
    4. Tại sao Java là độc lập cấu trúc?
    5. Hiệu suất cao (High Performance) được kích hoạt như thế nào trong Java?
    6. Tại sao Java được coi là động (Dynamic)?
    7. Java Virtual Machine là gì và nó có vai trò gì trong đặc điểm độc lập nền tảng của Java?
    8. Liệt kê hai JDE của Java?
    9. Liệt kê một số từ khóa trong Java (không giống từ khóa trong C, C++)?
    10. Bạn hiểu gì về Đối tượng?
    11. Định nghĩa Lớp (class)?
    12. Class có thể chứa những kiểu biến nào?
    13. Biến local hay biến cục bộ là gì?
    14. Biến instance là gì?
    15. Biến lớp là gì?
    16. Lớp Singleton là gì?
    17. Bạn hiểu gì về Contructor?
    18. Liệt kê ba bước để tạo một đối tượng cho một lớp?
    19. Giá trị mặc định của kiểu dữ liệu byte trong Java?
    20. Giá trị mặc định của kiểu dữ liệu float và double trong Java?
    21. Kiểu dữ liệu byte được sử dụng khi nào?
    22. Biến static (biến tĩnh) là gì?
    23. Bạn hiểu gì về Access Modifier?
    24. Protected Access Modifier là gì?
    25. Synchronized Non Access Modifier là gì?
    26. Theo quyền ưu tiên của các toán tử trong Java, toán tử nào có quyền ưu tiên cao nhất?
    27. Các biến được sử dụng trong lệnh switch có thể được sử dụng với kiểu dữ liệu nào?
    28. Khi nào phương thức parseInt() có thể được sử dụng?
    29. Tại sao lớp String được coi như là bất biến (Immutable)?
    30. Tại sao StringBuffer được gọi là khả biến?
    31. Sự khác nhau giữa hai lớp StringBuffer và StringBuilder?
    32. Package nào được sử dụng để so khớp mẫu (Pattern Matching) với Regular Expression trong Java?
    33. java.util.regex gồm các lớp nào?
    34. Phương thức finalize() làm gì?
    35. Exception (Ngoại lệ) là gì?
    36. Bạn biết gì về Checked Exception?
    37. Giải thích Runtime Exception?
    38. Lớp Exception có hai lớp con nào?
    39. Khi nào từ kháo throws được sử dụng?
    40. Khi nào từ khóa throw được sử dụng?
    41. Cách finally được sử dụng dưới Exception Handling?
    42. Bạn nên ghi nhớ điều gì trong khi tạo Exception cho riêng mình trong Java?
    43. Tính kế thừa (Inheritance) là gì?
    44. Sử dụng từ khóa super khi nào?
    45. Định nghĩa tính đa hình (Polymorphism)?
    46. Tính trừu tượng (Abstraction) là gì?
    47. Lớp Abstract là gì?
    48. Khi nào phương thức abstract được sử dụng?
    49. Tính bao đóng (Encapsulation) là gì?
    50. Lợi ích chính của tính bao đóng?
    51. Interface là gì?
    52. Một số đặc điểm của Interface?
    53. Trong Java, Package là gì?
    54. Tại sao Package được sử dụng?
    55. Bạn hiểu gì về Đa luồng (Multi-Thread)?
    56. Thread có thể được tạo bằng hai cách nào?
    57. Applet là gì?
    58. Một Applet kế thừa lớp nào?
    59. Giải thích trình dọn rác (Garbage Collector) trong Java?
    60. Định nghĩa đối tượng không thể biến đổi?
    61. Giải thích sự sử dụng của this() với các Constructor?
    62. Bạn biết gì về Set Interface?
    63. Trình bày TreeSet?
    64. Comparable Interface là gì?
    65. Điểm khác nhau giữa throws và throw?
    66. Giải thích dòng code sau bằng ngôn ngữ Java?
    67. JRE (Java Runtime Environment) là gì?
    68. JAR file là gì?
    69. WAR file là gì?
    70. Định nghĩa JIT Compiler?
    71. Điểm khác nhau giữa Ngôn ngữ lập trình hướng đối tượng và ngôn ngữ lập trình dựa vào đối tượng?
    72. Mục đích của Constructor mặc định?
    73. Một Constructor có thể được tạo là final không?
    74. Khối static là gì?
    75. Định nghĩa Composition?
    76. Quá tải phương thức (Method Overloading) là gì?
    77. Ghi đè phương thức (Method Overriding) là gì?
    78. Sự khác nhau giữa nạp chồng và ghi đè (Overloading vs Overriding)?
    79. Lớp final là gì?
    80. NullPointerException là gì?
    81. Các cách mà một Thread có thể đi vào trạng thái đợi?
    82. Cách mà Đa luồng (Multi-Thread) diễn ra trên một máy tính với một CPU đơn?
    83. Triệu hồi phương thức run() của một Thread là gì?
    84. Có vấn đề gì không với thứ tự của các lệnh catch được viết cho FileNotFoundException và IOException?
    85. Điểm khác nhau giữa yield và sleep?
    86. Tại sao lớp Vector được sử dụng?
    87. Có bao nhiêu Bit được sử dụng để biểu diễn các ký tự Unicode, ASCII, UTF-16 và UTF-8?
    88. Các lớp Wrapper là gì?
    89. Điểm khác nhau giữa một Window và một Frame?
    90. Package nào có các thành phần gọn nhẹ (lightweight)?
    91. Đâu là điểm khác nhau giữa hai phương thức paint() và repaint()?
    92. Lớp File có mục đích gì?
    93. Điểm khác nhau giữa cấu trúc lớp Reader/Writer và cấu trúc lớp InputStream/OutputStream.
    94. Bạn sử dụng lớp nào để lấy thông tin thiết kế về một đối tượng?
    95. Biến static và biến non-static khác nhau ở điểm nào?
    96. Serialization và Deserialization là gì?
    97. Case là gì?
    98. Giải thích sự sử dụng của lớp con trong một chương trình Java?
    99. Cách thêm menushortcut tới menu item?
    100. Bạn có thể viết môt lớp Java mà có thể được sử dụng như một Applet cũng như một ứng dụng không?
    101. Điểm khác nhau giữa các thành phần Swing và AWT?
    102. Điểm khác nhau giữa Constructor và các phương thức khác?
    103. Có bất kỳ giới hạn nào khi sử dụng Tính kế thừa (Inheritance)?
    104. Khi nào ArrayStoreException được ném?
    105. Bạn có thể gọi một Constructor này từ Constructor khác nến một lớp có nhiều Constructor không?
    106. Phương thức sleep() và wait() khác nhau ở điểm nào?
    107. ArithmeticException được ném khi nào?
    108. Một biến là transient (tạm thời) là gì?
    109. Synchronization (Đồng bộ hóa) là gì?
    110. Collection API là gì?
    111. Trình dọn rác có bảo đảm rằng một chương trình sẽ không chạy hết bộ nhớ?
    112. Lớp cha gần nhất (trực tiếp) của lớp Applet?
    113. Toán tử nào trong Java là Right-Associative?
    114. Điểm khác nhau giữa lệnh break và lệnh continue?
    115. Nếu một biến được khai báo là private, thì nó có thể được truy cập trong phạm vi nào?
    116. Mục đích của lớp System?
    117. Liệt kê các kiểu gốc trong Java?
    118. Mối quan hệ giữa Clipping và Repainting dưới AWT?
    119. Lớp nào là lớp cha gần nhất (trực tiếp) của lớp Container?
    120. Lớp Exception nào được tạo bởi Java runtime?
    121. Dưới các điều kiện nào thì một phương thức finalize() của đối tượng được triệu hồi bởi trình dọn rác (Garbage Collector)?
    122. Một Thread đã chết có thể được restart lại như thế nào?
    123. Các toán tử số học nào có thể gây ra sự kiện ném một ArithmeticException?
    124. Biến kiểu Boolean được tự động khởi tạo với giá trị?
    125. Các lệnh try có thể lồng nhau không?
    126. ClassLoader là gì?
    127. Điểm khác nhau giữa một Interface và một lớp Abstract?
    128. Điều gì xảy ra nếu Static Modifier bị gỡ bỏ từ phương thức main?
    129. Giá trị mặc định của một tham chiếu đối tượng được khai báo như là một biến instance?
    130. Lớp cao nhất có thể là private hoặc protected không?
    131. Tại sao chúng ta cần các lớp wrapper?
    132. Điểm khác nhau giữa Error và Exception?
    133. Có cần thiết để mỗi khối try phải được theo sau bởi một khối catch không?
    134. Khi một Thread được tạo và bắt đầu, trạng thái ban đầu (initial state) của nó là gì?
    135. Lớp Locale là gì?
    136. Phương thức synchronized và lệnh synchronized là gì?
    137. Gửi phương thức động hoặc đa hình tại runtime là gì?
    138. Dynamic Binding (Late Biding) là gì?
    139. Constructor có thể được kế thừa không?
    140. Lợi thế của ArrayList so với các mảng?
    141. Hoạt động xóa trong LinkedList là nhanh hơn trong ArrayList, tại sao?
    142. Bạn quyết định khi nào sử dụng ArrayList và LinkedList?
    143. Một Values Collection View là gì?
    144. Dot Operator (Toán tử .) là gì?
    145. Bạn có thể sử dụng Private Constructor ở đâu và như thế nào?
    146. Type Casting (Ép kiểu) là gì?
    147. Miêu tả vòng đời (Life Cycle) của Thread?
    148. Điểm khác nhau giữa hai toán tử » và »> ?
    149. Phương thức nào của lớp Component được sử dụng để thiết lập vị trí và kích cỡ của một component?
    150. Dãy giá trị của kiểu short?
    151. Lớp cha gần nhất của Menu?
    152. Java có cho phép các tham số mặc định không?
    153. Trong Java, hệ cơ số nào được biểu thị với số 0 bắt đầu?
    154. Trong Java, hệ cơ số nào được biểu thị với phần bắt đầu là 0x hoặc 0X?
    155. Lệnh break có thể được sử dụng như là các nhãn (label) trong Java?
    156. Lệnh import được sử dụng ở đâu trong một chương trình Java?
    157. Giải thích phương thức suspend() dưới lớp Thread?
    158. Giải thích phương thức isAlive() dưới lớp Thread?
    159. Bạn hiểu gì về phương thức currentThread()?
    160. Giải thích main thread dưới sự thực thi của lớp Thread?
    161. Vòng đời của một Applet?
    162. Vai trò của phương thức init() dưới Applet?
    163. Phương thức nào được gọi bởi lớp Applet để tải một hình ảnh?
    164. Định nghĩa phần code được sử dụng như là một thuộc tính của Applet?
    165. Canvas là gì?
    166. Định nghĩa Lập trình mạng?
    167. Socket là gì?
    168. Lợi thế của Java Socket?
    169. Hạn chế của Java Socket?
    170. Lớp nào được sử dụng bởi các ứng dụng Server để thu nhận một cổng (port) và các yêu cầu từ Client?
    171. Lớp nào biểu diễn Socket mà cả Server và Client sử dụng để giao tiếp với nhau?
    172. Tại sao Generic được sử dụng trong Java?
    173. Bạn cần thiết lập các biến môi trường nào trên thiết bị để có thể chạy các chương trình Java?
    174. Có cần thiết phải nhập java.lang package không?
    175. Lớp cao nhất được lồng là gì?
    176. Trình bày Externalizable Interface?
    177. Khối finally sẽ vẫn thực thi nếu như có System.exit(0); được viết ở cuối khối try?
    178. Bạn hiểu gì về Daemon Thread?
    179. Phương thức được sử dụng để tạo Daemon Thread?
    180. Tất cả Thread phải triển khai phương thức nào?
    181. Lớp GregorianCalendar là gì?
    182. Bạn hiểu gì về lớp SimpleTimeZone?
    183. Điểm khác nhau giữa hai tham số size và capacity của một Vector?
    184. Một Vector có thể chứa các đối tượng hỗn tạp không?
    185. Trình bày Enumeration?
    186. Path và Classpath khác nhau ở điểm nào?
    187. Một lớp được khai báo là private có thể được truy cập từ bên ngoài package của nó không?
    188. Ràng buộc nào phải được tuân theo trên một phương thức static hoặc một khối static?
    189. Một Interface có thể kế thừa Interface khác không?
    190. Ghi đè và nạp chồng là dựa trên khái niệm hướng đối tượng nào?
    191. Lock của một đối tượng là gì và các đối tượng nào có lock?
    192. Khái niệm Downcasting là gì?
    193. Thứ tự độ ưu tiên và Associativity là gì và cách chúng được sử dụng?
    194. Nếu một phương thức được khai báo là protected, thì phương thức đó có thể được truy cập ở đâu?
    195. Điểm khác nhau giữa Inner Class và Nested Class?
    196. Bạn cần chú ý điều gì khi thực hiện ghi đè phương thức?
    197. Chuỗi Constructor (hay Constructor Chaining) là gì và cách thực hiện nó trong Java?
    198. Có thể ép kiểu giá trị double thành một byte được không?
    199. Cách một lệnh try quyết định mệnh đề catch nào nên được sử dụng để xử lý một Exception?
    200. Các giá trị mặc định của tất cả phần tử trong một mảng khi được định nghĩa như là một biến instance là gì?


#### 1. Bạn biết gì về Java?
Java là một ngôn ngữ lập trình cấp cao, được phát triển đầu tiên bởi Sun Microsystems và được công bố năm 1995. Java chạy trên các nền tảng đa dạng, như Windows, Mac OS, và các phiên bản UNIX đa dạng.

Tham khảo thêm: Java là gì? Tại sao nên chọn Java?

#### 2. Các nền tảng được hỗ trợ bởi Ngôn ngữ lập trình Java?
Java là ngôn ngữ lập trình đa nền tảng, có thể chạy trên Windows, Mac OS, và các phiên bản UNIX đa dạng như HP-Unix, Sun Solaris, Redhat Linux, Ubuntu, CentOS,…

#### 3. Liệt kê 5 đặc điểm bất kỳ của Java?
Một số đặc điểm của Java là Hướng đối tượng, Độc lập nền tảng, Thông dịch, Đa luồng (Multi-thread), mạnh mẽ (robust).

#### 4. Tại sao Java là độc lập cấu trúc?
Trình biên dịch của nó tạo ra một định dạng file độc lập cấu trúc, làm cho code được biên dịch có thể thực thi trên bất kỳ bộ xử lý nào nào, với sự có mặt của hệ thống Java runtime.

#### 5. Hiệu suất cao (High Performance) được kích hoạt như thế nào trong Java?
Java sử dụng Just-In-Time compiler để kích hoạt hiệu năng cao. Trình biên dịch này biến Java Bytecode (một chương trình chứa các chỉ thị cần được thông dịch) thành các chỉ thị có thể được gửi trực tiếp tới bộ xử lý.

#### 6. Tại sao Java được coi là động (Dynamic)?
Nó được thiết kế để thích nghi với môi trường đang phát triển. Các chương trình Java có thể mang một lượng lớn thông tin trong thời điểm chạy có thể được sử dụng để kiểm tra và xử lý các truy cập tới đối tượng tại thời điểm chạy (runtime).

#### 7. Java Virtual Machine là gì và nó có vai trò gì trong đặc điểm độc lập nền tảng của Java?
Khi Java được biên dịch, nó không được biên dịch sang nền tảng máy cụ thể nào, mà được dịch sang Bytecode độc lập nền tảng. Bytecode này được phân phối thông qua Web và được thông dịch bởi Java Virtual Machine (JVM) trên bất kỳ nền tảng nào nó đang chạy.

#### 8. Liệt kê hai JDE của Java?
Netbeans, Eclipse,... (hãy kể nhiều JDE hơn hoặc nói chi tiết hơn một chút về 2 JDE này để ghi điểm với nhà tuyển dụng).

#### 9. Liệt kê một số từ khóa trong Java (không giống từ khóa trong C, C++)?
Một số từ khóa trong Java là import, super, finally,…

#### 10. Bạn hiểu gì về Đối tượng?
Đối tượng là một thực thể tại runtime, trạng thái của nó được lưu trữ trong các trường và hành vi được thể hiện thông qua các phương thức. Các phương thức vận hành trên trạng thái nội tại của đối tượng và đóng vai trò như là cơ chế chính để giao tiếp giữa các đối tượng với nhau.

#### 11. Định nghĩa Lớp (class)?
Một lớp là một thiết kế (blueprint) từ đó các đối tượng riêng lẻ được tạo. Một lớp có thể chứa các trường và các phương thức để miêu tả hành vi của một đối tượng.

#### 12. Class có thể chứa những kiểu biến nào?
Một lớp có thể gồm biến local, biến instance, và biến lớp.

#### 13. Biến local hay biến cục bộ là gì?
Các biến được định nghĩa bên trong phương thức, constructor hoặc các khối được gọi là biến local. Biến này sẽ được khai báo và khởi tạo bên trong phương thức và nó sẽ bị hủy khi phương thức kết thúc.

#### 14. Biến instance là gì?
Biến instance là các biến bên trong một lớp nhưng bên ngoài bất cứ phương thức nào. Những biến này được khởi tạo khi lớp được tải.

#### 15. Biến lớp là gì?
Đây là các biến được khai báo với một lớp, bên ngoài bất cứ phương thức nào, với từ khóa static.

#### 16. Lớp Singleton là gì?
Lớp Singleton trong Java kiểm soát việc tạo đối tượng, giới hạn số đối tượng là một nhưng nó cũng linh động khi cho phép bạn tạo nhiều đối tượng hơn nếu tình huống thay đổi.

#### 17. Bạn hiểu gì về Contructor?
Contructor được gọi khi một đối tượng mới được tạo. Mỗi lớp có một Constructor. Nếu chúng ta không viết constructor cho lớp một cách tường minh, thì trình biên dịch Java sẽ xây dựng một Constructor mặc định cho lớp đó.

#### 18. Liệt kê ba bước để tạo một đối tượng cho một lớp?
Đầu tiên, một đối tượng được khai báo, sau đó khởi tạo và cuối cùng là khởi chạy.

#### 19. Giá trị mặc định của kiểu dữ liệu byte trong Java?
Giá trị mặc định của kiểu dữ liệu byte là 0.

#### 20. Giá trị mặc định của kiểu dữ liệu float và double trong Java?
Giá trị mặc định của kiểu dữ liệu float và double trong Python khác với trong C/C++. Mặc định của float là 0.0f và của double là 0.0d.

#### 21. Kiểu dữ liệu byte được sử dụng khi nào?
Kiểu dữ liệu này được sử dụng để lưu trữ không gian trong các mảng rộng, chủ yếu để thay thế cho các số nguyên, vì một byte nhỏ hơn 4 lần so với một int.

#### 22. Biến static (biến tĩnh) là gì?
Các biến lớp cũng còn được biết đến với tên gọi là biến tĩnh (biến static) được khai báo với từ khóa static trong một lớp, nhưng nằm ngoài một phương thức, constructor hoặc một khối.

#### 23. Bạn hiểu gì về Access Modifier?
Java cung cấp một số Access Modifier để thiết lập mức độ truy cập cho các lớp, các biến, phương thức và constructor. Một thành viên có khả năng truy cập mặc định khi không có Access Modifier nào được xác định.

#### 24. Protected Access Modifier là gì?
Các biến, phương thức và constructor, mà được khai báo protected trong một lớp cha (superclass), chỉ được truy cập bởi các lớp cha trong package khác hoặc bất kỳ lớp nào bên trong package đó của lớp được protected.

#### 25. Synchronized Non Access Modifier là gì?
Java cung cấp Synchronized Non Access Modifier để mang tới những tính năng khác ngoài Access Modifier, từ Synchronized chỉ ra rằng một phương thức chỉ được truy cập bởi một luồng tại một thời điểm.

#### 26. Theo quyền ưu tiên của các toán tử trong Java, toán tử nào có quyền ưu tiên cao nhất?
Các toán tử postfix như (), [], . là có quyền ưu tiên cao nhất.

#### 27. Các biến được sử dụng trong lệnh switch có thể được sử dụng với kiểu dữ liệu nào?
Các biến được sử dụng trong một lệnh switch chỉ có thể là một byte, string, enum, short, int hoặc char.

#### 28. Khi nào phương thức parseInt() có thể được sử dụng?
Phương thức này được sử dụng để lấy kiểu dữ liệu gốc của một chuỗi nhất định.

#### 29. Tại sao lớp String được coi như là bất biến (Immutable)?
Lớp String là bất biến hay không thể thay đổi, và khi nó đã được tạo, một đối tượng String không thể bị biến đổi. Do String là bất biến, nên nó có thể được chia sẻ an toàn giữa nhiều luồng. Điều này là một phần rất quan trọng cho lập trình đa luồng.

#### 30. Tại sao StringBuffer được gọi là khả biến?
Các đối tượng StringBuffer có thể sửa đổi. Nếu có một tình huống bạn cần tạo nhiều sửa đổi đến các chuỗi ký tự thì nên sử dụng StringBuffer.

#### 31. Sự khác nhau giữa hai lớp StringBuffer và StringBuilder?
Sử dụng StringBuilder bất cứ khi nào có thể bởi vì nó nhanh hơn StringBuffer. Nhưng, nếu an toàn luồng (Thread Safety) là cần thiết, thì bạn nên sử dụng các đối tượng StringBuffer.

#### 32. Package nào được sử dụng để so khớp mẫu (Pattern Matching) với Regular Expression trong Java?
Để sử dụng cho mục đích này, bạn dùng package java.util.regex.

#### 33. java.util.regex gồm các lớp nào?
java.util.regex gồm ba lớp: lớp Pattern, lớp Matcher và lớp PatternSyntaxException.

#### 34. Phương thức finalize() làm gì?
Có thể định nghĩa một phương thức mà sẽ được gọi ngay trước khi hủy đối tượng bởi Garbage Collector (Trình dọn rác). Phương thức này được gọi là finalize(), và nó có thể được sử dụng để bảo đảm rằng đã hoàn toàn kết thúc một đối tượng.

#### 35. Exception (Ngoại lệ) là gì?
Một Exception là một vấn đề được tạo ra trong khi thực thi một chương trình. Các Exception được bắt bởi Handler được xác định cùng với lời gọi phương thức của Thread.

#### 36. Bạn biết gì về Checked Exception?
Đặc trưng của loại Exception này là một lỗi người dùng hoặc một vấn đề không thể biết trước bởi lập trình viên. Ví dụ, nếu một file đã được mở, nhưng không tìm thấy file đó, thì một Exception xuất hiện. Những Exception này không thể được bỏ qua một cách đơn giản tại thời điểm biên dịch.

#### 37. Giải thích Runtime Exception?
Nó là một Exception mà có thể được tránh bởi lập trình viên. Trái ngược với Checked Exception, các Runtime Exception bị bỏ qua tại thời điểm biên dịch.

#### 38. Lớp Exception có hai lớp con nào?
Lớp Exception có hai lớp con chính là: lớp IOException và lớp RuntimeException.

#### 39. Khi nào từ kháo throws được sử dụng?
Nếu một phương thức không xử lý một Checked Exception, phương thức phải được khai báo với từ khóa throws. Từ khóa throws xuất hiện ở phần cuối một phương thức.

#### 40. Khi nào từ khóa throw được sử dụng?
Một Exception có thể được ném, hoặc bởi được khởi tạo hoặc một Exception mà bạn vừa bắt, bởi sử dụng từ khóa throw.

#### 41. Cách finally được sử dụng dưới Exception Handling?
Từ khóa finally được sử dụng để tạo một khối code mà theo sau một khối try. Một khối finally luôn luôn thực thi, dù có xuất hiện một Exception hay không.

#### 42. Bạn nên ghi nhớ điều gì trong khi tạo Exception cho riêng mình trong Java?
Trong khi tạo riêng cho mình các Exception:
    Tất cả Exception phải là con của Throwable.
    Nếu bạn muốn viết một Checked Exception mà tự động được tuân theo bởi Handler hoặc Declare Rule (Qui tắc khai báo và xử lý ngoại lệ), thì bạn cần kế thừa lớp Exception.
    Nếu bạn muốn viết một Runtime Exception, bạn cần kế thừa lớp RuntimeException.

#### 43. Tính kế thừa (Inheritance) là gì?
Nó là một tiến trình mà một đối tượng thu được các thuộc tính của đối tượng khác. Sử dụng tính kế thừa, bạn có thể quản lý dễ dàng hơn với thông tin được tạo ra trong một cấu trúc có thứ bậc.

#### 44. Sử dụng từ khóa super khi nào?
Nếu phương thức ghi đè một trong các phương thức của lớp cha, thì phương thức bị ghi đè có thể được triệu hồi thông qua việc sử dụng từ khóa super. Nó cũng có thể được sử dụng để tham chiếu một trường bị ẩn.

#### 45. Định nghĩa tính đa hình (Polymorphism)?
Tính đa hình là khả năng giúp cho một đối tượng có nhiều hình thái. Trong OOP, sự sử dụng phổ biến nhất của tính đa hình là khi một tham chiếu lớp cha được sử dụng để tham chiếu tới một đối tượng lớp con.

#### 46. Tính trừu tượng (Abstraction) là gì?
Nó liên quan tới khả năng tạo một lớp trừu tượng (lớp abstract) trong OOP. Nó giúp giảm thiểu sự phức tạp và cũng cải thiện khả năng duy trì của hệ thống.

#### 47. Lớp Abstract là gì?
Những lớp này không thể được khởi tạo và được triển khai hoặc một phần hoặc không. Lớp này chứa một hoặc nhiều phương thức abstract, mà phần khai báo phương thức được đơn giản hóa với việc không có phần thân.

#### 48. Khi nào phương thức abstract được sử dụng?
Nếu bạn muốn một lớp chứa một phương thức cụ thể nhưng bạn muốn trình triển khai thực sự của phương thức đó được quyết định bởi các lớp con, bạn có thể khai báo phương thức trong lớp cha ở dạng abstract.

#### 49. Tính bao đóng (Encapsulation) là gì?
Nó là một kỹ thuật tạo các trường trong một lớp private và cung cấp truy cập tới các trường thông qua các phương thức public. Nếu một trường được khai báo là private,, nó không thể được truy cập bởi bất cứ phương thức nào bên ngoài lớp đó, từ đó ẩn các trường bên trong lớp. Vì thế, tính bao đóng cũng được xem như là Data hiding (ẩn dữ liệu).

#### 50. Lợi ích chính của tính bao đóng?
Lợi thế chủ yếu của tính bao đóng là khả năng để sửa đổi các code đã được triển khai của bạn mà không phá hủy phần code của ai đó. Nó như là tấm bảo vệ code và tránh code và dữ liệu của bạn bị truy cập một cách ngẫu nhiên từ code bên ngoài. Tính bao đóng cung cấp cho code tính duy trì, tính linh động, và mở rộng.

#### 51. Interface là gì?
Một Interface là một tập hợp các phương thức abstract. Một lớp triển khai một Interface, từ đó kế thừa các phương thức abstract của Interface đó.

#### 52. Một số đặc điểm của Interface?
Bao gồm:
    Interface không thể được khởi tạo.
    Một Interface không chứa bất cứ Constructor nào.
    Tất cả phương thức trong một Interface là Abtract.

#### 53. Trong Java, Package là gì?
Một Package có thể được định nghĩa như là một nhóm các kiểu (lớp, interface, kiểu liệt kê) có liên quan với nhau, cung cấp bảo vệ truy cập và trình quản lý namespace.

#### 54. Tại sao Package được sử dụng?
Package được sử dụng trong Java để ngăn ngừa các xung đột khi đặt tên, để điều khiển truy cập, để tìm kiếm và xác định vị trí, và để sử dụng các lớp, Interface, kiểu liệt kê … dễ dàng hơn.

#### 55. Bạn hiểu gì về Đa luồng (Multi-Thread)?
Một chương trình đa luồng bao gồm hai hoặc nhiều phần mà có thể chạy đồng thời. Mỗi phần của chương trình đó được gọi là một Thread, và một Thread xác định một trình thực thi khác nhau.

#### 56. Thread có thể được tạo bằng hai cách nào?
Thread có thể được tạo bởi: triển khai Runable Interface, kế thừa lớp Thread.

#### 57. Applet là gì?
Một Applet (vi mã) là một chương trình Java mà chạy trong một trình duyệt Web. Một Applet có thể là một ứng dụng Java đầy đủ tính năng bởi vì nó có toàn bộ Java API trong bố trí của nó.

#### 58. Một Applet kế thừa lớp nào?
Một Applet kế thừa lớp java.applet.Applet.

#### 59. Giải thích trình dọn rác (Garbage Collector) trong Java?
Java sử dụng trình dọn rác để giải phóng bộ nhớ. Bằng việc xóa bỏ các đối tượng mà không còn được sử dụng bởi bất cứ chương trình nào.

#### 60. Định nghĩa đối tượng không thể biến đổi?
Một đối tượng không thể biến đổi (immutable object) là không thể bị thay đổi từ khi nó được tạo.

#### 61. Giải thích sự sử dụng của this() với các Constructor?
Nó được sử dụng với các biến hoặc phương thức và được sử dụng để gọi Constructor của cùng lớp đó.

#### 62. Bạn biết gì về Set Interface?
Nó là một tập hợp phần tử mà không thể chứa bản sao các phần tử. Set Interface chỉ bao gồm các phương thức được kế thừa từ Collection và bổ sung thêm các giới hạn về ngăn cấm bản sao phần tử xuất hiện.

#### 63. Trình bày TreeSet?
Nó là một Set được triển khai khi chúng ta muốn các phần tử trong một thứ tự được sắp xếp.

#### 64. Comparable Interface là gì?
Nó được sử dụng để sắp xếp các Collection và các mảng đối tượng bởi sử dụng phương thức collection.sort() và java.utils. Các đối tượng của lớp triển khai Comparable Interface có thể được sắp xếp.

#### 65. Điểm khác nhau giữa throws và throw?
Bao gồm:
    Throw được sử dụng để kích hoạt một Exception trong khi throws được sử dụng trong khai báo của Exception.
    Không có throw, Checked Exception không thể được xử lý, trong khi throws được sử dụng để biểu thị những Exception không được xử lý bởi hàm.

#### 66. Giải thích dòng code sau bằng ngôn ngữ Java?
public static void main (String args[ ])

Dưới đây là phần giải tích chi tiết:
    public − nó là Access Specifier.
    static − nó cho phép main() để được gọi mà không cần khởi tạo một Instance cụ thể của một lớp.
    void − nó thông báo cho Compiler rằng không có giá trị nào được trả về bởi main().
    main() − phương thức này được gọi ở phần đầu chương trình Java.
    String args[ ] − tham số args là một mảng thể hiện của lớp String.

#### 67. JRE (Java Runtime Environment) là gì?
JRE là một trình triển khai của Java Virtual Machine mà thực thi các chương trình Java. Nó cung cấp các điều kiện tối thiểu để thực thi một ứng dụng Java.

#### 68. JAR file là gì?
JAR là viết tắt của Java Archive và nó kết hợp nhiều file lại thành một. Nó giữ các lớp Java trong một thư viện. JAR file được xây dựng trên định dạng ZIP file và có đuôi là .jar.

#### 69. WAR file là gì?
Đây là Web Archive File và được sử dụng để lưu trữ XML, các lớp Java, và JavaServer pages, mà được sử dụng để phân phối một tập hợp các JavaServer Page, Java Servlet, các lớp Java, XML file, Webpage tĩnh, …

#### 70. Định nghĩa JIT Compiler?
Nó cải thiện hiệu suất runtime của các chương trình máy tính dựa trên Bytecode.

#### 71. Điểm khác nhau giữa Ngôn ngữ lập trình hướng đối tượng và ngôn ngữ lập trình dựa vào đối tượng?
Ngôn ngữ lập trình dựa vào đối tượng có tất cả đặc điểm của OOP ngoại trừ Tính kế thừa (Inheritance). JavaScript là một ví dụ về Ngôn ngữ lập trình dựa trên đối tượng.

#### 72. Mục đích của Constructor mặc định?
Java Compiler tạo một Constructor mặc định chỉ nếu khi không có constructor nào trong lớp.

#### 73. Một Constructor có thể được tạo là final không?
Không, đây là điều không thể.

#### 74. Khối static là gì?
Nó được sử dụng để khởi tạo thành viên dữ liệu static. Nó được thực thi trước phương thức main tại thời gian tải lớp đó.

#### 75. Định nghĩa Composition?
Việc giữ tham chiếu của lớp khác bên trong một vài lớp khác được biết đến như là Composition.

#### 76. Quá tải phương thức (Method Overloading) là gì?
Nếu một lớp có nhiều hàm có cùng tên nhưng có tham số khác nhau, nó được xem như là quá tải phương thức (Method Overloading) hoặc quá tải hàm (Function Overloading).

#### 77. Ghi đè phương thức (Method Overriding) là gì?
Nếu một lớp con cung cấp một trình triển khai cụ thể của một phương thức mà đã được cung cấp bởi lớp cha của nó, thì đó là Ghi đè phương thức.

#### 78. Sự khác nhau giữa nạp chồng và ghi đè (Overloading vs Overriding)?
Nạp chồng phương thức tăng khả nang đọc của chương trình. Ghi đè phương thức cung cấp trình triển khai cụ thể của phương thức mà đã được cung cấp bởi lớp cha của nó. Tham số phải là khác kiểu trong nạp chồng, và trong ghi đè, các tham số là cùng kiểu.

#### 79. Lớp final là gì?
Các lớp final được tạo để các phương thức được triển khai bởi lớp đó không thể bị ghi đè. Nó không thể bị kế thừa.

#### 80. NullPointerException là gì?
Một NullPointerException được ném khi gọi phương thức instance của một đối tượng Null, truy cập hoặc sửa đổi các trường của một đối tượng Null,…

#### 81. Các cách mà một Thread có thể đi vào trạng thái đợi?
Một Thread có thể đi vào trạng thái đợi (Waiting state) bằng việc triệu hồi phương thức sleep() của nó, bằng việc được khóa trên IO, hoặc thất bại trong việc cố gắng thu được lock của đối tượng, hoặc bởi triệu hồi phương thức wait() của đối tượng. Nó cũng có thể đi vào trạng thái đợi bởi triệu hồi phương thức suspend() của nó (phương thức này đã cũ).

#### 82. Cách mà Đa luồng (Multi-Thread) diễn ra trên một máy tính với một CPU đơn?
Scheduler của hệ điều hành cấp phát thời gian thực thi cho các Task. Bằng việc nhanh nhóng chuyển đổi giữa các Task đang thực thi, nó tạo cho chúng ta cảm tưởng rằng các Task này được thực thi đồng thời.

#### 83. Triệu hồi phương thức run() của một Thread là gì?
Sau khi một Thread được tạo, thông qua phương thức start() của nó trong lớp Thread, JVM triệu hồi phương thức run() của Thread khi Thread này bắt đầu được thực thi.

#### 84. Có vấn đề gì không với thứ tự của các lệnh catch được viết cho FileNotFoundException và IOException?
Có. FileNotFoundException được kế thừa từ IOException. Các lớp con của Exception phải được bắt đầu tiên.

#### 85. Điểm khác nhau giữa yield và sleep?
Khi một tác vụ triệu hồi phương thức yield() của nó, nó chuyển thành trạng thái sẵn sàng. Khi một tác vụ triệu hồi phương thức sleep() của nó, nó chuyển sang trạnh thái đợi.

#### 86. Tại sao lớp Vector được sử dụng?
Lớp Vector cung cấp khả năng để triển khai mọt mảng có thể mở rộng của các đối tượng. Vector tỏ ra rất hữu ích nếu bạn không biết trước kích cỡ của mảng, hoặc nếu bạn chỉ cần một mảng mà có thể thay đổi kích cỡ trong thời gian sống của một chương trình.

#### 87. Có bao nhiêu Bit được sử dụng để biểu diễn các ký tự Unicode, ASCII, UTF-16 và UTF-8?
Unicode cần 16 bit và ASCII cần 7 bit. Mặc dù bộ ký tự ASCII chỉ sử dụng 7 bit, nhưng nó thường được biểu diễn bởi 8 bit. UTF-8 biểu diễn ký tự sử dụng 8 bit và là 16 bit cho UTF-16.

#### 88. Các lớp Wrapper là gì?
Đây là các lớp cho phép các kiểu dữ liệu gốc để được truy cập như là các đối tượng. Ví dụ: Integer, Character, Double, Boolean, …

#### 89. Điểm khác nhau giữa một Window và một Frame?
Lớp Frame kế thừa Window để định nghĩa một cửa sổ ứng dụng chính mà có thể có một menu bar.

#### 90. Package nào có các thành phần gọn nhẹ (lightweight)?
Đó là javax.Swing. Tất cả các thành phần trong Swing, ngoại trừ JApplet, JDialog, JFrame và JWindow là các thành phần gọn nhẹ.

#### 91. Đâu là điểm khác nhau giữa hai phương thức paint() và repaint()?
Phương thức paint() hỗ trợ việc vẽ thông qua một đối tượng Graphics. Phương thức repaint() được sử dụng để làm cho phương thức paint() có thể được triệu hồi bởi AWT Thread.

#### 92. Lớp File có mục đích gì?
Nó được sử dụng để tạo các đối tượng mà cung cấp sự truy cập tới các file và thư mục của hệ thống local file.

#### 93. Điểm khác nhau giữa cấu trúc lớp Reader/Writer và cấu trúc lớp InputStream/OutputStream.
Cấu trúc lớp Reader/Writer là hướng ký tự (Character-oriented), và cấu trúc lớp InputStream/OutputStream là hướng byte (Byte-oriented).

#### 94. Bạn sử dụng lớp nào để lấy thông tin thiết kế về một đối tượng?
Lớp Class được sử dụng để thu được thông tin về thiết kế của một đối tượng và sự thể hiện lớp java.lang.Class biểu diễn các lớp, Interface trong một ứng dụng Java đang chạy.

#### 95. Biến static và biến non-static khác nhau ở điểm nào?
Biến static (biến tĩnh) được gắn kết với toàn bộ lớp chứ không phải là instance của một lớp. Các biến non-static nhận các giá trị duy nhất với một sự thể hiện đối tượng.

#### 96. Serialization và Deserialization là gì?
Serialization là tiến trình ghi trạng thái của một đối tượng tới một Byte Stream. Deserialization là tiến trình phục hồi các đối tượng này.

#### 97. Case là gì?
Nó là một phần của tiến trình phân tích một chương trình và miêu tả một tình huống mà một chương trình có thể gặp phải và chương trình nên thực hiện hành vi nào trong tình huống đó.

#### 98. Giải thích sự sử dụng của lớp con trong một chương trình Java?
Các lớp con kế thừa tất cả các phương thức public và protected và triển triển khai. Nó cũng kế thừa tất cả các phương thức modifier mặc định và trình triển khai của chúng.

#### 99. Cách thêm menushortcut tới menu item?
Nếu có một sự thể hiện của button được gọi là b1, bạn có thể thêm menushortcut bằng việc gọi phương thức b1.setMnemonic('F'), từ đó người sử dụng có thể sử dụng phím tắt Alt+F để nhấn vào button đó.

#### 100. Bạn có thể viết môt lớp Java mà có thể được sử dụng như một Applet cũng như một ứng dụng không?
Có, chỉ cần thêm một phương thức main() tới Applet.

#### 101. Điểm khác nhau giữa các thành phần Swing và AWT?
Các thành phần AWT là nặng (heavy-weight), trong khi các thành phần Swing là gọn nhẹ (lightweight). Các thành phần nặng phụ thuộc vào bộ công cụ cửa sổ nội bộ (Local Windowing Toolkit). Ví dụ, java.awt.Button là một thành phần nặng, khi nó đang chạy trên nền tảng Java cho nền tảng Unix, nó ánh xạ tới Motif Button thực sự.

#### 102. Điểm khác nhau giữa Constructor và các phương thức khác?
Constructor phải có cùng tên với tên lớp và không thể trả về một giá trị. Chúng chỉ được gọi trong khi các phương thức thông thường có thể được gọi nhiều lần.

#### 103. Có bất kỳ giới hạn nào khi sử dụng Tính kế thừa (Inheritance)?
Có, khi tính kế thừa là kế thừa mọi thứ từ lớp cha và cả Interface, nhưng đôi khi nó có thể tạo ra đột biến (error-prone) với việc ghi đè động và nạp chồng động trong một số tình huống.

#### 104. Khi nào ArrayStoreException được ném?
Khi sao chép các phần tử giữa các mảng khác nhau, nếu tham số source hoặc tham số đích đến không là các mảng hoặc kiểu của chúng là không tương thích, thì khi đó một ArrayStoreException sẽ được ném.

#### 105. Bạn có thể gọi một Constructor này từ Constructor khác nến một lớp có nhiều Constructor không?
Có, sử dụng cú pháp this().

#### 106. Phương thức sleep() và wait() khác nhau ở điểm nào?
Ví dụ, sleep(2000); làm Thread đợi đúng 2 giây. Trong khi wait(2000); làm thời gian Thread chờ có thể lên tới 2 giây. Một Thread có thể dừng việc chờ đợi sớm hơn nếu nó nhận một lời gọi notify() hoặc notifyAll(). Phương thức wait() được định nghĩa trong lớp Object và phương thức sleep() được định nghĩa trong lớp Thread.

#### 107. ArithmeticException được ném khi nào?
ArithmeticException được ném khi chia số nguyên cho số 0 hoặc lấy phần dư của phép chia cho số 0. Nó không bao giờ được ném trong các phép toán về số thực.

#### 108. Một biến là transient (tạm thời) là gì?
Một biến transient là một biến mà không thể được xếp theo thứ tự trong Serialization và nó được khởi tạo bởi giá trị mặc định của nó trong Deserialization.

#### 109. Synchronization (Đồng bộ hóa) là gì?
Synchronization là khả năng điều khiển truy cập của nhiều Thread tới nguồn đã chia sẻ. Từ khóa synchronized trong Java cung cấp locking để đảm bảo sự truy cập tương hỗ mang tính loại trừ của nguồn đã chia sẻ và ngăn cản Data Race (Tranh đoạt dữ liệu).

#### 110. Collection API là gì?
Collection API là một tập hợp các lớp và Interface mà hỗ trợ các hoạt động trên các Collection của đối tượng.

#### 111. Trình dọn rác có bảo đảm rằng một chương trình sẽ không chạy hết bộ nhớ?
Trình dọn rác không bảo đảm rằng một chương trình sẽ không chạy hết bộ nhớ. Nó là có thể để cho các chương trình sử dụng hết nguồn bộ nhớ nhanh hơn việc chúng bị thu thập bởi trình dọn rác. Các chương trình cũng là có thể tạo các đối tượng mà không phụ thuộc vào trình dọn rác.

#### 112. Lớp cha gần nhất (trực tiếp) của lớp Applet?
Panel là lớp cha gần nhất (trực tiếp). Một panel cung cấp không gian trong đó một ứng dụng có thể đính kèm bất cứ thành phần nào, bao gồm các panel khác.

#### 113. Toán tử nào trong Java là Right-Associative?
Toán tử = là Right-Associative. (Nếu bạn chưa hiểu right và left associative, bạn theo dõi: Toán tử = cho phép bạn thực hiện nhiều phép gán trong cùng một lệnh. Ví dụ: a=b=c=d=99;)

#### 114. Điểm khác nhau giữa lệnh break và lệnh continue?
Lệnh break chấm dứt một lệnh mà nó áp dụng (switch, for, do, hoặc while). Một lệnh continue được sử dụng để kết thúc vòng lặp hiện tại và trả về điều khiển cho lệnh vòng lặp.

#### 115. Nếu một biến được khai báo là private, thì nó có thể được truy cập trong phạm vi nào?
Biến private chỉ có thể được truy cập bên trong lớp mà nó được khai báo.

#### 116. Mục đích của lớp System?
Mục đích của lớp System là cung cấp truy cập tới nguồn hệ thống.

#### 117. Liệt kê các kiểu gốc trong Java?
Có 8 kiểu dữ liệu gốc trong Java là byte, char, short, int, long, float, double và Boolean.

#### 118. Mối quan hệ giữa Clipping và Repainting dưới AWT?
Khi một cửa sổ được repaint bởi AWT Thread, nó thiết lập các khu vực Clipping thành khu vực của cửa sổ mà cần Repainting.

#### 119. Lớp nào là lớp cha gần nhất (trực tiếp) của lớp Container?
Lớp Component là lớp cha gần nhất.

#### 120. Lớp Exception nào được tạo bởi Java runtime?
Java runtime tạo các RuntimeException và Error.

#### 121. Dưới các điều kiện nào thì một phương thức finalize() của đối tượng được triệu hồi bởi trình dọn rác (Garbage Collector)?
Trình dọn rác triệu hồi một phương thức finalize() của đối tượng khi nó phát hiện rằng đối tượng đã thất bại.

#### 122. Một Thread đã chết có thể được restart lại như thế nào?
Một Thread đã chết không thể restart lại được.

#### 123. Các toán tử số học nào có thể gây ra sự kiện ném một ArithmeticException?
Phép chia / và lấy phần dư % số nguyên có thể gây ra sự kiện ném một ArithmeticException.

#### 124. Biến kiểu Boolean được tự động khởi tạo với giá trị?
Giá trị mặc định của kiểu Boolean là false.

#### 125. Các lệnh try có thể lồng nhau không?
Có.

#### 126. ClassLoader là gì?
ClassLoader là một đối tượng mà đảm nhiệm việc tải các lớp. Lớp ClassLoader là một lớp abstract.

#### 127. Điểm khác nhau giữa một Interface và một lớp Abstract?
Một lớp Abstract là một lớp có thể có các phương thức instance mà triển khai một hành vi mặc định. Một Interface chỉ có thể khai báo các hằng và các phương thức instance, nhưng không thể triển khai hành vi mặc định và tất cả phương thức là abstract ngầm định. Một Interface có tất cả thành viên public và không có trình triển khai.

#### 128. Điều gì xảy ra nếu Static Modifier bị gỡ bỏ từ phương thức main?
Chương trình ném lỗi NoSuchMethodError tại runtime.

#### 129. Giá trị mặc định của một tham chiếu đối tượng được khai báo như là một biến instance?
Giá trị Null, trừ khi nó được khai báo tường minh.

#### 130. Lớp cao nhất có thể là private hoặc protected không?
Không, một lớp cao nhất không thể là private hoặc protected. Nó chỉ có thể là public hoặc không có modifier nào.

#### 131. Tại sao chúng ta cần các lớp wrapper?
Chúng ta có thể truyền chúng ở dạng các tham số phương thức khi một phương thức chờ đợi một đối tượng. Nó cũng cung cấp các phương thức tiện ích.

#### 132. Điểm khác nhau giữa Error và Exception?
Một Error là một điều kiện không thể cứu chữa xuất hiện tại runtime, ví dụ OutOfMemory error. Các Exception là các điều kiện mà xuất hiện là do input không phù hợp, hoặc sai, … ví dụ FileNotFoundException sẽ bị ném nếu file đã cho không tồn tại.

#### 133. Có cần thiết để mỗi khối try phải được theo sau bởi một khối catch không?
Không cần thiết để mỗi khối try phải được theo sau bởi một khối catch. Mỗi khối try nên được theo sau bởi hoặc một khối catch hoặc một khối finally.

#### 134. Khi một Thread được tạo và bắt đầu, trạng thái ban đầu (initial state) của nó là gì?
Một Thread sau khi được tạo và được bắt đầu, nó trong trạng thái sẵn sàng (ready state).

#### 135. Lớp Locale là gì?
Lớp Locale được sử dụng để thiết kế đầu ra output của chương trình theo các qui ước của một khu vực địa lý, chính trị, hoặc văn hóa cụ thể.

#### 136. Phương thức synchronized và lệnh synchronized là gì?
Các phương thức synchronized là các phương thức được sử dụng để điều khiển truy cập tới một đối tượng. Một lệnh synchronized có thể chỉ được thực thi sau khi một Thread đã thu được lock cho đối tượng hoặc lớp được tham chiếu trong lệnh synchronized đó.

#### 137. Gửi phương thức động hoặc đa hình tại runtime là gì?
Gửi phương thức động hoặc đa hình tại runtime là một tiến trình trong đó một lời gọi tới một phương thức bị ghi đè được giải quyết tại runtime thay vì tại compile time. Trong tiến trình này, một phương thức bị ghi đè được gọi thông qua biến tham chiếu của một lớp cha.

#### 138. Dynamic Binding (Late Biding) là gì?
Binding là nói tới việc gắn kết lời gọi một tới code để được thực thi để phản hồi lại lời gọi đó. Dynamic Binding nghĩa là code được liên kết với lời gọi một thủ tục đã cho không được biết cho tới thời điểm của lời gọi đó tại runtime.

#### 139. Constructor có thể được kế thừa không?
Không, Constructor không thể bị kế thừa.

#### 140. Lợi thế của ArrayList so với các mảng?
ArrayList có thể tự động tăng kích cỡ và cung cấp một kỹ thuật chèn và tìm kiếm mạnh mẽ hơn khi so sánh với mảng thông thường.

#### 141. Hoạt động xóa trong LinkedList là nhanh hơn trong ArrayList, tại sao?
Hoạt động xóa trong LinkedList là nhanh hơn bởi vì nó chỉ bao gồm việc cập nhật con trỏ kế tiếp trong node trước node bị xóa và cập nhật con trỏ đằng trước trong node sau node bị xóa.

#### 142. Bạn quyết định khi nào sử dụng ArrayList và LinkedList?
Nếu bạn cần thường xuyên thêm và xóa các phần tử từ giữa danh sách và chỉ truy cập các phần tử theo dãy, thì LinkedList nên được sử dụng. Nếu bạn cần hỗ trợ truy cập ngẫu nhiên, mà không chèn hoặc xóa các phần tử từ bất kỳ vị trí nào khác ngoài vị trí cuối, thì nên sử dụng ArrayList.

#### 143. Một Values Collection View là gì?
Nó là một Collection được trả về bởi phương thức values() của Map Interface. Nó bao gồm tất cả đối tượng hiện diện như là các value trong Map đó.

#### 144. Dot Operator (Toán tử .) là gì?
Dot Operator được sử dụng để truy cập các biến và phương thức instance của các đối tượng lớp. Nó cũng được sử dụng để truy cập các lớp, các package con từ một Package.

#### 145. Bạn có thể sử dụng Private Constructor ở đâu và như thế nào?
Constructor dạng private được sử dụng nếu bạn không muốn các lớp khác khởi tạo đối tượng và để ngăn cản việc xuất hiện các lớp con.

#### 146. Type Casting (Ép kiểu) là gì?
Type Casting (Ép kiểu) nghĩa là xem một biến ở một kiểu này như thể nó là kiểu khác.

#### 147. Miêu tả vòng đời (Life Cycle) của Thread?
Một Thread là một sự thực thi trong một chương trình. Vòng đời của Thread bao gồm:
    Trạng thái Newborn
    Trạng thái Runnable
    Trạng thái Running
    Trạng thái Blocked
    Trạng thái Dead

#### 148. Điểm khác nhau giữa hai toán tử >> và >>> ?
Toán tử >> mang sign bit khi dịch chuyển sang phải. Toán tử >>> điền bit 0 khi đã được dịch chuyển.

#### 149. Phương thức nào của lớp Component được sử dụng để thiết lập vị trí và kích cỡ của một component?
Sử dụng phương thức setBounds() cho mục đích này.

#### 150. Dãy giá trị của kiểu short?
Dãy giá trị của kiểu short là từ -(2^15) tới 2^15 - 1.

#### 151. Lớp cha gần nhất của Menu?
Là lớp MenuItem.

#### 152. Java có cho phép các tham số mặc định không?
Java không cho phép các tham số mặc định (Default Argument).

#### 153. Trong Java, hệ cơ số nào được biểu thị với số 0 bắt đầu?
Hệ cơ số 8, ví dụ: 06

#### 154. Trong Java, hệ cơ số nào được biểu thị với phần bắt đầu là 0x hoặc 0X?
Hệ thập lục phân, ví dụ: 0XF.

#### 155. Lệnh break có thể được sử dụng như là các nhãn (label) trong Java?
Có, ví dụ như break one;

#### 156. Lệnh import được sử dụng ở đâu trong một chương trình Java?
Lệnh import được sử dụng ở phần đầu chương trình sau lệnh package.

#### 157. Giải thích phương thức suspend() dưới lớp Thread?
Nó được sử dụng để tạm dừng sự thực thi của Thread.

#### 158. Giải thích phương thức isAlive() dưới lớp Thread?
Nó được sử dụng để tìm xem có hay không một Thread là vẫn đang chạy.

#### 159. Bạn hiểu gì về phương thức currentThread()?
Đây là một phương thức public và static để thu nhận một tham chiếu tới Thread hiện tại.

#### 160. Giải thích main thread dưới sự thực thi của lớp Thread?
Main thread được tạo tự động và nó bắt đầu thực thi ngay khi một chương trình bắt đầu. Nó là một thread mà từ đó hình thành tất cả thread con khác.

#### 161. Vòng đời của một Applet?
Vòng đời của một Applet gồm:
    Khởi tạo
    Bắt đầu
    Dừng
    Hủy
    Vẽ

#### 162. Vai trò của phương thức init() dưới Applet?
Nó khởi tạo Applet và là phương thức đầu tiên được gọi.

#### 163. Phương thức nào được gọi bởi lớp Applet để tải một hình ảnh?
Sử dụng phương thức getImage(URL của đối tượng, tên file).

#### 164. Định nghĩa phần code được sử dụng như là một thuộc tính của Applet?
Nó được sử dụng để xác định tên của lớp Applet.

#### 165. Canvas là gì?
Nó là một bề mặt bản vẽ đơn giản mà được sử dụng để vẽ các hình ảnh hoặc để thực hiện các hoạt động đồ họa khác.

#### 166. Định nghĩa Lập trình mạng?
Nó nói tới việc viết các chương trình mà thực thi qua nhiều thiết bị (máy tính), trong đó các thiết bị được kết nối với nhau bởi sử dụng mạng.

#### 167. Socket là gì?
Socket cung cấp kỹ thuật giao tiếp giữa hai máy tính bởi sử dụng TCP. Một chương trình Client tạo một Socket trên đầu giao tiếp của nó và cố gắng kết nối Socket đó tới một Server.

#### 168. Lợi thế của Java Socket?
Lập trình dựa trên Socket hiệu quả có thể dễ dàng được triển khai cho truyền thông chung. Các Socket là linh động và nó làm lưu lượng truyền qua mạng ít hơn.

#### 169. Hạn chế của Java Socket?
Truyền thông dựa trên Socket chỉ cho phép gửi các gói dữ liệu thô giữa các ứng dụng. Cả Clietn-Side và Server-Side phải cung cấp các kỹ thuật để làm cho dữ liệu đó có thể dùng được trong bất cứ cách thức nào.

#### 170. Lớp nào được sử dụng bởi các ứng dụng Server để thu nhận một cổng (port) và các yêu cầu từ Client?
Lớp java.net.ServerSocket được sử dụng cho mục đích này.

#### 171. Lớp nào biểu diễn Socket mà cả Server và Client sử dụng để giao tiếp với nhau?
Đó là lớp java.net.Socket.

#### 172. Tại sao Generic được sử dụng trong Java?
Generic cung cấp tính an toàn kiểu tại compile-time mà cho phép lập trình viên để bắt các kiểu không hợp lệ tại thời gian biên dịch. Các phương thức Generic và các lớp Generic trong Java cho phép lập trình viên xác định, với một khai báo phương thức đơn, một tập hợp các phương thức liên quan, hoặc với một khai báo lớp đơn là một tập hợp các kiểu liên quan.

#### 173. Bạn cần thiết lập các biến môi trường nào trên thiết bị để có thể chạy các chương trình Java?
Hai biến môi trường CLASSPATH và PATH.

#### 174. Có cần thiết phải nhập java.lang package không?
Không. Nó được tải theo mặc định bởi JVM.

#### 175. Lớp cao nhất được lồng là gì?
Nếu một lớp được khai báo bên trong một lớp và xác định Static Modifier, bộ biên dịch xem lớp đó giống như bất cứ lớp cao nhất nào khác. Lớp cao nhất bị lồng là một lớp Inner.

#### 176. Trình bày Externalizable Interface?
Externalizable là một Interface chứa hai phương thức readExternal và writeExternal. Hai phương thức này cung cấp cho bạn một điều khiển thông qua kỹ thuật Serialization.

#### 177. Khối finally sẽ vẫn thực thi nếu như có System.exit(0); được viết ở cuối khối try?
Trong trường hợp này, khối finaaly sẽ không thực thi, bởi vì khi bạn cung cấp System.exit(0); thì điều khiển ngay lập tức thoát khỏi chương trình đó, và vì thế khối finally này sẽ không bao giờ thực thi.

#### 178. Bạn hiểu gì về Daemon Thread?
Daemon Thread là một Thread có quyền ưu tiên thấp, chạy không liên tục trong Background thực hiện hoạt động của trình dọn rác cho Java Runtime System.

#### 179. Phương thức được sử dụng để tạo Daemon Thread?
Phương thức setDaemon được sử dụng để tạo một Daemon Thread.

#### 180. Tất cả Thread phải triển khai phương thức nào?
Tất cả tác vụ phải triển khai phương thức run().

#### 181. Lớp GregorianCalendar là gì?
Lớp GregorianCalendar cung cấp sự hỗ trợ Western Calendar truyền thống.

#### 182. Bạn hiểu gì về lớp SimpleTimeZone?
Lớp SimpleTimeZone cung cấp sự hỗ trợ cho một Gregorian Calendar.

#### 183. Điểm khác nhau giữa hai tham số size và capacity của một Vector?
Tham số size là số phần tử thực sự được lưu giữ trong Vector đó, trong khi capacity là số phần tử tối đa nó có thể lưu giữ tại một thời điểm nào đó.

#### 184. Một Vector có thể chứa các đối tượng hỗn tạp không?
Có, một Vector có thể chứa các đối tượng hỗn tạp. Bởi vì một Vector lưu trữ mọi thứ theo khái niệm Đối tượng.

#### 185. Trình bày Enumeration?
Một Enumeration là một Interface chứa các phương thức để truy cập cấu trúc dữ liệu lớp dưới mà từ đó Enumeration được thu nhận. Nó cho phép sự truy cập liên tiếp tới tất cả phần tử được lưu trữ trong Collection đó.

#### 186. Path và Classpath khác nhau ở điểm nào?
Cả Path và Classpath đều là các biến môi trường của hệ điều hành. Path là các định nghĩa từ đó hệ thống có thể tìm thấy các file có thể thực thi (với đuôi .exe) và Classpath được sử dụng để xác định vị trí của .class file.

#### 187. Một lớp được khai báo là private có thể được truy cập từ bên ngoài package của nó không?
Không.

#### 188. Ràng buộc nào phải được tuân theo trên một phương thức static hoặc một khối static?
Một phương thức static không nên tham chiếu tới các biến instance mà không tạo một instance và không thể sử dụng toán tử this để tham chiếu Instance đó.

#### 189. Một Interface có thể kế thừa Interface khác không?
Có. Một Interface có thể kế thừa Interface khác, từ đó một Interface có thể kế thừa nhiều hơn một Interface.

#### 190. Ghi đè và nạp chồng là dựa trên khái niệm hướng đối tượng nào?
Đó là tính đa hình (Polymorphism)

#### 191. Lock của một đối tượng là gì và các đối tượng nào có lock?
Một lock của đối tượng là một kỹ thuật được sử dụng bởi nhiều Thread để thu được truy cập được đồng bộ hóa (synchronized) tới đối tượng đó. Một Thread có thể thực thi một phương thức synchronized của một đối tượng chỉ sau khi nó đã giành được lock của đối tượng đó.

#### 192. Khái niệm Downcasting là gì?
Nó là ép kiểu từ một kiểu chung thành một kiểu cụ thể hơn, ví dụ: ép kiểu xuống theo cấu trúc thứ bậc.

#### 193. Thứ tự độ ưu tiên và Associativity là gì và cách chúng được sử dụng?
Độ ưu tiên quyết định thứ tự trong đó toán tử được ước lượng trong các biểu thức. Associativity xác định xem một biểu thức là được tính toán từ trái-qua-phải hay từ phải-qua-trái.

#### 194. Nếu một phương thức được khai báo là protected, thì phương thức đó có thể được truy cập ở đâu?
Một phương thức protected chỉ có thể được truy cập bởi các lớp hoặc Interface của cùng package hoặc bởi các lớp con của lớp trong đó nó được khai báo.

#### 195. Điểm khác nhau giữa Inner Class và Nested Class?
Khi một lớp được định nghĩa bên trong một phạm vi của lớp khác, thì nó trở thành Inner Class. Nếu Access Modifier của Inner Class là static, thì nó trở thành Nested Class.

#### 196. Bạn cần chú ý điều gì khi thực hiện ghi đè phương thức?
Các phương thức bị ghi đè phải có cùng tên, danh sách tham số, và kiểu trả về. Phương thức ghi đè không thể giới hạn sự truy cập của phương thức nó ghi đè.

#### 197. Chuỗi Constructor (hay Constructor Chaining) là gì và cách thực hiện nó trong Java?
Một Constructor của đối tượng con đầu tiên luôn luôn cần để xây dựng cha của nó. Trong Java, điều này được thực hiện thông qua một lời gọi ngầm định tới constructor (không có tham số) như là lệnh đầu tiên.

#### 198. Có thể ép kiểu giá trị double thành một byte được không?
Có.

#### 199. Cách một lệnh try quyết định mệnh đề catch nào nên được sử dụng để xử lý một Exception?
Khi một Exception được ném bên trong thân khối lệnh try, thì các mệnh đề catch của lệnh try đó được kiểm tra. Mệnh đề catch đầu tiên nào có khả năng xử lý Exception đó sẽ được thực thi. Các mệnh đề catch còn lại được bỏ qua.

#### 200. Các giá trị mặc định của tất cả phần tử trong một mảng khi được định nghĩa như là một biến instance là gì?
Nếu mảng là một mảng các kiểu cơ sở (primitive type), thì tất cả phần tử của mảng đó sẽ được khởi tạo với giá trị mặc định tương ứng với kiểu cơ sở đó.


Tham khảo:
- [69 câu hỏi phỏng vấn về Spring (Phần 1)](https://codeaholicguy.com/2016/01/28/69-cau-hoi-phong-van-ve-spring-phan-1/)
- [69 câu hỏi phỏng vấn về Spring (Phần 2)](https://codeaholicguy.com/2016/02/02/69-cau-hoi-phong-van-ve-spring-phan-2/)
- [69 câu hỏi phỏng vấn về Spring (Phần cuối)
)](https://codeaholicguy.com/2016/02/04/69-cau-hoi-phong-van-ve-spring-phan-cuoi//)
- [Các câu hỏi phỏng vấn Java Spring cho vị trí Java Developer](https://vn.bitdegree.org/huong-dan/java-spring/)
- [Top 70 câu hỏi và câu trả lời về Spring Boot khi phỏng vấn](https://hocspringboot.net/2021/04/18/top-70-cau-hoi-va-cau-tra-loi-ve-spring-boot-khi-phong-van/)
- [Tổng hợp câu hỏi phỏng vấn JAVA - Java Interview Question](https://giai-ma.blogspot.com/2017/04/ngan-hang-cau-hoi-phong-van-ngon-ngu.html)
- [Top 10 câu hỏi phỏng vấn Java thường gặp](https://techtalk.vn/top-10-cau-hoi-phong-van-java-thuong-gap.html)
- [Top 22 câu hỏi phỏng vấn thường gặp & câu trả lời hoàn hảo (Mọi ngành)](https://boxxv.github.io/2019/05/19/top-20-questions-interview-and-asked/)
- [200 câu hỏi phỏng vấn Java hay thường gặp, có đáp án tham khảo](https://quantrimang.com/200-cau-hoi-phong-van-java-hay-thuong-gap-co-dap-an-144832)
- [200 Câu hỏi phỏng vấn Java](https://vietjack.com/cau_hoi_phong_van_java/phan_20.jsp)
- [201 câu hỏi phỏng vấn Java Core](https://viettuts.vn/interview/list-cau-hoi-phong-van-java-core)
- [Kinh nghiệm đi phỏng vấn cho sinh viên IT mới ra trường - Phần 1](https://viblo.asia/p/kinh-nghiem-di-phong-van-cho-sinh-vien-it-moi-ra-truong-phan-1-924lJOxb5PM)
- [https://viblo.asia/tags/java](https://viblo.asia/tags/java)
