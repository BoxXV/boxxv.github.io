---
layout: post
title: String concatenate, StringBuilder hay StringBuffer
subtitle: Vì một tương lai lương Java cao ngất
tags:
- Java
- Interview
---
Đây có thể coi là một trong những vấn đề kinh điển khi phỏng vấn Java core. Và theo kinh nghiệm trải qua nhiều cuộc phỏng vấn của mình, những lập trình viên Java có từ 3 năm kinh nghiệm trở lên thì chỉ có khoảng 70% phân biệt được và tỉ lệ sử dụng chính xác(lý giải được lý do và cách sử dụng đúng) chỉ dưới 5%. Tại sao khi cộng String(chuỗi) lại được khuyên sử dụng StringBuilder và StringBuffer? Nên sử dụng StringBuilder hay StringBuffer? Việc sử dụng StringBuilder hay StringBuffer có thực sự cần thiết? Hmmm, theo mình việc sử dụng StringBuilder hay StringBuffer không thật sự “thần thánh” như nhiều người nghĩ và cái cách nhiều người đang dùng rất có vấn đề.

## String là bất khả biến (immutable)
Đây là lý do mà đại đa số mọi người nghĩ rằng là nguyên nhân của các vấn đề trên.
    *Không phải lúc nào đa số cũng đúng
    --- Không rõ ai nói ---*

Tuy nhiên, trong trường hợp này, đa số đã đúng!!! Vậy String bất khả biến như thế nào? Ai cũng nghĩ nó có magic nào đó, nhưng thật ra nó đơn giản hơn mọi người nghĩ rất nhiều.
    Một đối tượng được gọi là bất khả biến(immutable) khi và chỉ khi bạn không thể thay đổi được bất kỳ thuộc tính nào của nó

Với String, thì thuộc tính của nó đại loại là một mảng char. Để không cho phép thay đổi mảng này, có 3kỹ thuật được áp dụng:
- final class
- Để mảng char là private, đảm bảo bên ngoài không thể truy xuất được biến.
- Luôn trả về copy của thuộc tính nếu thuộc tính là một đối tượng khả biến(mutable). Ví dụ thuộc tính của bạn là một mảng, nếu bạn return ra cái mảng này thì bên ngoài vẫn có thể thay đổi phần tử ở bên trong mảng nếu bạn trả về trực tiếp mảng đó

Bạn có thể xem qua cấu trúc của class String của java dưới đây để biết rõ hơn(source code từ Oracle Java SE Development Kit 8u181)

```java
public final class String
implements java.io.Serializable, Comparable, CharSequence {

    private final char value[];
 
    ....
 
    public void getChars(int srcBegin, int srcEnd, char dst[], int dstBegin) {
            if (srcBegin < 0) {
                throw new StringIndexOutOfBoundsException(srcBegin);
            }
            if (srcEnd > value.length) {
                throw new StringIndexOutOfBoundsException(srcEnd);
            }
            if (srcBegin > srcEnd) {
                throw new StringIndexOutOfBoundsException(srcEnd - srcBegin);
            }
            System.arraycopy(value, srcBegin, dst, dstBegin, srcEnd - srcBegin);
        }
 
        ....
 
    public String concat(String str) {
            int otherLen = str.length();
            if (otherLen == 0) {
                return this;
            }
            int len = value.length;
            char buf[] = Arrays.copyOf(value, len + otherLen);
            str.getChars(buf, len);
            return new String(buf, true);
        }
        ....
}
```


