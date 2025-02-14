---
layout: post
title: 17 lời khuyên từ một nhà phát triển .NET cao cấp
subtitle: 17 Tips from a Senior .NET Developer
date: 2025-02-12 11:00:00
tags:
- .NET
- Senior
- Tips
---

10 năm trong lĩnh vực phát triển .NET đã dạy tôi nhiều điều hơn là chỉ viết mã sạch.

- [Giới thiệu](#giới-thiệu)
- [1. Làm chủ lập trình bất đồng bộ](#1-làm-chủ-lập-trình-bất-đồng-bộ)
- [2. Dependency Injection là Không thể thương lượng](#2-dependency-injection-là-không-thể-thương-lượng)
- [3. Sử dụng Records và Immutable Types](#3-sử-dụng-records-và-immutable-types)
- [4. Tận dụng Pattern Matching](#4-tận-dụng-pattern-matching)
- [5. Tránh lạm dụng Reflection](#5-tránh-lạm-dụng-reflection)
- [6. Tối ưu hóa truy vấn LINQ](#6-tối-ưu-hóa-truy-vấn-linq)
- [7. Ưu tiên nội suy chuỗi hơn là nối chuỗi](#7-ưu-tiên-nội-suy-chuỗi-hơn-là-nối-chuỗi)
- [8. Thận trọng khi xử lý ngoại lệ](#8-thận-trọng-khi-xử-lý-ngoại-lệ)
- [9. Tránh tối ưu hóa sớm](#9-tránh-tối-ưu-hóa-sớm)
- [10. Sử dụng `Span<T>` và `Memory<T>` cho các tình huống hiệu suất cao](#10-sử-dụng-spant-và-memoryt-cho-các-tình-huống-hiệu-suất-cao)
- [11. Ghi nhật ký mọi thứ, nhưng phải khôn ngoan](#11-ghi-nhật-ký-mọi-thứ-nhưng-phải-khôn-ngoan)
- [12. Bảo mật ứng dụng .NET của bạn](#12-bảo-mật-ứng-dụng-net-của-bạn)
- [13. Hiểu các công cụ lập hồ sơ hiệu suất .NET](#13-hiểu-các-công-cụ-lập-hồ-sơ-hiệu-suất-net)
- [14. Luôn viết các bài kiểm tra đơn vị](#14-luôn-viết-các-bài-kiểm-tra-đơn-vị)
- [15. Sử dụng Source Generator](#15-sử-dụng-source-generator)
- [16. Sử dụng Minimal API trong .NET 6+](#16-sử-dụng-minimal-api-trong-net-6)
- [17. Tiếp tục học hỏi và chia sẻ kiến ​​thức](#17-tiếp-tục-học-hỏi-và-chia-sẻ-kiến-thức)
- [Kết luận](#kết-luận)


## Giới thiệu

Cho dù bạn là người mới bắt đầu hay đã có một vài năm kinh nghiệm, những mẹo này đều xuất phát từ kinh nghiệm thực tế — những sai lầm, bài học và bài học khó khăn.

Bài viết trình bày những mẹo và thủ thuật hay nhất mà tôi đã thu thập được trong nhiều năm.

## 1. Làm chủ lập trình bất đồng bộ

Khi tôi bắt đầu với .NET, async/await đang trở nên phổ biến. Tôi nhớ đã viết API đồng bộ ở khắp mọi nơi, chỉ để thấy chúng sụp đổ dưới tải. Chuyển sang lập trình async trong C# đã thay đổi mọi thứ. Sử dụng `Task.Run` một cách khôn ngoan, tránh `async void` và luôn tận dụng `ConfigureAwait(false)` trong mã thư viện.

Ví dụ:

```csharp
public async Task<string> FetchDataAsync(HttpClient client)
{
    var response = await client.GetAsync("https://api.example.com/data");
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
}
```

## 2. Dependency Injection là Không thể thương lượng

Tôi đã từng làm việc trên một dự án .NET Framework cũ với các dependency được mã hóa cứng. Việc tái cấu trúc để sử dụng Dependency Injection (DI) rất đau đớn nhưng lại mở mang tầm mắt. DI giúp mã của bạn có thể kiểm tra được và có tính mô-đun.

Ví dụ:

```csharp
public interface IDataService
{
    string GetData();
}
```

Đăng ký nó vào vùng chứa DI của bạn:

```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddScoped<IDataService, DataService>();
```

## 3. Sử dụng Records và Immutable Types

Khi C# 9 giới thiệu records, tôi nhận ra mình đã viết bao nhiêu lớp boilerplate không cần thiết. Ưu tiên records cho các cấu trúc dữ liệu không thay đổi.

Ví dụ:

```csharp
public record Person(string Name, int Age);
```

Tính năng này sẽ tự động tạo ra các kiểm tra tính bình đẳng và tính bất biến cho bạn.

## 4. Tận dụng Pattern Matching

Pattern matching trong C# là một công cụ thay đổi cuộc chơi. Tôi đã thấy các cơ sở mã chứa đầy các khối `if-else` không cần thiết có thể sạch hơn với pattern matching.

Ví dụ:

```csharp
static string GetMessage(object obj) => obj switch
{
    int number => $"Number: {number}",
    string text => $"Text: {text}",
    _ => "Unknown type"
};
```

## 5. Tránh lạm dụng Reflection

Reflection rất mạnh mẽ, nhưng nó đi kèm với chi phí hiệu suất. Vào giai đoạn đầu sự nghiệp, tôi đã lạm dụng reflection để gọi các phương thức một cách động, chỉ để sau đó hối hận. Nếu bạn có thể đạt được điều gì đó với generics hoặc interfaces, hãy làm điều đó thay thế.

Ví dụ tệ:

```csharp
var method = typeof(MyClass).GetMethod("MyMethod");
method.Invoke(instance, null);
```

Sử dụng kiểu chung để đảm bảo an toàn về kiểu và hiệu suất tốt hơn.

## 6. Tối ưu hóa truy vấn LINQ

LINQ rất thanh lịch, nhưng sử dụng bất cẩn có thể gây hại cho hiệu suất. Luôn lưu ý đến việc thực thi bị trì hoãn và tránh lặp lại dư thừa.

Ví dụ:

```csharp
var result = myCollection.Where(x => x.IsActive).Select(x => x.Name).ToList();
```

Chỉ nên sử dụng ToList() khi cần thiết để tránh thực hiện truy vấn nhiều lần.

## 7. Ưu tiên nội suy chuỗi hơn là nối chuỗi

Nội suy chuỗi giúp mã của bạn dễ đọc và hiệu quả hơn.

Không tốt:

```csharp
string message = "Hello " + name + "!";
```

Tốt:

```csharp
string message = $"Hello {name}!";
```

## 8. Thận trọng khi xử lý ngoại lệ

Bắt ngoại lệ chung là lỗi thường gặp của người mới bắt đầu. Luôn xử lý ngoại lệ cụ thể và tránh nuốt chúng.

Không tốt:

```csharp
try { /* Code */ }
catch (Exception) { /* Do nothing */ }
```

Tốt:

```csharp
try { /* Code */ }
catch (IOException ex) { Log(ex.Message); }
```

## 9. Tránh tối ưu hóa sớm

Một trong những sai lầm lớn nhất của tôi khi còn là một nhà phát triển mới vào nghề là tối ưu hóa mã quá sớm. Hãy lập hồ sơ mã của bạn trước khi thực hiện thay đổi.

## 10. Sử dụng `Span<T>` và `Memory<T>` cho các tình huống hiệu suất cao

Với .NET Core, `Span<T>` và `Memory<T>` đã cải thiện đáng kể hiệu suất để xử lý dữ liệu lớn.

Ví dụ:

```csharp
Span<int> numbers = stackalloc int[] { 1, 2, 3, 4 };
```

## 11. Ghi nhật ký mọi thứ, nhưng phải khôn ngoan

Ghi nhật ký quá ít thì không tốt, nhưng ghi nhật ký quá nhiều có thể làm tràn nhật ký của bạn. Sử dụng ghi nhật ký có cấu trúc với Serilog hoặc NLog.

## 12. Bảo mật ứng dụng .NET của bạn

Sử dụng `IOptions<T>` để lưu trữ các giá trị cấu hình nhạy cảm thay vì mã hóa cứng các bí mật trong cơ sở mã của bạn.

## 13. Hiểu các công cụ lập hồ sơ hiệu suất .NET

Sử dụng các công cụ như dotTrace và BenchmarkDotNet để đo lường và tối ưu hóa hiệu suất.

## 14. Luôn viết các bài kiểm tra đơn vị

Mọi nhà phát triển có kinh nghiệm đều biết nỗi đau của một thay đổi đột ngột. Luôn viết các bài kiểm tra đơn vị bằng `xUnit` hoặc `NUnit`.

Ví dụ:

```csharp
[Fact]
public void Add_ShouldReturnSum()
{
    int result = Add(2, 3);
    Assert.Equal(5, result);
}
```

## 15. Sử dụng Source Generator

C# 10 giới thiệu các source generator có thể giúp tự động tạo mã lặp lại tại thời điểm biên dịch.

## 16. Sử dụng Minimal API trong .NET 6+

Minimal API giảm bớt boilerplate và đơn giản hóa quá trình phát triển.

Ví dụ:

```csharp
var app = WebApplication.Create();
app.MapGet("/hello", () => "Hello World");
app.Run();
```

## 17. Tiếp tục học hỏi và chia sẻ kiến ​​thức

Tôi nhận ra rằng những nhà phát triển giỏi nhất là những người tiếp tục học hỏi và chia sẻ.

## Kết luận

Trở thành một nhà phát triển .NET cao cấp không chỉ là viết mã; mà còn là viết các ứng dụng có thể bảo trì, hiệu suất cao và an toàn.

-----
Tham khảo:
- [17 Tips from a Senior .NET Developer](https://medium.com/write-a-catalyst/17-tips-from-a-senior-net-developer-fc43b604d8c0?sk=9f98adbb3ce4c34758d0197fb76e6648)
- [25 Advanced LINQ Queries Every .NET Developer Should Know](https://blog.devgenius.io/25-advanced-linq-queries-every-net-developer-should-know-b40079a23923)
- []()