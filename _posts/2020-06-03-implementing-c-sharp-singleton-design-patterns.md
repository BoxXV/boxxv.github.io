---
layout: post
title: Triển khai mẫu Singleton trong C#
subtitle: Implementing the Singleton Pattern in C#
tags:
- Csharp
- Tips
- Tricks
- Singleton
- volatile
- Invoke
- InvokeRequired
---

### 1. Introduction

![singleton](http://boxxv.com/img/patterns/singleton.png "singleton")_singleton_

Mẫu singleton là một trong những mẫu được biết đến nhiều nhất trong công nghệ phần mềm. Về cơ bản, singleton là một lớp chỉ cho phép tạo một thể hiện duy nhất của chính nó và thường cung cấp quyền truy cập đơn giản vào thể hiện đó. Thông thường nhất, singletons không cho phép bất kỳ tham số nào được chỉ định khi tạo cá thể - vì nếu không thì yêu cầu thứ hai cho một thể hiện nhưng với một tham số khác có thể có vấn đề! (Nếu cùng một trường hợp nên được truy cập cho tất cả các yêu cầu có cùng tham số, mẫu nhà máy phù hợp hơn.) Bài viết này chỉ đề cập đến tình huống không yêu cầu tham số. Thông thường, một yêu cầu của singletons là chúng được tạo ra một cách lười biếng - tức là trường hợp đó không được tạo cho đến khi nó cần thiết trước tiên.

Có nhiều cách khác nhau để thực hiện mẫu singleton trong C#. Tôi sẽ trình bày chúng ở đây theo thứ tự ngược lại của sự thanh lịch, bắt đầu với phiên bản thường thấy nhất, không an toàn cho đa luồng, và làm việc với một phiên bản đầy đủ, đơn giản và hiệu suất cao được tải đầy đủ.

Tuy nhiên, tất cả các triển khai này đều có chung bốn đặc điểm chung:
- Một constructor duy nhất, là riêng tư và không tham số. Điều này ngăn các lớp khác khởi tạo nó (sẽ vi phạm mẫu). Lưu ý rằng nó cũng ngăn chặn phân lớp - nếu một singleton có thể được phân lớp một lần, nó có thể được phân lớp hai lần và nếu mỗi phân lớp đó có thể tạo một thể hiện, mẫu bị vi phạm. Mẫu nhà máy có thể được sử dụng nếu bạn cần một phiên bản duy nhất của loại cơ sở, nhưng loại chính xác không được biết cho đến khi chạy.
- Lớp học được niêm phong. Điều này là không cần thiết, nói đúng, do quan điểm trên, nhưng có thể giúp JIT tối ưu hóa mọi thứ nhiều hơn.
- Một biến tĩnh chứa tham chiếu đến cá thể được tạo, nếu có.
- Một phương tiện tĩnh công khai để có được tham chiếu đến cá thể được tạo duy nhất, tạo một tham chiếu nếu cần thiết.

Lưu ý rằng tất cả các triển khai này cũng sử dụng Trường hợp thuộc tính tĩnh công khai làm phương tiện truy cập thể hiện. Trong mọi trường hợp, thuộc tính có thể dễ dàng được chuyển đổi thành một phương thức, không ảnh hưởng đến an toàn hoặc hiệu suất của luồng.

-----
### 2. First version - not thread-safe

{% highlight js %}
namespace NonThreadSafe
{
    // Bad code! Do not use!
    public sealed class Singleton
    {
        private static Singleton instance = null;

        private Singleton()
        {
        }

        public static Singleton Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
{% endhighlight %}

Như đã nói ở trên, ở trên không phải là an toàn cho đa luồng. Hai luồng khác nhau có thể cả hai đã đánh giá thử nghiệm `if (instance == null)` và thấy nó là đúng, sau đó cả hai đều tạo ra các trường hợp vi phạm mẫu đơn. Lưu ý rằng trong thực tế, thể hiện có thể đã được tạo trước khi biểu thức được ước tính, nhưng mô hình bộ nhớ không đảm bảo rằng giá trị mới của cá thể sẽ được nhìn thấy bởi các luồng khác trừ khi các rào cản bộ nhớ phù hợp đã được thông qua.


-----
### 3. Second version - simple thread-safety (An toàn luồng)

{% highlight js %}
namespace SimpleThreadSafe
{
    public sealed class Singleton
    {
        private static Singleton instance = null;
        private static readonly object padlock = new object();

        Singleton()
        {
        }

        public static Singleton Instance
        {
            get
            {
                lock (padlock)
                {
                    if (instance == null)
                    {
                        instance = new Singleton();
                    }
                    return instance;
                }
            }
        }
    }
}
{% endhighlight %}

Việc thực hiện này là an toàn luồng. Các luồng lấy ra một khóa trên một đối tượng chia sẻ, và sau đó kiểm tra xem cá thể đã được tạo hay chưa trước khi tạo cá thể. Điều này quan tâm đến vấn đề rào cản bộ nhớ (vì khóa đảm bảo rằng tất cả các lần đọc xảy ra một cách hợp lý sau khi khóa có được và mở khóa đảm bảo rằng tất cả ghi xảy ra một cách hợp lý trước khi phát hành khóa) và đảm bảo rằng chỉ một luồng sẽ tạo ra một thể hiện (như chỉ một luồng có thể nằm trong phần đó của mã tại một thời điểm - tại thời điểm luồng thứ hai nhập vào nó, luồng đầu tiên sẽ tạo ra thể hiện, do đó biểu thức sẽ đánh giá thành sai). Thật không may, hiệu năng bị khóa khi có được khóa mỗi lần yêu cầu.

Lưu ý rằng thay vì khóa trên typeof (Singleton) như một số phiên bản của việc triển khai này, tôi khóa giá trị của một biến tĩnh là riêng tư đối với lớp. Khóa trên các đối tượng mà các lớp khác có thể truy cập và khóa (chẳng hạn như loại) có nguy cơ xảy ra các vấn đề về hiệu năng và thậm chí là bế tắc. Đây là một sở thích kiểu chung của tôi - bất cứ khi nào có thể, chỉ khóa trên các đối tượng được tạo riêng cho mục đích khóa hoặc tài liệu mà chúng sẽ bị khóa cho các mục đích cụ thể (ví dụ: để chờ / đập hàng đợi). Thông thường các đối tượng như vậy nên riêng tư đối với lớp mà chúng được sử dụng. Điều này giúp cho việc viết các ứng dụng an toàn luồng dễ dàng hơn đáng kể.

-----
### 4. Third version - attempted thread-safety using double-check locking

{% highlight js %}
namespace DoubleChecked
{
    // Bad code! Do not use!
    public sealed class Singleton
    {
        private static Singleton instance = null;
        private static readonly object padlock = new object();

        Singleton()
        {
        }

        public static Singleton Instance
        {
            get
            {
                if (instance == null)
                {
                    lock (padlock)
                    {
                        if (instance == null)
                        {
                            instance = new Singleton();
                        }
                    }
                }
                return instance;
            }
        }
    }
}
{% endhighlight %}

Việc triển khai này cố gắng an toàn cho luồng mà không cần phải lấy khóa mỗi lần. Thật không may, có bốn nhược điểm của mẫu:
- Nó không hoạt động trong Java. Điều này có vẻ là một điều kỳ lạ để bình luận, nhưng thật đáng để biết nếu bạn cần mẫu đơn trong Java và các lập trình viên C# cũng có thể là lập trình viên Java. Mô hình bộ nhớ Java không đảm bảo rằng hàm tạo hoàn thành trước khi tham chiếu đến đối tượng mới được gán cho cá thể. Mô hình bộ nhớ Java đã trải qua quá trình làm lại cho phiên bản 1.5, nhưng khóa kiểm tra hai lần vẫn bị phá vỡ sau khi không có biến số biến động (như trong C#).
- Không có bất kỳ rào cản bộ nhớ nào, nó cũng bị phá vỡ trong đặc tả ECMA CLI. Có thể theo mô hình bộ nhớ .NET 2.0 (mạnh hơn thông số ECMA), nó an toàn, nhưng tôi không muốn dựa vào các ngữ nghĩa mạnh hơn đó, đặc biệt là nếu có bất kỳ nghi ngờ nào về an toàn. Làm cho biến đối tượng biến động có thể làm cho nó hoạt động, như các cuộc gọi rào cản bộ nhớ rõ ràng, mặc dù trong trường hợp sau, ngay cả các chuyên gia cũng không thể đồng ý chính xác những rào cản nào được yêu cầu. Tôi có xu hướng cố gắng tránh các tình huống mà các chuyên gia không đồng ý điều gì đúng và điều gì sai!
- Rất dễ mắc sai lầm. Mẫu cần phải khá chính xác như trên - bất kỳ thay đổi đáng kể nào cũng có khả năng ảnh hưởng đến hiệu suất hoặc tính chính xác.
- Nó vẫn không thực hiện tốt như các triển khai sau này.

-----
### 5. Fourth version - not quite as lazy, but thread-safe without using locks

{% highlight js %}
namespace ThreadSafeNotLock
{
    public sealed class Singleton
    {
        private static readonly Singleton instance = new Singleton();

        // Explicit static constructor to tell C# compiler
        // not to mark type as beforefieldinit
        static Singleton()
        {
        }

        private Singleton()
        {
        }

        public static Singleton Instance
        {
            get
            {
                return instance;
            }
        }
    }
}
{% endhighlight %}

Trình static constructor rõ ràng để báo cho trình biên dịch C# không đánh dấu kiểu như `beforefieldinit`

Như bạn có thể thấy, điều này thực sự cực kỳ đơn giản - nhưng tại sao nó lại an toàn cho chủ đề và nó lười đến mức nào? Chà, các hàm tạo tĩnh trong C# được chỉ định để thực thi chỉ khi một thể hiện của lớp được tạo hoặc một thành viên tĩnh được tham chiếu và chỉ thực hiện một lần cho mỗi AppDomain. Cho rằng kiểm tra này cho loại đang được xây dựng mới cần được thực hiện bất cứ điều gì khác xảy ra, nó sẽ nhanh hơn việc thêm kiểm tra bổ sung như trong các ví dụ trước. Tuy nhiên, có một vài nếp nhăn:
- Nó không lười biếng như các triển khai khác. Cụ thể, nếu bạn có các thành viên tĩnh ngoài Instance, tham chiếu đầu tiên cho các thành viên đó sẽ liên quan đến việc tạo cá thể. Điều này được sửa chữa trong việc thực hiện tiếp theo.
- Có những sự phức tạp nếu một hàm tạo tĩnh gọi một cái khác gọi cái đầu tiên một lần nữa. Xem trong thông số kỹ thuật .NET (hiện tại là mục 9.5.3 của phân vùng II) để biết thêm chi tiết về bản chất chính xác của trình khởi tạo kiểu - chúng không thể cắn bạn, nhưng đáng để nhận ra hậu quả của các hàm tạo tĩnh liên quan đến từng hàm khác trong một chu kỳ.
- Sự lười biếng của các trình khởi tạo kiểu chỉ được đảm bảo bởi .NET khi loại không được đánh dấu bằng một cờ đặc biệt có tên là `beforefieldinit`. Thật không may, trình biên dịch C# (như được cung cấp trong thời gian chạy .NET 1.1, ít nhất) đánh dấu tất cả các loại không có hàm tạo tĩnh (nghĩa là một khối trông giống như một hàm tạo nhưng được đánh dấu tĩnh) là `beforefieldinit`. Bây giờ tôi có một bài viết với nhiều chi tiết hơn về vấn đề này. Cũng lưu ý rằng nó ảnh hưởng đến hiệu suất, như được thảo luận ở gần cuối trang.

Một lối tắt bạn có thể thực hiện với cách triển khai này (và chỉ có một phím tắt này) là chỉ tạo một biến chỉ đọc tĩnh công khai và loại bỏ hoàn toàn thuộc tính. Điều này làm cho mã bộ xương cơ bản hoàn toàn nhỏ bé! Tuy nhiên, nhiều người thích có một tài sản trong trường hợp cần thêm hành động trong tương lai và nội tuyến JIT có khả năng làm cho hiệu suất giống hệt nhau. (Lưu ý rằng bản thân hàm tạo tĩnh vẫn được yêu cầu nếu bạn yêu cầu sự lười biếng.)


-----
### 6. Fifth version - fully lazy instantiation

{% highlight js %}
namespace FullyLazy
{
    public sealed class Singleton
    {
        private Singleton()
        {
        }

        public static Singleton Instance { get { return Nested.instance; } }

        private class Nested
        {
            // Explicit static constructor to tell C# compiler
            // not to mark type as beforefieldinit
            static Nested()
            {
            }

            internal static readonly Singleton instance = new Singleton();
        }
    }
}
{% endhighlight %}

Ở đây, khởi tạo được kích hoạt bởi tham chiếu đầu tiên đến thành viên tĩnh của lớp lồng nhau, chỉ xảy ra trong Instance. Điều này có nghĩa là việc thực hiện hoàn toàn lười biếng, nhưng có tất cả các lợi ích hiệu suất của những lần trước. Lưu ý rằng mặc dù các lớp lồng nhau có quyền truy cập vào các thành viên riêng của lớp kèm theo, nhưng điều ngược lại là không đúng, do đó, ví dụ cần phải là nội bộ ở đây. Tuy nhiên, điều đó không gây ra bất kỳ vấn đề nào khác, vì bản thân lớp học là riêng tư. Tuy nhiên, mã phức tạp hơn một chút để làm cho việc khởi tạo trở nên lười biếng.

-----
### 7. Sixth version - using .NET 4's Lazy<T> type

Nếu bạn đang sử dụng .NET 4 (hoặc cao hơn), bạn có thể sử dụng loại System.Lazy <T> để làm cho sự lười biếng thực sự đơn giản. Tất cả những gì bạn cần làm là chuyển một ủy nhiệm cho hàm tạo gọi hàm tạo Singleton - được thực hiện dễ dàng nhất với biểu thức lambda.

{% highlight js %}
using System;

namespace LazyT
{
    public sealed class Singleton
    {
        private static readonly Lazy<Singleton> lazy = new Lazy<Singleton>(() => new Singleton());

        public static Singleton Instance { get { return lazy.Value; } }

        private Singleton()
        {
        }
    }
}
{% endhighlight %}

Nó đơn giản và thực hiện tốt. Nó cũng cho phép bạn kiểm tra xem cá thể đã được tạo hay chưa với thuộc tính `IsValueCreated`, nếu bạn cần điều đó.

Đoạn mã trên hoàn toàn sử dụng `LazyThreadSquilMode.ExecutAndPublication` làm chế độ an toàn luồng cho `Lazy<Singleton>`. Tùy thuộc vào yêu cầu của bạn, bạn có thể muốn thử nghiệm với các chế độ khác.

-----
### Performance vs laziness

Trong nhiều trường hợp, bạn thực sự sẽ không yêu cầu sự lười biếng hoàn toàn - trừ khi việc khởi tạo lớp của bạn làm một việc gì đó đặc biệt tốn thời gian hoặc có một số tác dụng phụ ở nơi khác, có lẽ không nên bỏ qua hàm tạo tĩnh rõ ràng được trình bày ở trên. Điều này có thể tăng hiệu suất vì nó cho phép trình biên dịch JIT thực hiện một kiểm tra duy nhất (ví dụ khi bắt đầu một phương thức) để đảm bảo rằng loại đã được khởi tạo, và sau đó giả sử nó. Nếu cá thể đơn lẻ của bạn được tham chiếu trong một vòng lặp tương đối chặt chẽ, điều này có thể tạo ra sự khác biệt đáng kể (tương đối). Bạn nên quyết định xem có cần phải khởi tạo hoàn toàn lười biếng hay không và ghi lại quyết định này một cách thích hợp trong lớp.

Rất nhiều lý do cho sự tồn tại của trang này là những người cố gắng tỏ ra thông minh, và do đó đưa ra thuật toán khóa được kiểm tra hai lần. Có một thái độ của khóa là đắt tiền là phổ biến và sai lầm. Tôi đã viết một điểm chuẩn rất nhanh, chỉ cần mua các trường hợp đơn lẻ trong một tỷ cách, thử các biến thể khác nhau. Điều đó không khoa học lắm, bởi vì trong cuộc sống thực, bạn có thể muốn biết nó nhanh đến mức nào nếu mỗi lần lặp thực sự liên quan đến một cuộc gọi vào một phương thức tìm nạp đơn, v.v. Tuy nhiên, nó cho thấy một điểm quan trọng. Trên máy tính xách tay của tôi, giải pháp chậm nhất (theo hệ số khoảng 5) là khóa một (giải pháp 2). Nó rất quan trọng? Có lẽ là không, khi bạn nhớ rằng nó vẫn có thể thu được đơn lẻ một tỷ lần trong vòng dưới 40 giây. (Lưu ý: bài viết này ban đầu được viết cách đây khá lâu - Tôi mong đợi hiệu suất tốt hơn bây giờ.) Điều đó có nghĩa là nếu bạn "chỉ" có được đơn vị bốn trăm nghìn lần mỗi giây, chi phí mua lại sẽ tăng đạt 1% hiệu suất - vì vậy việc cải thiện nó sẽ không làm được gì nhiều. Bây giờ, nếu bạn có được singleton thường xuyên - không phải là bạn đang sử dụng nó trong một vòng lặp sao? Nếu bạn quan tâm nhiều đến việc cải thiện hiệu suất một chút, tại sao không khai báo một biến cục bộ bên ngoài vòng lặp, hãy lấy singleton một lần rồi lặp lại. Bingo, ngay cả việc thực hiện chậm nhất cũng trở nên dễ dàng đầy đủ.

Tôi sẽ rất thích thú khi thấy một ứng dụng trong thế giới thực, nơi sự khác biệt giữa sử dụng khóa đơn giản và sử dụng một trong những giải pháp nhanh hơn thực sự tạo ra sự khác biệt đáng kể về hiệu suất.

-----
### Exceptions

Đôi khi, bạn cần thực hiện công việc trong một hàm tạo đơn lẻ có thể tạo ra ngoại lệ, nhưng có thể không gây tử vong cho toàn bộ ứng dụng. Có khả năng, ứng dụng của bạn có thể khắc phục sự cố và muốn thử lại. Sử dụng bộ khởi tạo kiểu để xây dựng singleton trở nên có vấn đề ở giai đoạn này. Các thời gian chạy khác nhau xử lý trường hợp này khác nhau, nhưng tôi không biết bất kỳ điều gì làm điều mong muốn (chạy lại trình khởi tạo kiểu) và ngay cả khi có, mã của bạn sẽ bị hỏng trong các thời gian chạy khác. Để tránh những vấn đề này, tôi khuyên bạn nên sử dụng mẫu thứ hai được liệt kê trên trang - chỉ cần sử dụng một khóa đơn giản và kiểm tra mỗi lần, xây dựng thể hiện trong phương thức / thuộc tính nếu nó chưa được xây dựng thành công.

-----
### Conclusion

Có nhiều cách khác nhau để thực hiện mẫu singleton trong C#. Một độc giả đã viết cho tôi chi tiết một cách anh ta đã gói gọn khía cạnh đồng bộ hóa, điều mà trong khi tôi thừa nhận có thể hữu ích trong một vài tình huống rất đặc biệt (cụ thể là bạn muốn hiệu suất rất cao và khả năng xác định liệu đơn có được hay không được tạo và sự lười biếng hoàn toàn bất kể các thành viên tĩnh khác được gọi). Cá nhân tôi không thấy rằng tình huống sắp tới thường đủ để xứng đáng tiến xa hơn trên trang này, nhưng vui lòng gửi thư cho tôi nếu bạn ở trong tình huống đó.

Sở thích cá nhân của tôi là giải pháp 4: lần duy nhất tôi thường rời xa nó là nếu tôi cần có thể gọi các phương thức tĩnh khác mà không kích hoạt khởi tạo, hoặc nếu tôi cần biết liệu singleton đã được khởi tạo hay chưa. Tôi không nhớ lần cuối cùng tôi ở trong tình huống đó, giả sử tôi thậm chí còn có. Trong trường hợp đó, có lẽ tôi sẽ tìm giải pháp 2, vẫn còn tốt và dễ dàng để có được quyền.

Giải pháp 5 thanh lịch, nhưng phức tạp hơn 2 hoặc 4, và như tôi đã nói ở trên, những lợi ích mà nó cung cấp dường như chỉ hiếm khi hữu ích. Giải pháp 6 là một cách đơn giản hơn để đạt được sự lười biếng, nếu bạn đang sử dụng .NET 4. Nó cũng có một ưu điểm là rõ ràng là lười biếng. Hiện tại tôi có xu hướng vẫn sử dụng giải pháp 4, đơn giản là thông qua thói quen - nhưng nếu tôi làm việc với các nhà phát triển thiếu kinh nghiệm, tôi hoàn toàn có thể tìm giải pháp 6 để bắt đầu như một mô hình dễ áp ​​dụng và phổ biến.

(Tôi sẽ không sử dụng giải pháp 1 vì nó bị hỏng và tôi sẽ không sử dụng giải pháp 3 vì nó không có lợi ích hơn 5.)

-----
Tham khảo:
- [Singleton Main article](https://refactoring.guru/design-patterns/singleton)
- [Singleton Usage in C#](https://refactoring.guru/design-patterns/singleton/csharp/example#lang-features)
- [Singleton Pattern in C#](https://viblo.asia/p/singleton-pattern-in-c-07LKXA2DZV4)
- [Singleton Design Pattern](https://www.dofactory.com/net/singleton-design-pattern)
- [Implementing the Singleton Pattern in C#](https://csharpindepth.com/Articles/Singleton)
