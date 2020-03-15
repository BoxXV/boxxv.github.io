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
1. Phương thức [System.Windows.Forms.Control.Invoke](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.control.invoke), gọi một ủy nhiệm từ luồng chính để gọi điều khiển.
2. Một thành phần [System.ComponentModel.BackgroundWorker](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker?view=netframework-4.8), cung cấp một mô hình hướng sự kiện.

Trong cả hai ví dụ, luồng background sleeps trong một giây để mô phỏng công việc đang được thực hiện trong luồng đó.

Bạn có thể xây dựng và chạy các ví dụ này dưới dạng các ứng dụng .NET Framework từ dòng lệnh C# hoặc Visual Basic. Để biết thêm thông tin, hãy xem [Xây dựng dòng lệnh với csc.exe](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-options/command-line-building-with-csc-exe) hoặc [Build từ dòng lệnh (Visual Basic)](https://docs.microsoft.com/en-us/dotnet/visual-basic/reference/command-line-compiler/building-from-the-command-line).

Bắt đầu với .NET Core 3.0, bạn cũng có thể xây dựng và chạy các ví dụ dưới dạng ứng dụng Windows .NET Core từ một thư mục có tệp .NET Core Windows Forms <tên thư mục>.csproj tệp dự án.

-----
### 3. Sử dụng phương thức Invoke với một delegate

Ví dụ sau đây minh họa một mẫu để đảm bảo các cuộc gọi an toàn luồng cho điều khiển Windows Forms. Nó truy vấn thuộc tính `System.Windows.Forms.Control.InvokeRequired`, so sánh ID luồng tạo của điều khiển với ID luồng gọi. Nếu ID luồng giống nhau, nó gọi điều khiển trực tiếp. Nếu ID luồng khác nhau, nó gọi phương thức `Control.Invoke` với một ủy nhiệm từ luồng chính, thực hiện cuộc gọi thực tế đến điều khiển.

`SafeCallDelegate` cho phép thiết lập thuộc tính Text của điều khiển TextBox. Phương thức `WriteTextSafe` truy vấn [InvokeRequired](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.control.invokerequired?view=netframework-4.8). Nếu `InvokeRequired` trả về `true`, `WriteTextSafe` sẽ chuyển `SafeCallDelegate` sang phương thức `Invoke` để thực hiện cuộc gọi thực tế đến điều khiển. Nếu `InvokeRequired` trả về `false`, `WriteTextSafe` sẽ đặt [TextBox.Text](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.textbox.text?view=netframework-4.8) trực tiếp. Trình xử lý sự kiện `Button1_Click` tạo luồng mới và chạy phương thức `WriteTextSafe`.

{% highlight js %}
using System;
using System.Drawing;
using System.Threading;
using System.Windows.Forms;

public class InvokeThreadSafeForm : Form
{
    private delegate void SafeCallDelegate(string text);
    private Button button1;
    private TextBox textBox1;
    private Thread thread2 = null;

    [STAThread]
    static void Main()
    {
        Application.SetCompatibleTextRenderingDefault(false);
        Application.EnableVisualStyles();
        Application.Run(new InvokeThreadSafeForm());
    }
    public InvokeThreadSafeForm()
    {
        button1 = new Button
        {
            Location = new Point(15, 55),
            Size = new Size(240, 20),
            Text = "Set text safely"
        };
        button1.Click += new EventHandler(Button1_Click);
        textBox1 = new TextBox
        {
            Location = new Point(15, 15),
            Size = new Size(240, 20)
        };
        Controls.Add(button1);
        Controls.Add(textBox1);
    }

    private void Button1_Click(object sender, EventArgs e)
    {
        thread2 = new Thread(new ThreadStart(SetText));
        thread2.Start();
        Thread.Sleep(1000);
    }

    private void WriteTextSafe(string text)
    {
        if (textBox1.InvokeRequired)
        {
            var d = new SafeCallDelegate(WriteTextSafe);
            textBox1.Invoke(d, new object[] { text });
        }
        else
        {
            textBox1.Text = text;
        }
    }

    private void SetText()
    {
        WriteTextSafe("This text was set safely.");
    }
}
{% endhighlight %}

-----
### 4. Sử dụng trình xử lý sự kiện BackgroundWorker

Một cách dễ dàng để thực hiện đa luồng là với thành phần `System.ComponentModel.BackgroundWorker`, sử dụng mô hình hướng sự kiện. Chủ đề Background chạy sự kiện [BackgroundWorker.DoWork](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.dowork?view=netframework-4.8), không tương tác với chủ đề chính. Chuỗi chính chạy các trình xử lý sự kiện [BackgroundWorker.ProgressChanged](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.progresschanged?view=netframework-4.8) và [BackgroundWorker.RunWorkerCompleted](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.runworkercompleted?view=netframework-4.8), có thể gọi các điều khiển của luồng chính.

Để thực hiện cuộc gọi an toàn luồng bằng cách sử dụng BackgroundWorker, hãy tạo một phương thức trong luồng background để thực hiện công việc và liên kết nó với sự kiện DoWork. Tạo một phương thức khác trong luồng chính để báo cáo kết quả của công việc nền và liên kết nó với sự kiện ProgressChanged hoặc RunWorkerCompleted. Để bắt đầu chuỗi nền, hãy gọi BackgroundWorker.RunWorkerAsync.


{% highlight js %}
using System;
using System.ComponentModel;
using System.Drawing;
using System.Threading;
using System.Windows.Forms;

public class BackgroundWorkerForm : Form
{
    private BackgroundWorker backgroundWorker1;
    private Button button1;
    private TextBox textBox1;

    [STAThread]
    static void Main()
    {
        Application.SetCompatibleTextRenderingDefault(false);
        Application.EnableVisualStyles();
        Application.Run(new BackgroundWorkerForm());
    }
    public BackgroundWorkerForm()
    {
        backgroundWorker1 = new BackgroundWorker();
        backgroundWorker1.DoWork += new DoWorkEventHandler(BackgroundWorker1_DoWork);
        backgroundWorker1.RunWorkerCompleted += new RunWorkerCompletedEventHandler(BackgroundWorker1_RunWorkerCompleted);
        button1 = new Button
        {
            Location = new Point(15, 55),
            Size = new Size(240, 20),
            Text = "Set text safely with BackgroundWorker"
        };
        button1.Click += new EventHandler(Button1_Click);
        textBox1 = new TextBox
        {
            Location = new Point(15, 15),
            Size = new Size(240, 20)
        };
        Controls.Add(button1);
        Controls.Add(textBox1);
    }
    private void Button1_Click(object sender, EventArgs e)
    {
        backgroundWorker1.RunWorkerAsync();
    }

    private void BackgroundWorker1_DoWork(object sender, DoWorkEventArgs e)
    {
        // Sleep 2 seconds to emulate getting data.
        Thread.Sleep(2000);
        e.Result = "This text was set safely by BackgroundWorker.";
    }

    private void BackgroundWorker1_RunWorkerCompleted(object sender, RunWorkerCompletedEventArgs e)
    {
        textBox1.Text = e.Result.ToString();
    }
}
{% endhighlight %}


-----
Tham khảo:
- [How to: Make thread-safe calls to Windows Forms controls](https://docs.microsoft.com/en-us/dotnet/framework/winforms/controls/how-to-make-thread-safe-calls-to-windows-forms-controls)
