---
layout: post
title: Make thread-safe calls to Windows Forms controls
subtitle: C# Programming Tips & Tricks
tags:
- Csharp
- Tips
- Tricks
- volatile
- Invoke
- InvokeRequired
---

Đa luồng có thể cải thiện hiệu suất của các ứng dụng Windows Forms, nhưng việc truy cập vào các điều khiển của Windows Forms không phải là chủ đề an toàn. Đa luồng có thể làm lộ mã của bạn thành các lỗi rất nghiêm trọng và phức tạp. Hai hoặc nhiều luồng điều khiển một điều khiển có thể buộc điều khiển vào trạng thái không nhất quán và dẫn đến tình trạng race, bế tắc và đóng băng hoặc treo. Nếu bạn triển khai đa luồng trong ứng dụng của mình, hãy nhớ gọi điều khiển đa luồng theo cách an toàn cho luồng. Để biết thêm thông tin, hãy xem [Thực hành tốt nhất về quản lý luồng](https://docs.microsoft.com/en-us/dotnet/standard/threading/managed-threading-best-practices).

Có hai cách để gọi điều khiển Windows Forms một cách an toàn từ một luồng không tạo điều khiển đó. Bạn có thể sử dụng phương thức `System.Windows.Forms.Control.Invoke` để gọi một đại biểu được tạo trong luồng chính, lần lượt gọi điều khiển. Hoặc, bạn có thể triển khai `System.ComponentModel.BackgroundWorker`, sử dụng mô hình hướng sự kiện để tách công việc được thực hiện trong luồng chạy nền khỏi báo cáo kết quả.


### 1. Unsafe cross-thread calls - Cuộc gọi giữa các luồng không an toàn
Sẽ không an toàn khi gọi điều khiển trực tiếp từ một luồng không tạo ra nó. Đoạn mã sau minh họa một cuộc gọi không an toàn đến điều khiển `System.Windows.Forms.TextBox`. Trình xử lý sự kiện `Button1_Click` tạo ra một luồng `WriteTextUnsafe` mới, trực tiếp đặt thuộc tính `TextBox.Text` của luồng chính.
{% highlight js %}
private void Button1_Click(object sender, EventArgs e)
{
    thread2 = new Thread(new ThreadStart(WriteTextUnsafe));
    thread2.Start();
}

private void WriteTextUnsafe()
{
    textBox1.Text = "This text was set unsafely.";
}
{% endhighlight %}

Trình gỡ lỗi Visual Studio phát hiện các cuộc gọi luồng không an toàn này bằng cách đưa ra một `InvalidOperationException` với thông báo, **Cross-thread operation not valid. Control "" accessed from a thread other than the thread it was created on.** InvalidOperationException luôn xảy ra đối với các cuộc gọi đa luồng không an toàn trong quá trình gỡ lỗi Visual Studio và có thể xảy ra khi chạy ứng dụng. Bạn nên khắc phục sự cố, nhưng bạn có thể vô hiệu hóa ngoại lệ bằng cách đặt thuộc tính `Control.CheckForIllegalCrossThreadCalls` thành false.


-----
### 2. Safe cross-thread calls - Cuộc gọi giữa các luồng an toàn

Các ví dụ mã sau đây trình bày hai cách để gọi điều khiển Windows Forms một cách an toàn từ một luồng không tạo ra nó:
1. Phương thức System.Windows.Forms.Control.Invoke, gọi một ủy nhiệm từ luồng chính để gọi điều khiển.
2. Một thành phần System.ComponentModel.BackgroundWorker, cung cấp một mô hình hướng sự kiện.

{% highlight js %}
private void cmdGenerate_Click(object sender, EventArgs e)
{
    // Chuẩn bị
    lstNumber.Items.Clear();
 
    // Tạo và chạy thread
    Thread thrGenerating = new Thread(new ThreadStart(DoWork));
    thrGenerating.Start();
}
 
private void DoWork()
{
    for (int i = 1; i <= 1000; i++)
    {
        // Thêm item vào list qua invoke
        lstNumber.Invoke(new MethodInvoker(delegate()
            {
                lstNumber.Items.Add(i);
                lstNumber.TopIndex = lstNumber.Items.Count - 1;
            }));
 
        // Cập nhật tiến độ qua progress bar
        pgrOperation.Invoke(new MethodInvoker(delegate()
        {
            pgrOperation.Value = (i * 100 / 1000);
        }));
    }
 
    MessageBox.Show("Hoàn tất");
}
{% endhighlight %}

-----
### 3. Viết phương thức C# tính tổng tất cả các số chẵn trong một mảng số nguyên.
{% highlight js %}
static long TotalAllEvenInts(int[] intArray) {
  return (from i in intArray where i % 2 == 0 select (long)i).Sum();
}
{% endhighlight %}

-----
### 4. How to: Make thread-safe calls to Windows Forms controls
{% highlight js %}
private void Button1_Click(object sender, EventArgs e)
{
    thread2 = new Thread(new ThreadStart(WriteTextUnsafe));
    thread2.Start();
}
private void WriteTextUnsafe()
{
    textBox1.Text = "This text was set unsafely.";
}
{% endhighlight %}
[How to: Make thread-safe calls to Windows Forms controls](https://docs.microsoft.com/en-us/dotnet/framework/winforms/controls/how-to-make-thread-safe-calls-to-windows-forms-controls?redirectedfrom=MSDN)



-----
Tham khảo:
- [Ý Nghĩa Của Từ Khóa Volatile Trong C](https://ktmt.github.io/blog/2013/05/09/y-nghia-cua-tu-khoa-volatile-trong-c/)
- [Top 16 C# Programming Tips & Tricks](https://www.vn.freelancer.com/community/articles/top-16-c-programming-tips-tricks)
- [Invoke, InvokeRequired trong C# có nghĩa là gì?](http://diendan.congdongcviet.com/threads/t52293::invoke-invokerequired-trong-csharp-co-nghia-la-gi.cpp)
