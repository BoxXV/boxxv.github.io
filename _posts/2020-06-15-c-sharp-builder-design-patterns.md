---
layout: post
title: Builder Pattern in C#
subtitle: Hướng dẫn C# Design Pattern - Builder
tags:
- Csharp
- Tips
- Tricks
- Singleton
- volatile
- Invoke
- InvokeRequired
---

### 1. Ý Nghĩa

![singleton](http://boxxv.com/img/patterns/singleton.png "singleton")_singleton_

Singleton là một mẫu thiết kế sáng tạo cho phép bạn đảm bảo rằng một lớp chỉ có một đối tượng duy nhất, trong khi cung cấp một điểm truy cập toàn cầu cho đối tượng này.


-----
### 2. Vấn đề
Mẫu Singleton giải quyết hai vấn đề cùng một lúc, vi phạm Nguyên tắc Trách nhiệm duy nhất:
- Đảm bảo rằng một lớp chỉ có một đối tượng duy nhất.
- Cung cấp một điểm truy cập toàn cầu cho trường hợp đó.

Ngày nay, mẫu Singleton đã trở nên phổ biến đến mức mọi người có thể gọi một cái gì đó là singleton ngay cả khi nó chỉ giải quyết được một trong những vấn đề được liệt kê.

-----
### 3. Giải pháp
Tất cả các triển khai của Singleton đều có hai bước chung:
- Đặt hàm tạo mặc định ở chế độ riêng tư, để ngăn các đối tượng khác sử dụng toán tử mới với lớp Singleton.
- Tạo một phương thức tạo tĩnh hoạt động như một hàm tạo. Trong mui xe, phương thức này gọi hàm tạo riêng để tạo một đối tượng và lưu nó trong trường tĩnh. Tất cả các cuộc gọi sau đến phương thức này trả về đối tượng được lưu trữ.

Nếu mã của bạn có quyền truy cập vào lớp Singleton, thì nó có thể gọi phương thức tĩnh Singleton. Vì vậy, bất cứ khi nào phương thức đó được gọi, cùng một đối tượng luôn được trả về.

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
