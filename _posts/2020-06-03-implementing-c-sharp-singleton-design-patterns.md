---
layout: post
title: Triển khai mẫu Singleton trong C #
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

Có nhiều cách khác nhau để thực hiện mẫu singleton trong C #. Tôi sẽ trình bày chúng ở đây theo thứ tự ngược lại của sự thanh lịch, bắt đầu với phiên bản thường thấy nhất, không an toàn cho đa luồng, và làm việc với một phiên bản đầy đủ, đơn giản và hiệu suất cao được tải đầy đủ.

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
- Nó không hoạt động trong Java. Điều này có vẻ là một điều kỳ lạ để bình luận, nhưng thật đáng để biết nếu bạn cần mẫu đơn trong Java và các lập trình viên C # cũng có thể là lập trình viên Java. Mô hình bộ nhớ Java không đảm bảo rằng hàm tạo hoàn thành trước khi tham chiếu đến đối tượng mới được gán cho cá thể. Mô hình bộ nhớ Java đã trải qua quá trình làm lại cho phiên bản 1.5, nhưng khóa kiểm tra hai lần vẫn bị phá vỡ sau khi không có biến số biến động (như trong C #).
- Không có bất kỳ rào cản bộ nhớ nào, nó cũng bị phá vỡ trong đặc tả ECMA CLI. Có thể theo mô hình bộ nhớ .NET 2.0 (mạnh hơn thông số ECMA), nó an toàn, nhưng tôi không muốn dựa vào các ngữ nghĩa mạnh hơn đó, đặc biệt là nếu có bất kỳ nghi ngờ nào về an toàn. Làm cho biến đối tượng biến động có thể làm cho nó hoạt động, như các cuộc gọi rào cản bộ nhớ rõ ràng, mặc dù trong trường hợp sau, ngay cả các chuyên gia cũng không thể đồng ý chính xác những rào cản nào được yêu cầu. Tôi có xu hướng cố gắng tránh các tình huống mà các chuyên gia không đồng ý điều gì đúng và điều gì sai!
- Rất dễ mắc sai lầm. Mẫu cần phải khá chính xác như trên - bất kỳ thay đổi đáng kể nào cũng có khả năng ảnh hưởng đến hiệu suất hoặc tính chính xác.
- Nó vẫn không thực hiện tốt như các triển khai sau này.

-----
### 5. Cấu trúc

{% highlight js %}
{% endhighlight %}


-----
### 6. Cách sử dụng mẫu Singleton trong C#

{% highlight js %}
using System;

namespace Singleton
{
    // The Singleton class defines the `GetInstance` method that serves as an
    // alternative to constructor and lets clients access the same instance of
    // this class over and over.
    class Singleton
    {
        // The Singleton's constructor should always be private to prevent
        // direct construction calls with the `new` operator.
        private Singleton() { }

        // The Singleton's instance is stored in a static field. There there are
        // multiple ways to initialize this field, all of them have various pros
        // and cons. In this example we'll show the simplest of these ways,
        // which, however, doesn't work really well in multithreaded program.
        private static Singleton _instance;

        // This is the static method that controls the access to the singleton
        // instance. On the first run, it creates a singleton object and places
        // it into the static field. On subsequent runs, it returns the client
        // existing object stored in the static field.
        public static Singleton GetInstance()
        {
            if (_instance == null)
            {
                _instance = new Singleton();
            }
            return _instance;
        }

        // Finally, any singleton should define some business logic, which can
        // be executed on its instance.
        public static void someBusinessLogic()
        {
            // ...
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // The client code.
            Singleton s1 = Singleton.GetInstance();
            Singleton s2 = Singleton.GetInstance();

            if (s1 == s2)
            {
                Console.WriteLine("Singleton works, both variables contain the same instance.");
            }
            else
            {
                Console.WriteLine("Singleton failed, variables contain different instances.");
            }
        }
    }
}
{% endhighlight %}

-----
### 7. Thread-safe Singleton

{% highlight js %}
using System;
using System.Threading;

namespace Singleton
{
    // This Singleton implementation is called "double check lock". It is safe
    // in multithreaded environment and provides lazy initialization for the
    // Singleton object.
    class Singleton
    {
        private Singleton() { }

        private static Singleton _instance;

        // We now have a lock object that will be used to synchronize threads
        // during first access to the Singleton.
        private static readonly object _lock = new object();

        public static Singleton GetInstance(string value)
        {
            // This conditional is needed to prevent threads stumbling over the
            // lock once the instance is ready.
            if (_instance == null)
            {
                // Now, imagine that the program has just been launched. Since
                // there's no Singleton instance yet, multiple threads can
                // simultaneously pass the previous conditional and reach this
                // point almost at the same time. The first of them will acquire
                // lock and will proceed further, while the rest will wait here.
                lock (_lock)
                {
                    // The first thread to acquire the lock, reaches this
                    // conditional, goes inside and creates the Singleton
                    // instance. Once it leaves the lock block, a thread that
                    // might have been waiting for the lock release may then
                    // enter this section. But since the Singleton field is
                    // already initialized, the thread won't create a new
                    // object.
                    if (_instance == null)
                    {
                        _instance = new Singleton();
                        _instance.Value = value;
                    }
                }
            }
            return _instance;
        }

        // We'll use this property to prove that our Singleton really works.
        public string Value { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // The client code.
            
            Console.WriteLine(
                "{0}\n{1}\n\n{2}\n",
                "If you see the same value, then singleton was reused (yay!)",
                "If you see different values, then 2 singletons were created (booo!!)",
                "RESULT:"
            );
            
            Thread process1 = new Thread(() =>
            {
                TestSingleton("FOO");
            });
            Thread process2 = new Thread(() =>
            {
                TestSingleton("BAR");
            });
            
            process1.Start();
            process2.Start();
            
            process1.Join();
            process2.Join();
        }
        
        public static void TestSingleton(string value)
        {
            Singleton singleton = Singleton.GetInstance(value);
            Console.WriteLine(singleton.Value);
        } 
    }
}
{% endhighlight %}


-----
Tham khảo:
- [Singleton Main article](https://refactoring.guru/design-patterns/singleton)
- [Singleton Usage in C#](https://refactoring.guru/design-patterns/singleton/csharp/example#lang-features)
- [Singleton Pattern in C#](https://viblo.asia/p/singleton-pattern-in-c-07LKXA2DZV4)
- [Singleton Design Pattern](https://www.dofactory.com/net/singleton-design-pattern)
- [Implementing the Singleton Pattern in C#](https://csharpindepth.com/Articles/Singleton)
