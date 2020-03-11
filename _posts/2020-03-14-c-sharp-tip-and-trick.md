---
layout: post
title: C# Programming Tips & Tricks
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
tags:
- Csharp
- Tips
- Tricks
- Coding Conventions
modified: 2019-05-13
---



### 1 A

Khi chúng ta nói về ghi Log, theo truyền thống, chúng ta có nghĩa là lưu tin nhắn vào một tệp. Đó thực sự là ghi Log, nhưng còn nhiều các loại ghi Log duy nhất này. Dưới đây là một số mục tiêu ghi Log phổ biến để xem xét:
- **Database**. Ghi Log vào cơ sở dữ liệu có nhiều lợi thế
  * Bạn có thể truy xuất Log từ bất cứ đâu mà không cần truy cập vào máy sản xuất.
  * Nó dễ dàng tổng hợp các bản ghi Log từ nhiều máy.
  * Không có trường hợp nào các bản ghi Log sẽ bị xóa khỏi một máy cục bộ.
  * Bạn có thể dễ dàng tìm kiếm và trích xuất số liệu thống kê từ Log. Điều này đặc biệt hữu ích nếu bạn sử dụng ghi Log có cấu trúc.


### 2. B

### 3. Viết phương thức C# tính tổng tất cả các số chẵn trong một mảng số nguyên.
{% highlight js %}
static long TotalAllEvenInts(int[] intArray) {
  return (from i in intArray where i % 2 == 0 select (long)i).Sum();
}
{% endhighlight %}


-----
Tham khảo:
- [Ý Nghĩa Của Từ Khóa Volatile Trong C](https://ktmt.github.io/blog/2013/05/09/y-nghia-cua-tu-khoa-volatile-trong-c/)
