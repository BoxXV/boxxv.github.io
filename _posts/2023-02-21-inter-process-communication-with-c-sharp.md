---
layout: post
title: Inter-Process Communication với C#
subtitle: Local Machine Interprocess Communication with .NET
image: "img/technology.png"
tags:
- IPC
- .NET
- C#
---

![IPC](https://boxxv.github.io/img/2023/whats-new-in-aspne.png "IPC")

Để có thể hiểu sau hơn chút về sự giao tiếp này, hãy cùng lật lại về mô hình chúng ta thường làm - mô hình Nguyên Khối (Monolithic Architecture). Chúng ta đều biết, trong mô hình Nguyên Khối, các thành phần đều được liên kết đến nhau thông qua các lời gọi hàm hay các phương thức tùy ngôn ngữ. Điều này làm nó ít hay nhiều phụ thuộc vào ngôn ngữ hoặc chí ít là sẽ phụ thuộc lẫn nhau.

Đi ngược lại với quan điểm xây dựng chung trên cùng một khối, mô hình Microservice lại xây dựng nhiều khối phân tán trên các máy khác nhau. Mà thường mỗi một khối là một quá trình. Do đó các quá trình này sẽ cần một cơ chế giao tiếp giữa các quá trình (Inter-Process Communication hay IPC) này để tương tác được với nhau.

![Microservice](https://boxxv.github.io/img/2023/13cf1604-47c4-41c6-8d66-82e772712ed8.png "Microservice")

Nhìn hình thấy nó liên kết cũng khá lằng nhằng chả khác vẹo gì các mô hình Nguyên Khối lắm nhỉ =))

Nhưng trước tiên muốn hiểu được hình ảnh trên chúng ta cần phải hiểu được giao tiếp giữa các quá trình xảy ra như nào đã 😄


## Kiểu Tương Tác

Khi bạn đã sử dụng IPC cho service của mình, bạn sẽ thấy thích thú khi tìm hiểu về cách nó tương tác với nhau. Nó có nhiểu kiểu được chia theo nhiều cách, nhưng phần lớn đều tuân theo dạng Client - Service.

Chúng có thể chia theo chiều:
- `One to one`: Mỗi yêu cầu của client được xử lý bởi duy nhất một service
- `One to many`: Mỗi yêu cầu của client được xử lý bởi nhiều service

Hoặc chúng có thể chia theo cách xử lý đồng bộ hay bất đồng bộ:
- `Đồng bộ` (Synchronous): Client chỉ đinh thời gian cho phép đợi phản hồi từ dịch vụ, thâm chí có thể chặn luôn luồng trong khi đợi.
- `Bất đồng bộ` (Asynchronous): Client sẽ không chặn trong khi chờ đợi phản hồi, và phản hồi đó không nhất thiết là phải gửi ngay tức thì tại thời điểm đó.

Và tổng hợp cả hai cách chia trên thì chúng ta đã có một số kiểu tương tác thú zị sau:
- One to one with Synchronous: Request/response
- One to one with Asynchronous: Notification hoặc Request/async response
- One to many with Asynchronous: Publish/subscribe hoặc Publish/async responses

Thông thường trong một ứng dụng sử dụng mô hình Microservice sẽ kết hợp các kiểu tương tác này lại với nhau để đạt hiệu quả cao nhất.

Sau đây là một ví dụ về sự kết hợp các cách tương tác của sự giao tiếp các khối dịch vụ này :

