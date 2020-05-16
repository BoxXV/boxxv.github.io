---
layout: post
title: Singleton Pattern in C# 
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
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
Tham khảo:
- [Singleton](https://refactoring.guru/design-patterns/singleton)
- [Top 16 C# Programming Tips & Tricks](https://www.vn.freelancer.com/community/articles/top-16-c-programming-tips-tricks)
- [Invoke, InvokeRequired trong C# có nghĩa là gì?](http://diendan.congdongcviet.com/threads/t52293::invoke-invokerequired-trong-csharp-co-nghia-la-gi.cpp)
