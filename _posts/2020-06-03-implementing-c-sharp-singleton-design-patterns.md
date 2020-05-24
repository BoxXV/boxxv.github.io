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

Có nhiều cách khác nhau để thực hiện mẫu singleton trong C #. Tôi sẽ trình bày chúng ở đây theo thứ tự ngược lại của sự thanh lịch, bắt đầu với phiên bản thường thấy nhất, không an toàn cho chủ đề, và làm việc với một phiên bản đầy đủ, đơn giản và hiệu suất cao được tải đầy đủ.

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

Như đã nói ở trên, ở trên không phải là chủ đề an toàn. Hai luồng khác nhau có thể cả hai đã đánh giá thử nghiệm `if (instance == null)` và thấy nó là đúng, sau đó cả hai đều tạo ra các trường hợp vi phạm mẫu đơn. Lưu ý rằng trong thực tế, thể hiện có thể đã được tạo trước khi biểu thức được ước tính, nhưng mô hình bộ nhớ không đảm bảo rằng giá trị mới của cá thể sẽ được nhìn thấy bởi các luồng khác trừ khi các rào cản bộ nhớ phù hợp đã được thông qua.


-----
### 3. Second version - simple thread-safety

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

-----
### 4. Tương tự thế giới thực
Chính phủ là một ví dụ tuyệt vời của mô hình Singleton. Một quốc gia chỉ có thể có một chính phủ. Bất kể danh tính cá nhân của các cá nhân thành lập chính phủ, tiêu đề, Chính phủ của X, là một điểm truy cập toàn cầu xác định nhóm người phụ trách.

-----
### 5. Cấu trúc
![Structure](http://boxxv.com/img/patterns/structure-en.png "Structure")_Structure_


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
