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

![IPC](https://boxxv.github.io/img/2023/Interprocess.png "IPC")

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

** Contracts **

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

Bởi vì phương thức **Gửi** trong hợp đồng của tôi được trang trí decorated  bằng OperationContractAttribute với thuộc tính IsOneWay được đặt, nên tin nhắn được gửi mà không cần đợi tin nhắn phản hồi, làm cho nó nhanh hơn một chút.

{% highlight %}
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



### Sockets



## API Service

API Service là một bản hợp đồng giữa service và client. Bất kể là kiểu tương tác nào đi chăng nữa, thì việc xác định rõ IDL (Interface Definition Language) hay ngôn ngữ định nghĩa giao diên cũng là quan trọng nhất. Chỉ khi bạn định nghĩa được nó thì bạn mới có thể khai thác được dịch vụ của mình. Nó giúp tăng khẳ năng đáp ứng nhu cầu của client

Một dịch vụ sử dụng API luôn luôn phải thay đổi để phù hợp với yêu cầu. Điều đó là khá dễ dàng nếu như bạn viết nó trong mô hình Nguyên Khối. Nhưng trong mô hình Microservice thì điều đó quả là khó khăn, ngay cả khi tất cả các API đó cùng nằm trong một ứng dụng. Và tất nhiên bạn cũng không thể bắt client thay đổi theo từng bước phát triển API này được =)) nghe vô lý :v Và cũng có thể bạn sẽ phải làm cách nào đó cho cả API cũ và API mới đều hoạt động được =))




-----
Tham khảo:

- [Sự giao tiếp trong mô hình Microservice](https://viblo.asia/p/su-giao-tiep-trong-mo-hinh-microservice-bJzKmxqX59N)
- [Xây dựng Microservice bằng API Gateway](https://viblo.asia/p/xay-dung-microservice-bang-api-gateway-3P0lPnv4Kox)
- []()