![Microservice](https://boxxv.github.io/img/2023/8641d56b-5bfc-417a-8b48-611e1d51840e.png "Microservice")

Điện thoại thông minh hành khách hành khách gửi thông báo đến dịch vụ Quản lý chuyến đi để yêu cầu đón khách. Dịch vụ Quản lý chuyến đi xác minh rằng tài khoản Hành khách đang hoạt động bằng cách sử dụng request/response để gọi Dịch vụ hành khách. Dịch vụ Quản lý chuyến đi sau đó tạo chuyến đi và sử dụng publish/subscribe để thông báo cho các dịch vụ khác bao gồm cả Người điều hành, nơi định vị một tài xế có sẵn.

Tiếp theo sau khi quan tâm đến kiểu tương tác thì chúng ta cần quan tâm đến API, nó như tiếng nói dùng để giao tiếp giữa các khối dịch vụ vậy.


## IPC with C#

Đôi khi, cần có nhiều quy trình (processes) chạy trên cùng một máy để nói chuyện với nhau. Ví dụ, đây là cách để họ có thể đồng bộ hóa hoặc chia sẻ một số loại dữ liệu. Điều này thường được gọi là InterProcess Communication hoặc IPC.

Trong bài đăng này, tôi sẽ đề cập đến một số cách mà mã .NET có thể giao tiếp với mã .NET khác trên cùng một máy. Các kỹ thuật tôi sẽ nói về là:

- [`WCF`](https://learn.microsoft.com/en-us/dotnet/framework/wcf/)
- [`Sockets`](https://learn.microsoft.com/en-us/dotnet/fundamentals/networking/sockets/tcp-classes)
- [`.NET Remoting`](https://learn.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))
- [`Message Queues`](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))
- [`Named Pipes`](https://learn.microsoft.com/en-us/dotnet/standard/io/pipe-operations)
- [`Memory-mapped files`](https://learn.microsoft.com/en-us/dotnet/standard/io/memory-mapped-files)
- [`Event Tracing for Windows`](https://learn.microsoft.com/en-us/windows/win32/etw/event-tracing-portal)
- `Files`
- `COM Interop`
- [`WM_COPYDATA`](https://learn.microsoft.com/en-us/windows/win32/dataxchg/wm-copydata) Win32 message

Bạn có thể nhận thấy rằng tôi sẽ chỉ nói về nội dung gốc của Windows/.NET, không có thư viện hoặc dịch vụ bổ sung nào. Tất nhiên, hãy nhớ rằng mã tôi sắp trình bày chỉ là bằng chứng về khái niệm, nếu nó được sử dụng trong các ứng dụng thực tế, nó sẽ cần một số cải tiến.

Đây là một bài viết dài, hãy cẩn thận!

**Contracts**

Vì vậy, chúng ta sẽ có một giao diện mô tả phía máy khách ( IIpcClient ) và một giao diện khác mô tả phía máy chủ ( IIpcServer ). Định nghĩa của họ là:

```cs
[ServiceContract]
public interface IIpcClient
{
    [OperationContract(IsOneWay = true)]
    void Send(string data);
}

public interface IIpcServer : IDisposable
{
    void Start();
    void Stop();
 
    event EventHandler<DataReceivedEventArgs> Received;
}

[Serializable]
public sealed class DataReceivedEventArgs : EventArgs
{
    public DataReceivedEventArgs(string data)
    {
        this.Data = data;
    }

    public string Data { get; private set; }
}
```

Như bạn có thể thấy, đây là những giao tiếp rất đơn giản, chỉ một chiều từ máy khách đến máy chủ. Trong trường hợp bạn đang thắc mắc, các thuộc tính [ ServiceContract ] và [ OperationContract ] thực sự chỉ hữu ích cho việc triển khai WCF, nhưng tôi để chúng ở đây vì chúng thực sự sẽ không gây hại gì. Thêm về điều này trong một phút.

**IIpcClient** chỉ cho phép gửi tin nhắn văn bản.

**IIpcServer** phức tạp hơn một chút, vì người ta có thể khởi động và dừng máy chủ, cũng như nhận các sự kiện từ nó. Nó triển khai IDisposable vì một số triển khai có thể cần giải phóng các tài nguyên không được quản lý.


### WCF

![WCF Architecture](https://boxxv.github.io/img/2023/wcf-architecture.gif "Kiến trúc WCF")

Vì vậy, lần triển khai đầu tiên sử dụng WCF và ràng buộc `NetNamedPipeBinding` (vận chuyển). Những lý do tôi chọn ràng buộc binding  này là:
- Nó là nhị phân
- Nó nhanh
- Không cần mở TCP sockets
- Được tối ưu hóa cho cùng một máy (thực tế, việc triển khai WCF chỉ hoạt động theo cách này, mặc dù giao thức [named pipes protocol](https://learn.microsoft.com/en-us/windows/win32/ipc/named-pipes) có thể được sử dụng trên các máy).

{% highlight js %}
public class WcfClient : ClientBase<IIpcClient>, IIpcClient
{
    public WcfClient() : base(new NetNamedPipeBinding(), new EndpointAddress(string.Format("net.pipe://localhost/{0}", typeof(IIpcClient).Name)))
    {
    }
 
    public void Send(string data)
    {
        this.Channel.Send(data);
    }
}
{% endhighlight %}

Bởi vì phương thức **Gửi** trong hợp đồng của tôi được trang trí decorated  bằng [OperationContractAttribute](https://learn.microsoft.com/en-us/dotnet/api/system.servicemodel.operationcontractattribute) với thuộc tính [IsOneWay](https://learn.microsoft.com/en-us/dotnet/api/system.servicemodel.operationcontractattribute.isoneway) được đặt, nên tin nhắn được gửi mà không cần đợi tin nhắn phản hồi, làm cho nó nhanh hơn một chút.

{% highlight cpp %}
public sealed class WcfServer : IIpcServer
{
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]
    private class _Server : IIpcClient
    {
        private readonly WcfServer server;
 
        public _Server(WcfServer server)
        {
            this.server = server;
        }
 
        public void Send(string data)
        {
            this.server.OnReceived(new DataReceivedEventArgs(data));
        }
    }
 
    private readonly ServiceHost host;
 
    private void OnReceived(DataReceivedEventArgs e)
    {
        var handler = this.Received;
 
        if (handler != null)
        {
            handler(this, e);
        }
    }
 
    public WcfServer()
    {
        this.host = new ServiceHost(new _Server(this), new Uri(string.Format("net.pipe://localhost/{0}", typeof(IIpcClient).Name)));
    }
 
    public event EventHandler<DataReceivedEventArgs> Received;
 
    public void Start()
    {
        this.host.Open();
    }
 
    public void Stop()
    {
        this.host.Close();
    }
 
    void IDisposable.Dispose()
    {
        this.Stop();
 
        (this.host as IDisposable).Dispose();
    }
}
{% endhighlight %}

Một lần nữa, không có gì đặc biệt, chỉ đáng chú ý rằng, để đơn giản, tôi chỉ cho phép một phiên bản duy nhất của máy chủ ( InstanceContextMode.Single ).


### Sockets

Windows không hỗ trợ họ ổ cắm AF_UNIX, chỉ hỗ trợ TCP/IP, vì vậy, để minh họa giao tiếp mạng IP, tôi có thể chọn [TCP](https://learn.microsoft.com/en-us/dotnet/fundamentals/networking/sockets/tcp-classes) hoặc [UDP](https://learn.microsoft.com/en-us/dotnet/fundamentals/networking/sockets/tcp-classes) , nhưng tôi đã chọn UDP vì hiệu suất tốt hơn và vì tính đơn giản tương đối mà ví dụ này yêu cầu.


### .NET Remoting

![.NET Remoting](https://boxxv.github.io/img/2023/remoting.png "Remoting")

Ngày xưa, .NET Remoting là phản hồi của .NET đối với Java RMI và về cơ bản là một triển khai tham chiếu từ xa, tương tự như CORBA. Với Remote, người ta có thể gọi các phương thức trên một đối tượng nằm trong một máy khác. .NET Remoting từ lâu đã bị thay thế bởi WCF, nhưng nó vẫn là một giải pháp thay thế khả thi, đặc biệt vì WCF không cho phép tham chiếu từ xa.

Remoting là về các đối tượng phân tán, trong khi WCF là về các dịch vụ. Remoting có khả năng chuyển các phiên bản đối tượng giữa client và server, WCF thì không. Sự khác biệt này cơ bản hơn nhiều so với các vấn đề kỹ thuật như công nghệ nào hiệu quả hơn, chết nhiều hơn hay liệu nó có thể kết nối .NET với Java hay không, nhưng tôi chỉ mới nhận ra điều đó gần đây, khi tôi đang tranh luận về việc sử dụng công nghệ nào để giao tiếp giữa hai ứng dụng .NET cụ thể mà chúng tôi có.

WCF vs Remoting
WCF và .NET Remote thực sự có thể so sánh được về hiệu năng. Sự khác biệt rất nhỏ (đo độ trễ của máy khách) nên việc cái nào nhanh hơn một chút không quan trọng. WCF mặc dù có thông lượng máy chủ tốt hơn nhiều so với .NET Remoting. Nếu tôi bắt đầu dự án hoàn toàn mới, tôi sẽ chọn WCF. Dù sao thì WCF còn làm được nhiều điều hơn là Remoting và đối với tất cả những tính năng đó, tôi yêu thích nó.

Nếu đó là trên một máy duy nhất, Named Pipes mang lại cho bạn hiệu suất tốt hơn và có thể được triển khai với cơ sở hạ tầng từ xa cũng như WCF. Hoặc bạn chỉ có thể sử dụng trực tiếp System.IO.Pipes.

Nếu ý bạn là giao tiếp giữa các quá trình, thì tôi đã sử dụng .NET Remoting cho đến nay mà không gặp bất kỳ sự cố nào. Nếu hai quá trình trên cùng một máy, giao tiếp khá nhanh.

Các đường ống được đặt tên chắc chắn hiệu quả hơn, nhưng chúng yêu cầu thiết kế ít nhất một giao thức ứng dụng cơ bản, điều này có thể không khả thi. Remoting cho phép bạn gọi các phương thức từ xa một cách dễ dàng.

.NET Remoting dành riêng cho một **công nghệ cũ** được giữ lại để tương thích ngược với các ứng dụng hiện có và **không được khuyến nghị cho sự phát triển mới**. Các ứng dụng phân tán bây giờ sẽ được phát triển bằng cách sử dụng Windows Communication Foundation (WCF).


### Message Queues

Windows đã bao gồm việc triển khai hàng đợi tin nhắn trong một thời gian dài, điều mà các nhà phát triển thường bỏ quên. Nếu bạn chưa cài đặt nó – bạn có thể kiểm tra xem dịch vụ Message Queuing có tồn tại hay không – bạn có thể cài đặt nó thông qua **Programs and Features – Turn Windows features on and off** trên **Control Panel**.

![WCF Services](https://boxxv.github.io/img/2023/HTTP_activation.png "WCF Services")


### Named Pipes

Các Named Pipes trong Windows là một phương tiện gửi dữ liệu song công giữa các máy chủ Windows. Chúng tôi đã sử dụng nó trong triển khai WCF, được hiển thị trước đó, nhưng .NET có hỗ trợ tích hợp sẵn riêng cho giao tiếp Named Pipes.


### Memory-Mapped Files

Memory-mapped files trong Windows cho phép chúng tôi ánh xạ một “cửa sổ” của một tệp lớn trên hệ thống tệp hoặc để tạo một vùng bộ nhớ được đặt tên có thể được chia sẻ giữa các quy trình. Trong mẫu này, tôi sẽ tạo một khu vực được chia sẻ một cách nhanh chóng và sử dụng AutoResetEvents có tên để kiểm soát quyền truy cập vào khu vực đó.


### Event Tracing for Windows

Việc triển khai ETW yêu cầu bạn sử dụng .NET 4.6 hoặc bạn cài đặt Thư viện nguồn sự kiện của Microsoft từ NuGet. Điều này là do sự khác biệt về API trong EventSource và các lớp liên quan. Tất nhiên, ETW hữu ích hơn nhiều so với việc chỉ gửi tin nhắn văn bản giữa các điểm cuối, nhưng, này, nó cũng có thể làm điều đó, vì vậy đây là cách.


### Files

Tôi đã do dự trước khi đưa vào cái này, nhưng dù sao thì nó cũng đến đây. Về cơ bản, các lớp máy chủ và máy khách sẽ cố gắng giành được khóa độc quyền trên một tệp. Máy chủ sẽ kiểm tra trước nếu tệp không trống, nếu không, nó sẽ chỉ lặp lại. Thật không may, không có cách nào dễ dàng để xem liệu một tệp có bị khóa hay không, đây là một vấn đề phổ biến.


### COM Interop

COM đã được giới thiệu trong Windows từ nhiều thập kỷ trước và phần lớn phụ thuộc vào nó. Nó cũng là cơ sở cho tự động hóa và những thứ thú vị khác. Nó là một tiêu chuẩn cho khả năng tương tác dựa trên các định nghĩa giao diện không phụ thuộc vào ngôn ngữ. Việc triển khai COM có thể được viết bằng một số ngôn ngữ, từ Visual Basic đến C và C++, và tất nhiên là cả C# và .NET.

COM có khái niệm về một nhà máy lớp, được sử dụng để xây dựng các triển khai giao diện COM thực tế. Chúng ta có thể sử dụng cách triển khai của riêng mình để luôn trả về cùng một phiên bản – một singleton. Đối với ví dụ này, lần khởi tạo đầu tiên của thành phần COM sẽ tạo một phiên bản trong bộ nhớ và những phiên bản tiếp theo sẽ luôn truy cập vào phiên bản đó. Các cuộc gọi đến các phương thức của nó sẽ được tuần tự hóa và dữ liệu được truyền liền mạch giữa các quy trình. Bây giờ, COM Interop là một chủ đề phức tạp và tôi sẽ chỉ khám phá bề nổi của nó. Cái này cần nhiều công việc hơn những cái trước.


### WM_COPYDATA

WM_COPYDATA có thể không nói nhiều với các nhà phát triển .NET, nhưng đối với các nhà phát triển Win32 C/C++ kiểu cũ thì chắc chắn là có! Về cơ bản, đó là cách mà người ta có thể gửi dữ liệu tùy ý, bao gồm cả dữ liệu có cấu trúc, giữa các quy trình (thực ra, nói đúng ra là cửa sổ). Một người sẽ gửi một thông báo WM_COPYDATA tới một tay cầm cửa sổ, đang chạy trên bất kỳ quy trình nào và Windows sẽ đảm nhận việc sắp xếp lại dữ liệu để nó có sẵn bên ngoài không gian địa chỉ của quy trình gửi. Thậm chí có thể gửi nó tới tất cả các quy trình, sử dụng HWND_BROADCAST , nhưng điều đó có lẽ sẽ không khôn ngoan, bởi vì các ứng dụng khác nhau có thể có cách hiểu khác nhau về nó. Ngoài ra, nó cần được chuyển bằng SendMessage , PostMessage sẽ không hoạt động.

> [Inter-Process Communication with C#](https://www.codeproject.com/Articles/19570/Inter-Process-Communication-with-C)

## API Service

API Service là một bản hợp đồng giữa service và client. Bất kể là kiểu tương tác nào đi chăng nữa, thì việc xác định rõ IDL (Interface Definition Language) hay ngôn ngữ định nghĩa giao diên cũng là quan trọng nhất. Chỉ khi bạn định nghĩa được nó thì bạn mới có thể khai thác được dịch vụ của mình. Nó giúp tăng khẳ năng đáp ứng nhu cầu của client

Một dịch vụ sử dụng API luôn luôn phải thay đổi để phù hợp với yêu cầu. Điều đó là khá dễ dàng nếu như bạn viết nó trong mô hình Nguyên Khối. Nhưng trong mô hình Microservice thì điều đó quả là khó khăn, ngay cả khi tất cả các API đó cùng nằm trong một ứng dụng. Và tất nhiên bạn cũng không thể bắt client thay đổi theo từng bước phát triển API này được =)) nghe vô lý :v Và cũng có thể bạn sẽ phải làm cách nào đó cho cả API cũ và API mới đều hoạt động được =))


## Tổng kết:

![.NET Framework](https://boxxv.github.io/img/2023/Dot-Net.png ".NET Framework component stack")

- Named/Anonymous Pipes: Yêu cầu/phản hồi trực tiếp. Hoạt động, nhưng nó hơi rắc rối khi xử lý nhiều máy khách giao tiếp với một máy chủ.
- WCF: Yêu cầu/Phản hồi trực tiếp. Đẹp và dễ thực hiện, ngoại trừ người dùng cần lo lắng về việc định cấu hình một cổng hợp lệ để hệ thống chạy trên đó.
- Pipes quá tệ, level quá thấp, SignalR quá tệ, level quá cao.
- gRPC là câu trả lời hiện đại. WCF cách đây 10 năm, COM cách đây 15-20 năm.

Cả SignalR và gRPC đều là những cơ chế giao tiếp tuyệt vời mà mọi nhà phát triển phần mềm Microsoft-stack nên tìm hiểu. Và không phải là tốt hơn so với khác. Chỉ có những tình huống cụ thể có lợi cho việc sử dụng một tình huống cụ thể. Nếu bạn cần xây dựng thứ gì đó mà máy chủ thường xuyên giao tiếp với máy khách, thì SignalR sẽ tốt hơn. Mặt khác, nếu bạn đang xây dựng một ứng dụng phân tán lớn với nhiều bộ phận chuyển động, gRPC sẽ là một cơ chế tốt hơn để các bộ phận đó giao tiếp với nhau.

-----
Tham khảo:

- [Sự giao tiếp trong mô hình Microservice](https://viblo.asia/p/su-giao-tiep-trong-mo-hinh-microservice-bJzKmxqX59N)
- [Xây dựng Microservice bằng API Gateway](https://viblo.asia/p/xay-dung-microservice-bang-api-gateway-3P0lPnv4Kox)
- [Local Machine Interprocess Communication with .NET](https://weblogs.asp.net/ricardoperes/local-machine-interprocess-communication-with-net)
- [Best choice for .NET inter-process communication](https://stackoverflow.com/q/84855/20202692)
- [WCF vs .NET Remoting](https://ikriv.com/blog/?p=2551)
- [SIGNALR VS GRPC ON ASP.NET CORE – WHICH ONE TO CHOOSE](https://scientificprogrammer.net/2022/07/25/signalr-vs-grpc-on-asp-net-core-which-one-to-choose/)
- []()