### Tại sao String phải bất khả biến?
Để biết câu trả lời, bạn có thể tham khảo [tại đây](https://dzone.com/articles/why-string-immutable-java). Mình xin bổ sung thêm một điều về lợi ích của một class bất khả biến đó là thread-safe. Một đối tượng mà bất khả biến thì bạn sẽ chẳng cần nghĩ ngợi gì khi sử dụng nó trong đa luồng. Đây cũng chính là lý do tại sao đến Java 8, Oracle đã tạo ra Date time API là các đối tượng bất khả biến, thay cho các class về date/time như trước.

Để hiểu rõ hơn, mình có ví dụ dưới đây:

```java
public class TestString {
    public static void main(String[] args) {
        String query = "SELECT first_name, last_name, ";
        query += " age, gender ";
        query += " FROM User WHERE id = ?";
        query += " AND actived = true ";
        query += " AND c = true ";
    }
}
```

Một câu dùng để khởi tạo SQL rất hay thường dùng và thực tế là nhiều dev vẫn code theo cách này. Rất rất nhiều dev(ngạc nhiên là các bạn code có thâm niên từ 2 năm trở lên lại sai nhiều hơn các bạn mới ra trường) đều nhầm tưởng trong trường hợp này Java sẽ dùng method `concat của String`. Nhưng điều đó là sai.

    Tại sao người nhiều kinh nghiệm lại sai nhiều hơn là các bạn trẻ? Vì kiến thức các bạn bị sai từ đầu và các bạn quá lười học tập thêm, không như nhiều bạn trẻ thời nay.

Chúng ta hãy xem Java (từ Java 6 đến Java 8) xử lý nó như thế nào khi compile:

```java
public class TestString {
    public TestString();
    Code:
    0: aload_0
    1: invokespecial #1 // Method java/lang/Object."":()V
    4: return
 
    public static void main(java.lang.String[]);
    Code:
    0: ldc #2 // String SELECT first_name, last_name,
    2: astore_1
    3: new #3 // class java/lang/StringBuilder
    6: dup
    7: invokespecial #4 // Method java/lang/StringBuilder."":()V
    10: aload_1
    11: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    14: ldc #6 // String age, gender
    16: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    19: invokevirtual #7 // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
    22: astore_1
    23: new #3 // class java/lang/StringBuilder
    26: dup
    27: invokespecial #4 // Method java/lang/StringBuilder."":()V
    30: aload_1
    31: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    34: ldc #8 // String FROM User WHERE id = ?
    36: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    39: invokevirtual #7 // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
    42: astore_1
    43: new #3 // class java/lang/StringBuilder
    46: dup
    47: invokespecial #4 // Method java/lang/StringBuilder."":()V
    50: aload_1
    51: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    54: ldc #9 // String AND actived = true
    56: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    59: invokevirtual #7 // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
    62: astore_1
    63: new #3 // class java/lang/StringBuilder
    66: dup
    67: invokespecial #4 // Method java/lang/StringBuilder."":()V
    70: aload_1
    71: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    74: ldc #10 // String AND c = true
    76: invokevirtual #5 // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
    79: invokevirtual #7 // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
    82: astore_1
    83: return
}
```

Rất nhiều đối tượng StringBuilder được tạo ra. Đây là giải pháp của Java để xử lý vấn đề khi ta cộng chuỗi vì rõ ràng cái mảng char[] value của String không phải concat như mọi người nghĩ. Java sẽ liên tục tạo ra các instance của StringBuilder sau đó append vào StringBuilder này, bạn cộng chuỗi trên bao nhiêu câu lệnh sẽ có bấy nhiêu đối tượng StringBuilder được tạo ra, với những đoạn cộng chuỗi tiếp theo, hàm append sẽ được sử dụng tiếp. Việc liên tục tạo ra các instance của StringBuilder sẽ khiến JVM tốn nhiều thời gian và bộ nhớ để tạo object đồng thời bắt Garbage Collection(GC) “hốt rác giùm”. Điều này vừa gây chậm chương trình, vừa tạo áp lực hoạt động cho CPU khi GC phải hoạt động liên tục.

(Đến Java 9, Java đã sử dụng `StringConcatFactory.makeConcatWithConstants`, mình cũng chưa có thời gian nghiên cứu, xin hẹn ở những bài viết sau)

Ngoài ra, class String còn một method là concat cũng có thể thực hiện được việc cộng chuỗi. Cách thức hoạt động rất đơn giản. Ví dụ đoạn code:

```java
String a = "V.N.E.X.T";
String b = "JSC";
String c = a.concat(b);
```

Với hàm concat, Java sẽ xử lý bằng cách
1. Tạo ra một mảng char có số ký tự bằng đúng số ký tự của chuỗi a và chuỗi b cộng lại.
2. Copy toàn bộ các phần tử của mảng char của a vào mảng char mới ở bước 1
3. Copy tiếp toàn bộ các phần tử của mảng char của b vào mảng mới của bước 1.
4. Tạo ra một chuỗi mới từ mảng mới của bước 1

Dưới đây là source code(từ Oracle Java SE Development Kit 8u181)

```java
public String concat(String str) {
    int otherLen = str.length();
    if (otherLen == 0) {
        return this;
    }
    int len = value.length;
    char buf[] = Arrays.copyOf(value, len + otherLen);
    str.getChars(buf, len);
    return new String(buf, true);
}
```

Các này cũng không phải là tối ưu vì nó cũng phải tạo ra một String mới, gây tiêu tốn bộ nhớ và việc tạo mảng mới tiêu tốn nhiều thời gian không kém gì giải pháp trên.


## Giải pháp: StringBuilder/StringBuffer dùng một cách chủ động!

Thay vì dùng cách khờ dại như dưới đây

```java
public String makeAnAwesomeString() {
    String text = "";
    for (int i = 0; i < 10_000; i++) {
        text += i;
    }
    return text;
}
```

thì hãy dùng StringBuilder

```java
public String makeAnAwesomeString() {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 10_000; i++) {
        sb.append(i);
    }
    return sb.toString();
}
```

Thay vì dùng mảng char và là bất khả biến như `String, StringBuilder/StringBuffer` dùng mảng byte(String trong Java 9 đã thay mảng char bằng mảng byte, nhưng tính bất khả biến vẫn còn). Khi có sự thay đổi về chuỗi, `StringBuilder/StringBuffer` chỉ đơn giản là thay đổi mảng byte(thay đổi giá trị phần tử) hoặc tạo mảng mới(như cái cách hàm String.concat hoạt động), không liên tục tạo ra các đối tượng mới, giúp giảm thiểu tài nguyên sử dụng và giảm thời gian xử lý.

`StringBuffer` “cùng cha cùng ông nội” với `StringBuilder`, khi nó giống hệt StringBuilder, chỉ khác rằng `StringBuffer` là `thread-safe`(an toàn khi dùng với đa luồng) và "buffer" lại giá trị của toString. Nếu không dùng đa luồng và share object giữa các luồng, đừng dại mà dùng `StringBuffer` thay cho `StringBuilder`, sẽ làm giảm perfomance rất nhiều.


### Không phải lúc nào cũng cần dùng StringBuilder và StringBuffer!!!

Nhiều bạn hiện nay vẫn giữ quan niệm dùng StringBuilder/StringBuffer append mọi lúc mọi nơi, mặc cho mọi hoàn cảnh. Theo mình quan niệm như vậy là sai. Cần hiểu đúng, hiểu đủ để vận dụng linh hoạt, hài hòa giữa perfomance và clean code.

Thông thường, có 2 trường hợp mà mình sẽ tránh dùng 2 class trên:

1. Khi có những giải pháp tối ưu hơn hẳn

Ta có đoạn code sau:

```java
public static void main(String[] args){
    String query = "SELECT first_name, last_name, "
                    + " age, gender "
                    + " FROM User WHERE id = ?";
}
```

Nhiều người sẽ cải tiến đoạn code trên thành như dưới đây:

```java
public static void main(String[] args){
    String query = new StringBuilder()
    .append("SELECT first_name, last_name, ")
    .append(" age, gender ")
    .append(" FROM User WHERE id = ?").toString();
}
```

Mọi người đều nghĩ nếu để cộng chuỗi như ban đầu, Java sẽ lại liên tục tạo ra `StringBuilder` và gọi method `append`. Nhưng sự thật là Java Compiler không “đơn thuần” như mọi người nghĩ. Với đoạn code ban đầu, Java compiler sẽ xử lý thành

```java
public static void main(java.lang.String[]);
    Code:
       0: ldc           #2                  // String SELECT first_name, last_name,  age, gender  FROM User WHERE id = ?
       2: astore_1
       3: return
```

Chỉ một String duy nhất được tạo ra, không StringBuilder, không concat!

Vẫn là đoạn code trên, nhưng ta có thể thêm một số tùy chỉnh:

Cộng thêm một số nguyên:

```java
String query = "SELECT first_name, last_name, "
               + " age, gender "
               + ", "
               + 1000
               + " FROM User WHERE id = ?";
```

Cộng thêm với một biết kiểu bất kỳ:

```java
long number = 1000;
String query = "SELECT first_name, last_name, "
               + " age, gender "
               + ", "
               + number
               + " FROM User WHERE id = ?";
```

Và cuối cùng, vẫn là biến đó, nhưng ta khai báo là final:

```java
final long number = 1000;
String query = "SELECT first_name, last_name, "
               + " age, gender "
               + ", "
               + number
               + " FROM User WHERE id = ?";
```

Ba trường hợp trên thì có 2 trường hợp được compile ra giống nhau(trường hợp 1 và trường hợp 3).

Java Compiler có rất nhiều điều thú vị.

Cân bằng giữa perfomance và clean code, ưu tiên cái nào, hy sinh cái nào luôn là điều trăn trở của nhiều lập trình viên. Nó gần như một trường phái code vậy và mình là người nghiêng về trường phái clean code.

Tại sao clean code lại quan trọng hơn(quan điểm của mình, một Java web developer)? Vì để tăng perfomance, có rất rất nhiều cách, đặc biệt khi code Java web(khác Android), nhưng nếu bạn quá chú tâm vào code sao cho best của best perfomance, khiến code của bạn rối lên đôi khi lại gây cản trở việc tối ưu perfomance bằng các nguồn bên ngoài, đồng thời khó bảo trì(code quá rối), khó sửa lỗi.

Để tăng perfomance, có thể tính đến load balancer, các giải pháp cache(file, Java object, database, html, js, css,….). Cao hơn thì là tùy chỉnh JVM options. “Like a boss” hơn nữa là…nâng cấp phần cứng. OK là chi phí phần cứng sẽ tăng(RAM, CPU, server, cache,…), nhưng đổi lại bạn có một hệ thống ổn định, dễ maintance, dễ nâng cấp, đó mới là những điều mà một ứng dụng Enterprise cần, chứ không phải một chút operation per second(OPS) chênh lệch.

Hơi lạc đề một chút, ta quay lại String với ví dụ dưới đây

```java
// 1. Cộng chuỗi thông thường
"Processing " + size + "files on " + name;

// 2. Dùng StringBuilder
new StringBuilder()
    .append("Processing ")
    .append(size)
    .append("files on ")
    .append(name)
    .toString();

// 3. Dùng MessageFormat
MessageFormat.format("Processing {0} files on {1}", size, name);
```

Với 3 cách trên thì mình lại khuyến khích cách số 3 hơn(dùng `MessageFormat`) mặc dù trên thực tế dùng `MessageFormat` chậm hơn 2 cách trên vài trăm lần. Vì sao? Vì nếu chỉ đoạn code trên thì nó quá nhỏ và dùng `MessageFormat` thì quá đẹp! Chênh lệch xử lý chỉ vài nano giây với chỉ đoạn code trên, ngoài ra Just-in-time(JIT) compiler của Java có nhiều cách xử lý rất độc đáo khi những đoạn code trên chạy trong cả một hệ thống thực tế. Lúc đó thì chưa biết “mèo nào cắn mỉu nào” đâu.

Chú ý: nếu bạn dùng đoạn trên với log4j, họ đã xây dựng một cách format text riêng để tăng perfomance thay vì chỉ dùng `MessageFormat` đơn thuần. Đoạn code trên khi dùng log, nên được viết như sau:

```java
log.info("Processing {} files on {}", size, name);
```

Ngoài `MessageFormat`, nếu bạn dùng với stream trong java 8 thì có thể thử giải pháp sử dụng String.join/StringJoiner hoặc dùng stream kết hợp StringBuilder, hiệu năng vẫn ổn mà code vẫn gọn gàng.

### Tuy nhiên, sử dụng vòng lặp với số lần lặp rất lớn thì dùng StringBuilder/StringBuffer gần như là bắt buộc.

Với vòng lặp lớn, chắc chắn việc dùng `MessageFormat` hay khiến Java phải liên tục tạo đối tượng `StringBuilder` sẽ rất rất tệ cho perfomance của chương trình. Lúc này thì rõ ràng perfomance là cái rất đáng quan tâm rồi. Bạn vẫn có thể hài hòa bằng cách vẫn dùng 2 class trên, đồng thời sử dụng các biện pháp clean code như `Move Method`, `Move Class` để làm gọn code.


## Kết luận
`String`/`StringBuilder`/`StringBuffer` tưởng đơn giản mà thật ra lại có rất nhiều vấn đề cần tìm hiểu, các bạn nên nghiên cứu kỹ về cấu trúc và cách thức hoạt động của chúng, từ đó biết được cách code tối ưu nhất. Thật tiếc là hiện nay mình chưa có điều kiện làm việc với Java 9, vì Java 9 có cách xử lý String cực kỳ khác so với từ Java 8 trở về trước, đành nợ các bạn ở những bài viết sau.



Tham khảo:
- [String concatenate, StringBuilder hay StringBuffer](https://luanvv.com/blog/string-concatenate-stringbuilder-hay-stringbuffer/)
- [Why String is Immutable in Java](https://dzone.com/articles/why-string-immutable-java)
