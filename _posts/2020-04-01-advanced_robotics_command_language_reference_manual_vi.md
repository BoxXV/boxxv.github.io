---
layout: post
title: Advanced Robotics Command Language
subtitle: Omron Reference Guide
tags:
- Tips
- Tricks
---

[Advanced_Robotics_Command_Language_RefMan_en_201701_I617-E-01_tcm849-112545.pdf](http://products.omron.us/Asset/Advanced_Robotics_Command_Language_RefMan_en_201701_I617-E-01_tcm849-112545.pdf)
[i617_advanced_robotics_command_language_reference_manual_en.pdf](https://assets.omron.eu/downloads/manual/en/v1/i617_advanced_robotics_command_language_reference_manual_en.pdf)


### ARCL Reference Guide - Mobile Robots
This is a PDF/print version of the ARCL Reference Guide. A Table of Contents is provided so that you can locate the desired topics. Because the ARCL Reference Guide was designed for online viewing,there may be slight formatting anomalies in the PDF/print version. Addi-tionally, links to external documents will not work in the PDF file.

Đây là phiên bản PDF / in của Hướng dẫn tham khảo ARCL. Mục lục được cung cấp để bạn có thể định vị các chủ đề mong muốn. Vì Hướng dẫn tham khảo ARCL được thiết kế để xem trực tuyến, có thể có sự bất thường về định dạng nhỏ trong phiên bản PDF / in. Ngoài ra, các liên kết đến các tài liệu bên ngoài sẽ không hoạt động trong tệp PDF.

> LƯU Ý: Vui lòng xem tệp ReadMe, được bao gồm trong phần mềm Motivity của bạn, để biết mô tả về mọi thay đổi gần đây.


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

[InvokeHelper.cs](https://github.com/DavidTyler/Door-Lock/blob/master/TwitterDoorLock/InvokeHelper.cs)

https://github.com/search?q=%22void+SetPropertyThreadSafe%22&type=Code

-----
### 4. Sử dụng trình xử lý sự kiện BackgroundWorker

Một cách dễ dàng để thực hiện đa luồng là với thành phần `System.ComponentModel.BackgroundWorker`, sử dụng mô hình hướng sự kiện. Chủ đề Background chạy sự kiện [BackgroundWorker.DoWork](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.dowork?view=netframework-4.8), không tương tác với chủ đề chính. Chuỗi chính chạy các trình xử lý sự kiện [BackgroundWorker.ProgressChanged](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.progresschanged?view=netframework-4.8) và [BackgroundWorker.RunWorkerCompleted](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.runworkercompleted?view=netframework-4.8), có thể gọi các điều khiển của luồng chính.

Để thực hiện cuộc gọi an toàn luồng bằng cách sử dụng [BackgroundWorker](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker?view=netframework-4.8), hãy tạo một phương thức trong luồng background để thực hiện công việc và liên kết nó với sự kiện [DoWork](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.dowork?view=netframework-4.8). Tạo một phương thức khác trong luồng chính để báo cáo kết quả của công việc background và liên kết nó với sự kiện [ProgressChanged](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.progresschanged?view=netframework-4.8) hoặc [RunWorkerCompleted](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.runworkercompleted?view=netframework-4.8). Để bắt đầu chuỗi nền, hãy gọi [BackgroundWorker.RunWorkerAsync](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.runworkerasync?view=netframework-4.8).

Ví dụ sử dụng trình xử lý sự kiện [RunWorkerCompleted](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.backgroundworker.runworkercompleted?view=netframework-4.8) để đặt thuộc tính Text của điều khiển TextBox. Để biết ví dụ sử dụng sự kiện `ProgressChanged`, hãy xem `BackgroundWorker`.

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
- [Multithreading – Lập trình đa luồng, đa tiến trình](https://cameoplus.com/multithreading-lap-trinh-da-luong-da-tien-trinh/)
- [Giới thiệu và hướng dẫn sử dụng Thread và Multi Thread, Process trong visual dot net](https://laptrinhvb.net/bai-viet/chuyen-de-vb-net/Gioi-thieu-va-huong-dan-su-dung-Thread-va-Multi-Thread,-Process-trong-visual-dot-net/a54766b0b5180aa5.html)
- [Threading - Nền tảng lập trình C#](https://www.mastercode.vn/blog/web-development/bai-10-threading-nen-tang-lap-trinh-c.58)


