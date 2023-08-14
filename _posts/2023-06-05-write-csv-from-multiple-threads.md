---
layout: post
title: Ghi vào tệp CSV từ nhiều luồng
subtitle: Writing to CSV-file from multiple threads
image: "img/technology.png"
tags:
- CSV
- CsvHelper
- multi-thread
- .NET
- C#
---

Tôi đang viết [tài liệu và trình xuất siêu dữ liệu](https://gunnarpeipman.com/traverse-hierarchy-optimized/) đọc dữ liệu từ [SharePoint](https://gunnarpeipman.com/sharepoint/) và ghi dữ liệu đó vào nhiều tệp. Tôi cần tăng cường hiệu suất cho trình xuất của mình và tôi đã sử dụng nhiều luồng xử lý dữ liệu từ SharePoint. Một vấn đề tôi gặp phải – ghi siêu dữ liệu vào tệp CSV từ nhiều luồng song song. Bài đăng trên blog này cho biết cách thực hiện bằng cách sử dụng hàng đợi đồng thời.

> Bài đăng này sử dụng thư viện [CsvHelper](https://joshclose.github.io/CsvHelper/) để ghi các đối tượng vào tệp CSV. Lần trước tôi đã đề cập đến thư viện này trong bài đăng trên blog của mình [Tạo tệp CSV trên .NET](https://gunnarpeipman.com/dotnet-csv/).


# Vấn đề: ghi vào tập tin từ nhiều luồng

Tôi có nhiều luồng duyệt qua thư viện tài liệu trên SharePoint và tôi cần tạo nhanh một số báo cáo. Tôi không có tùy chọn để thêm dữ liệu vào một số bộ đệm và xóa nó vào các tệp khi kết thúc dự án vì bộ nhớ máy chủ bị hạn chế.

![multiple-threads](https://boxxv.github.io/img/2023/multiple-threads-one-file.png.webp "multiple-threads")

Những gì tôi cần là một số danh sách an toàn cho luồng (thread-safe) mà tôi có thể đọc từ một luồng khác và nơi các luồng công nhân có thể thêm DTO-s của họ.

Tôi đã có một số cân nhắc:
- Tôi không muốn ràng buộc mã quá chặt với một số khung ghi nhật ký có thể thực hiện công việc.
- Tôi cần một số điểm trong mã để tôi có thể kiểm soát việc đọc và ghi dữ liệu.
- Thay vì mã tùy chỉnh nguyên thủy với khóa luồng, tôi thích thứ gì đó do khung cung cấp hơn.

Với những ý tưởng này trong đầu, tôi bắt đầu xây dựng giải pháp của mình.

## Sử dụng `ConcurrentQueue<T>`

Tôi đã giải quyết vấn đề bằng cách sử dụng `ConcurrentQueue<T>`. Chủ đề thu thập dữ liệu từ thư viện tài liệu SharePoint thêm Đối tượng Truyền Dữ liệu (DTO) vào hàng đợi đồng thời. Tôi không phải lo lắng về các vấn đề phân luồng vì đây là lý do tại sao hàng đợi đồng thời được tạo cho. Tôi cũng đã thêm luồng đọc từ hàng đợi đồng thời và ghi DTO-s vào tệp CSV.

![multiple-threads](https://boxxv.github.io/img/2023/concurrent-queue-reader-file-writer.png.webp "multiple-threads")

Tôi đã viết ứng dụng bảng điều khiển ví dụ để minh họa cho giải pháp của mình. Thật dễ dàng để thử. Xin lỗi vì mã lộn xộn.

{% highlight js %}
class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public double Price { get; set; }
}
 
class Program
{
    private static ConcurrentQueue<Product> _products = new ConcurrentQueue<Product>();
 
    static void Main(string[] args)
    {
        var source = new CancellationTokenSource();
        var token = source.Token;           
 
        Task.Run(() => {
            var conf = new Configuration();
            conf.Encoding = Encoding.UTF8;
            conf.CultureInfo = CultureInfo.InvariantCulture;
 
            using (var stream = File.OpenWrite("products.txt"))
            using (var streamWriter = new StreamWriter(stream))
            using (var writer = new CsvWriter(streamWriter, conf))
            {
                writer.WriteHeader<Product>();
                writer.NextRecord();
 
                while (true)
                {
                    if(token.IsCancellationRequested)
                    {
                        streamWriter.Flush();
                        return;
                    }
 
                    Product product = null;
 
                    while(_products.TryDequeue(out product))
                    {
                        writer.WriteRecord(product);
                        writer.NextRecord();
                    }
                }
            }
        }, token);
 
        var task1 = Task.Run(() => 
        {
            foreach(var number in Enumerable.Range(1, 10))
            {
                var product = new Product
                {
                    Id = number,
                    Name = "Product " + number,
                    Price = Math.Round((10d * number) / DateTime.Now.Second, 2)
                };
 
                _products.Enqueue(product);
 
                Task.Delay(150).Wait();
            }
        });
 
        var task2 = Task.Run(() => 
        {
            foreach (var number in Enumerable.Range(11, 10))
            {
                var product = new Product
                {
                    Id = number,
                    Name = "Product " + number,
                    Price = Math.Round((10d * number) / DateTime.Now.Second, 2)
                };
 
                _products.Enqueue(product);
 
                Task.Delay(150).Wait();
            }
        });
 
        Task.WaitAll(task1, task2);            
 
        Console.WriteLine(Environment.NewLine);
        Console.WriteLine("Press any key to exit ...");
        Console.ReadKey();
 
        source.Cancel();
    }
}
{% endhighlight %}

Mã này hoạt động tốt trong trường hợp của tôi. Đây là tệp CSV chứa thông tin sản phẩm.

![multiple-threads](https://boxxv.github.io/img/2023/concurrentqueue-csv.png.webp "multiple-threads")

Mặc dù tôi đã sử dụng các cài đặt mặc định nhưng thật dễ dàng để định cấu hình CsvWriter để sử dụng các cài đặt mà một người cần.


## Điều gì xảy ra nếu SpinWait quá tích cực?

Một số độc giả thân mến của tôi chỉ ra một điều – việc đọc hàng chờ đồng thời có quá hung hăng không? Chà, không có câu trả lời nào tốt hơn câu trả lời thông thường "còn tùy". Nội bộ `ConcurrentQueue<T>` sử dụng `SpinWait` và điều này là đủ trong trường hợp của tôi. Tuy nhiên, khi nó chạy trống, nó tiêu tốn 25% CPU. `SpinWait` vẫn ổn khi các mục được thêm vào hàng đợi thường xuyên.

Nếu SpinWait trong hàng đợi đồng thời quá căng thẳng thì có thể làm dịu nó xuống một chút khi hàng đợi trống. Tôi đã thêm độ trễ 500 mili giây.

{% highlight js %}
Task.Run(async () => {
    var conf = new Configuration();
    conf.Encoding = Encoding.UTF8;
    conf.CultureInfo = CultureInfo.InvariantCulture;
 
    using (var stream = File.OpenWrite("products.txt"))
    using (var streamWriter = new StreamWriter(stream))
    using (var writer = new CsvWriter(streamWriter, conf))
    {
        writer.WriteHeader<Product>();
        writer.NextRecord();
 
        while (true)
        {
            if(token.IsCancellationRequested)
            {
                streamWriter.Flush();
                return;
            }
 
            Product product = null;
 
            while(_products.TryDequeue(out product))
            {
                writer.WriteRecord(product);
                writer.NextRecord();
            }
 
            // No data, let's delay
            await Task.Delay(500);
        }
    }
}, token);
{% endhighlight %}

Trong trường hợp của tôi, nó làm dịu việc đọc hàng đợi đồng thời. Thay vào đó, trên 25% CPU, nó vẫn ở mức gần 3% khi hàng đợi đồng thời trống.


# IOException: The process cannot access the file ‘file path’ because it is being used by another process

✅ Resolution
✅ Solution 1 -The file may be in use by some other process
✅ Solution 2 – Implements IDisposable for Files handles
✅ Solution 3 – Implement File Lock, Unlock – Thread Synchronization
✅ Solution 4 – Implement a Retry pattern for File processing

-----

## Mô tả vấn đề

Trong khi thực hiện một thao tác trên tệp sẽ tạo ra lỗi như bên dưới,

> IOException:The process cannot access the file 'file' because it is being used by another process.

![IOException](https://boxxv.github.io/img/2023/IOException-The-process-cannot-access-the-file-1024x284.webp "multiple-threads")


## Cách giải quyết

Lỗi này có nghĩa là tệp mà bạn đang cố truy cập không thể truy cập được vì:
- Tệp có thể đang được sử dụng bởi một số quy trình khác.
- Tệp được mở bằng quy trình Riêng (có thể do sự cố mã hóa).
- Thuộc tính tệp được đặt thành không chia sẻ trong khi đọc hoặc ghi tệp.

Sự cố này có thể xảy ra khi thực hiện bất kỳ thao tác nào như
- Đọc
- Viết
- Xóa bỏ

Vấn đề này có thể được giải quyết bằng cách làm theo cẩn thận tất cả các phương pháp có thể dựa trên cách ứng dụng của bạn xử lý các tệp.


### Giải pháp 1 – Tệp có thể đang được sử dụng bởi một số quy trình khác

> Vui lòng đảm bảo xác minh rằng tệp không được mở bởi quy trình khác.

Đây có thể là bất kỳ quy trình cụ thể nào trên hệ thống hoặc chương trình mở tệp tại thời điểm chương trình hoặc ứng dụng của bạn đang sử dụng tệp đó.

Điều quan trọng là cách các phương thức khác nhau đang được sử dụng trong mã. Có nhiều cách để xử lý các thao tác Mở, Tạo, Đọc hoặc ghi tệp.

Một vài ví dụ về các phương thức liên quan đến Tệp nhưng không giới hạn như bên dưới:
- File.Create
- File.Open
- File.ReadAllText()
- File.WriteAllText()
- File.ReadAllLines()
- File.WriteAllLines()

#### Example

```cs
// Create the file, or overwrite if the file exists.

using (FileStream fs = File.Create(path))
{
    byte[] info = new UTF8Encoding(true).GetBytes("This is test file.");

    // Add details to the file.
    fs.Write(info, 0, info.Length);
}
```

**Lưu ý:** Khi sử dụng `File.Create`, xin lưu ý rằng giá trị `FileShare` của `Không` được sử dụng làm hành vi mặc định, tức là không có quy trình hoặc mã nào khác có thể truy cập tệp cho đến khi đóng phần xử lý tệp gốc.

Hiểu việc liệt kê tệp để giải quyết các sự cố truy cập tệp,

Trong khi sử dụng lớp FileStream, bạn có khả năng chỉ định loại quyền truy cập FileShare mà một quy trình khác có thể có trong khi xử lý Xử lý tệp. Lớp FileStream hỗ trợ các loại dưới đây,

- FileShare.ReadWrite
- FileShare.Write
- FileShare.Read
- FileShare.None

Để biết thêm thông tin và các phương pháp hay nhất, vui lòng truy cập bài viết bên dưới.

[How to use File – Code Best practices](https://www.thecodebuzz.com/how-to-use-file-in-best-practices-csharp-dotnet-python/)

> Việc sử dụng đúng cách liệt kê `FileShare` sẽ giúp bạn giải quyết các vấn đề phổ biến nhất khi xử lý tệp.


### Giải pháp 2 – Triển khai `IDisposable` cho các tệp xử lý

Luôn luôn an toàn khi sử dụng câu lệnh “using” trong khi xử lý các tệp thay vì tự tạo và quản lý phiên bản.

Bọc tất cả mã của bạn bên trong câu lệnh "using".

![IOException](https://boxxv.github.io/img/2023/How-to-File-best-practices-File.Create-always-use-using-768x225.webp "multiple-threads")

Để biết thêm thông tin và các phương pháp hay nhất, vui lòng truy cập bài viết bên dưới.

[How to use File – Code Best practices](https://www.thecodebuzz.com/how-to-use-file-in-best-practices-csharp-dotnet-python/)


### Giải pháp 3 – Thực hiện Khóa tệp, Mở khóa – Đồng bộ hóa luồng

- Tệp có thể được truy cập bởi nhiều luồng trong ứng dụng hoặc bởi các luồng quy trình bên ngoài.
- Nếu bạn có nhiều luồng đang cố truy cập vào cùng một tệp, hãy cân nhắc sử dụng cơ chế Đồng bộ hóa bằng Khóa hoặc cơ chế đồng bộ hóa luồng khác.
- Người ta có thể khóa hoặc mở khóa tệp theo yêu cầu xử lý tệp đối với Đọc, Viết hoặc Xóa, v.v.

Để biết thêm thông tin và các phương pháp hay nhất, vui lòng truy cập bài viết bên dưới.

[How to File Lock and Unlock in C# .NET](https://www.thecodebuzz.com/file-lock-unlock-read-write-file-c-sharp-thread-safe-net-core/)


### Giải pháp 4 – Triển khai mẫu Thử lại để xử lý tệp

Điều này không bắt buộc nhưng luôn hữu ích khi xử lý các ngoại lệ đối với tệp hoặc trục trặc tạm thời khi truy cập tệp.

Để biết thêm thông tin và các phương pháp hay nhất, vui lòng truy cập bài viết bên dưới.

[Implement Simple Retry pattern in C# – Resiliency](https://www.thecodebuzz.com/implement-retry-pattern-in-csharp-dotnet-resiliency/)


### Tham khảo:

Để biết thêm thông tin và các phương pháp hay nhất, vui lòng truy cập bài viết bên dưới.

[How to use File – Code Best practices](https://www.thecodebuzz.com/how-to-use-file-in-best-practices-csharp-dotnet-python/)

That’s all! Happy coding!

Điều này có giúp bạn khắc phục sự cố của mình không?

Bạn có giải pháp hay gợi ý nào tốt hơn không? Xin vui lòng tắt ý kiến ​​​​của bạn dưới đây.


# Kết thúc

Thay vì phát minh ra các cơ chế tùy chỉnh để xử lý việc ghi đồng thời vào tệp từ nhiều luồng, chúng ta có thể sử dụng các lớp và thành phần đã có sẵn. CsvHelper là thư viện tuyệt vời với hiệu suất tuyệt vời. Lớp ConcurrentQueue<T> đã giúp chúng tôi kiểm soát việc ghi tệp để điều chỉnh mức sử dụng CPU trong quá trình xuất dữ liệu. Cuối cùng, chúng tôi có giải pháp đơn giản và dễ mở rộng mà chúng tôi cũng có thể sử dụng trong các dự án khác.


-----
Tham khảo:
- [Writing to CSV-file from multiple threads](https://gunnarpeipman.com/write-csv-from-multiple-threads/)
- [IOException: The process cannot access the file ‘file path’ because it is being used by another process](https://www.thecodebuzz.com/file-error-the-process-cannot-access-the-file-because-it-is-being-used-by-another-process/)