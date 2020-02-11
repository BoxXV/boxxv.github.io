---
layout: post
title: Logging trong C#
subtitle: Thực tiễn hiện đại, Hướng dẫn đầy đủ
tags:
- Csharp
- Comment
- Commenting Convention
- Coding Conventions
modified: 2019-05-13
---

Ghi Log là một phần quan trọng của phát triển phần mềm trong nhiều năm nay. Người ta có thể lập luận rằng một cơ chế ghi Log là một phần bắt buộc phải có của bất kỳ ứng dụng hoặc thư viện nào.  

Ghi Log có một phần quan trọng để chạy trong kịch bản mà bạn có thể sử dụng gỡ lỗi tương tác (nghĩa là đính kèm trình gỡ lỗi như Visual Studio). Nó cho phép chúng tôi điều tra lỗi sau khi sự cố đã xảy ra. Trong một số trường hợp, như Gỡ lỗi sản phẩm, Log có thể là thông tin duy nhất bạn có.

Ngay cả khi bạn có thể gỡ lỗi quy trình của riêng mình, Log có thể cung cấp cho bạn thông tin vô giá về các thành phần khác như thư viện của bên thứ 3, có sẵn trong framework .NET và CLR.

Bên cạnh việc ghi Log, một thuật ngữ mới đang trở nên phổ biến: Giám sát. Giám sát có nghĩa là có một công cụ tự động báo cáo thông tin về ứng dụng của bạn. Thông tin đó thường là lỗi (Giám sát lỗi Error, Giám sát sự cố Crash), nhưng cũng là thông tin về các yêu cầu và về hiệu suất (Giám sát hiệu suất). Điều này rất khác với việc ghi Log nơi mã của bạn chủ động viết tin nhắn và ngoại lệ để ghi Log.

Ghi Log cũng có thể được sử dụng để thu thập dữ liệu và số liệu thống kê về người dùng của bạn. Dữ liệu này có thể được sử dụng để nghiên cứu mô hình sử dụng, nhân khẩu học và hành vi. Không cần phải nói, loại dữ liệu này là vô giá trong một số sản phẩm.


## Các nơi có thể ghi Log - Logging Target Types

Khi chúng tôi nói về ghi Log, theo truyền thống, chúng tôi có nghĩa là lưu tin nhắn vào một tệp. Đó thực sự là ghi Log, nhưng còn nhiều các loại ghi Log duy nhất này. Dưới đây là một số mục tiêu ghi Log phổ biến để xem xét:
- **Database**. Ghi Log vào cơ sở dữ liệu có nhiều lợi thế
  * Bạn có thể truy xuất Log từ bất cứ đâu mà không cần truy cập vào máy sản xuất.
  * Nó dễ dàng tổng hợp các bản ghi Log từ nhiều máy.
  * Không có trường hợp nào các bản ghi Log sẽ bị xóa khỏi một máy cục bộ.
  * Bạn có thể dễ dàng tìm kiếm và trích xuất số liệu thống kê từ Log. Điều này đặc biệt hữu ích nếu bạn sử dụng ghi Log có cấu trúc.
- Có rất nhiều lựa chọn cho cơ sở dữ liệu để lưu trữ Log của bạn. Chúng ta có thể phân loại chúng như sau:
  * Cơ sở dữ liệu **Relational** luôn là một lựa chọn. Họ dễ dàng thiết lập, có thể được truy vấn bằng SQL và hầu hết các kỹ sư đã quen thuộc với họ. Cơ sở dữ liệu quan hệ chứa các bảng và mỗi bảng có Primary Key riêng.
  * Cơ sở dữ liệu **NoSQL** như [CouchDB](https://couchdb.apache.org). Đây là hoàn hảo cho các bản ghi có cấu trúc được lưu trữ ở định dạng JSON.
  * Cơ sở dữ liệu **Time-series** như [InfluxDB](https://www.influxdata.com) được tối ưu hóa để lưu trữ các sự kiện dựa trên thời gian. Điều này có nghĩa là hiệu suất ghi Log của bạn sẽ tốt hơn và Log của bạn sẽ chiếm ít dung lượng lưu trữ hơn. Đây là một lựa chọn tốt cho ghi Log tải cao cường độ cao.
- **Searchable Solutions** như [Logstash](https://www.elastic.co/logstash) + [Elastic Search](https://www.elastic.co/elasticsearch) + [Kibana](https://www.elastic.co/kibana) (`Elastic Stack`) cung cấp dịch vụ đầy đủ cho Log của bạn. Họ sẽ lưu trữ, lập chỉ mục, thêm khả năng tìm kiếm và thậm chí trực quan hóa dữ liệu Log của bạn. Họ làm việc tốt nhất với ghi Log có cấu trúc.
- **Error Monitoring** Các công cụ giám sát lỗi cũng có thể hoạt động như các mục tiêu ghi Log. Điều này rất có lợi vì chúng có thể hiển thị lỗi cùng với các thông điệp tường trình trong cùng một bối cảnh. Ví dụ, bối cảnh có thể là cùng một yêu cầu http. Một vài lựa chọn là [Elmah](https://elmah.io) và [Azure Application Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview).
- **Logging to File** Ghi Log vào tập tin vẫn là một mục tiêu ghi Log tốt. Nó không phải là độc quyền, bạn có thể ghi Log cả vào tệp và cơ sở dữ liệu chẳng hạn. Đối với các ứng dụng máy tính để bàn, ghi Log vào tập tin là rất hiệu quả. Khi một vấn đề đã xảy ra, khách hàng có thể dễ dàng tìm và gửi các tệp Log của họ để điều tra.
- **Logging to Standard Output (Console) and Debug Output (Trace)** Ghi Log vào Đầu ra tiêu chuẩn (Bảng điều khiển) và Đầu ra gỡ lỗi (Dấu vết) - Ghi Log vào Bảng điều khiển, còn được gọi là Đầu ra tiêu chuẩn, rất thuận tiện, đặc biệt là trong quá trình phát triển. Windows cũng hỗ trợ một mục tiêu ghi Log tương tự có tên là **Debug Output**, bạn có thể ghi Log bằng `System.Diagnostics.Trace ("My message")`. Điều tuyệt vời của cả hai về ghi Log Console và Trace là bạn cũng có thể ghi Log tin nhắn từ mã gốc, dễ dàng đạt được một hệ thống ghi Log dùng chung. Bạn có thể xem Đầu ra gỡ lỗi trực tiếp với một chương trình như [DebugView](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview). Bạn cũng có thể sử dụng lớp [ConsoleTraceListener](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.consoletracelistener?view=netframework-4.8) để hướng thông tin này đến mọi nơi, như đến cơ sở dữ liệu.
- **Logging to Event Viewer** Ghi Log vào Trình xem sự kiện - Nếu ứng dụng của bạn có trên Windows, bạn có thể sử dụng [Windows Event Log](https://searchwindowsserver.techtarget.com/definition/Windows-event-log) để ghi Log tin nhắn. Nó rất dễ làm và bạn có thể [xem tin nhắn](https://www.loggly.com/ultimate-guide/net-logging-basics/) bằng chương trình [Event Viewer](https://www.howtogeek.com/123646/htg-explains-what-the-windows-event-viewer-is-and-how-you-can-use-it/). Như một phần thưởng, tất cả các sự cố được tự động thêm vào như Log sự kiện. Vì vậy, sau bất kỳ sự cố quy trình .NET nào, bạn có thể vào Trình xem sự kiện và xem Ngoại lệ và ngăn xếp cuộc gọi của nó. Điều này khá tốn kém về mặt hiệu suất, do đó, tốt nhất là chỉ sử dụng cho các thông báo quan trọng, như lỗi nghiêm trọng.
- **Log to ETW** Ghi Log vào ETW - Windows có một hệ thống ghi Log tích hợp cực kỳ nhanh có tên là **Event Tracing for Windows (ETW)**. Bạn có thể sử dụng nó để xem các bản ghi từ .NET framework, hệ điều hành và thậm chí cả kernel. Nhưng bạn cũng có thể sử dụng ETW để ghi Log chính mình với `System.Diagnostics.Tracing.EventSource`. Đây là tùy chọn ghi Log nhanh nhất có sẵn trong .NET. Nếu bạn có một con đường hấp dẫn mà thực hiện 100.000 lần một giây, thì ETW có thể dành cho bạn. .NET Core 3.0 Preview 5+ hiện có một thay thế ETW được gọi là [dotnet-track](https://github.com/dotnet/diagnostics/blob/master/documentation/dotnet-trace-instructions.md) là đa nền tảng.


## Structured Logging Revolution

Trong ghi Log truyền thống, chúng ta ghi Log một thông điệp chuỗi đơn giản. Đối với thông báo đó, chúng ta thường thêm Dấu thời gian, cấp độ Log và có thể là bối cảnh bổ sung như Exception.
{% highlight js %}
try
{
	_log.Debug("About to do something");
	// ...
}
catch (Exception ex)
{
	_log.Error("Doing something failed with", ex);
}
{% endhighlight %}

Trong Ghi Log có cấu trúc, chúng ta cũng thêm các trường có cấu trúc vào thông báo. Đó là, chúng ta đã đánh dấu một số dữ liệu dưới dạng các trường và đặt tên cho nó. Sau đó, chúng ta sẽ có thể tìm kiếm trong các trường đó, lọc theo chúng và thu thập dữ liệu. Theo thư viện ghi Log của bạn, một thông điệp tường trình có cấu trúc có thể trông giống như thế này:
{% highlight js %}
var requestInfo = new { Url = "https://myurl.com/data", Payload = 12 };
_log.Information("Request info is {@RequestInfo}", requestInfo);
{% endhighlight %}

Khi được gửi đến máy chủ, điều này được lưu dưới dạng JSON chứ không phải là một chuỗi thông thường. Ý nghĩa rất lớn. Bây giờ, chúng ta có thể tìm thấy tất cả các thông điệp tường trình với một giá trị `Payload` nhất định. Hoặc lọc thông điệp tường trình theo URL yêu cầu. Chúng tôi có thể lưu dữ liệu của người tiêu dùng và thử và tìm mối tương quan với việc sử dụng chúng. Có lẽ chúng tôi sẽ thấy rằng phụ nữ trong độ tuổi từ 30 đến 35 có nhiều khả năng mua giày trong mùa hè. Điều này có nghĩa là chúng tôi có thể đề xuất nhiều giày hơn, nhận được nhiều doanh số hơn và có tiền thưởng Giáng sinh lớn. Tất cả với sức mạnh của ghi Log có cấu trúc.

Tất cả các frameworks ghi Log phổ biến đều hỗ trợ ghi Log tùy chỉnh, mặc dù tôi tin rằng [Serilog](https://serilog.net) là người đầu tiên thực hiện ghi Log có cấu trúc như một công dân hạng nhất.


## Logging Frameworks

Có 4 framework ghi Log thống trị chính trong .NET. Đó là [log4net](https://logging.apache.org/log4net), [NLog](https://nlog-project.org), [Serilog](https://serilog.net) và [Microsoft.Extensions.Logging](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-3.1) (chỉ dành cho .NET Core và ASP.NET Core). Tất cả chúng đều tuyệt vời, miễn phí và cung cấp chức năng tương tự.

Hãy nói chuyện trước với 3 framework ghi Log của cộng đồng: log4net, NLog và Serilog.

### [log4net](https://logging.apache.org/log4net)
[Apache log4net](https://logging.apache.org/log4net/release/features.html) là framework cũ nhất trong ba framework. Nó ban đầu được chuyển từ dự án **log4j** Java Java. Bạn sẽ tìm thấy nó trong hầu hết các dự án .NET cũ.

Để thiết lập, bạn sẽ cần xây dựng tệp cấu hình XML (log4net.config) trông giống như thế này:
```xml
<log4net>
  <appender name="RollingFile" type="log4net.Appender.RollingFileAppender">
    <file value="my_log.log" />
    <appendToFile value="true" />
    <maximumFileSize value="50KB" />
    <maxSizeRollBackups value="2" />
 
    <layout type="log4net.Layout.PatternLayout">
      <conversionPattern value="%date %level %message%newline" />
    </layout>
  </appender>
 
  <root>
    <level value="ALL" />
    <appender-ref ref="RollingFile" />
  </root>
</log4net>
```

Sau đó, thêm các mục sau vào `AssociationInfo.cs`:
{% highlight js %}
[assembly: log4net.Config.XmlConfigurator(ConfigFile = "log4net.config")]
{% endhighlight %}

Sau đó, chúng ta có thể bắt đầu ghi Log:
{% highlight js %}
class MyClass
{
	private static readonly log4net.ILog _log = log4net.LogManager.GetLogger(System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

	public void Foo()
	{
		_log.Debug("Foo started");
	}
}
{% endhighlight %}

**log4net** hỗ trợ [ghi Log có cấu trúc](https://stackify.com/log4net-guide-dotnet-logging/), nhưng không hoàn toàn như những người khác. Nó hỗ trợ một loạt các mục tiêu ghi Log được gọi là [appender](https://logging.apache.org/log4net/release/config-examples.html). Mặc dù nó hỗ trợ ít mục tiêu hơn các mục tiêu khác, log4net rất lớn đến nỗi bất cứ thứ gì được hỗ trợ, bạn đều có thể tìm thấy một triển khai tùy chỉnh trên internet, như ứng dụng tìm kiếm [log4net-to-ElasticSearch](https://www.nuget.org/packages/log4net.ElasticSearch/) này.

Vấn đề lớn nhất của log4net có lẽ là cấu hình khá khó khăn. Hãy cùng xem các đối thủ của mình xử lý việc này như thế nào.

### [NLog](https://nlog-project.org)

NLog xuất hiện thứ hai sau log4net và được rất nhiều người biết đến.

Giống như các thư viện khác, NLog bắt đầu với [NuGet package](https://www.nuget.org/packages/NLog/). Sau đó, bạn có thể định cấu hình bằng XML như log4net hoặc bằng code. Tôi sẽ chỉ cho bạn cách làm điều đó trong code (từ [tài liệu](https://github.com/NLog/NLog/wiki/Tutorial#configure-nlog-targets-for-output):

{% highlight csharp %}
var config = new NLog.Config.LoggingConfiguration();

// Targets where to log to: File and Console
var logfile = new NLog.Targets.FileTarget("logfile") { FileName = "file.txt" };
var logconsole = new NLog.Targets.ConsoleTarget("logconsole");

// Rules for mapping loggers to targets            
config.AddRule(LogLevel.Info, LogLevel.Fatal, logconsole);
config.AddRule(LogLevel.Debug, LogLevel.Fatal, logfile);

// Apply config           
NLog.LogManager.Configuration = config;
{% endhighlight %}

Bây giờ, bắt đầu ghi Log:

{% highlight js %}
class MyClass
{
	private static readonly NLog.Logger _log_ = NLog.LogManager.GetCurrentClassLogger();

	public void Foo()
	{
		_log.Debug("Foo started");
		// structured logging:
		_log.Info("Hello {Name}", "Michael");
	}
}
{% endhighlight %}

NLog có một thiết lập và API dễ dàng. Theo một số tài khoản, nó cũng nhanh hơn log4net. Nó hỗ trợ ghi Log có cấu trúc và 84 mục tiêu ngoài hộp bao gồm tất cả các cơ sở dữ liệu phổ biến. Giống như với bất kỳ thư viện nào, bạn có thể mở rộng NLog để viết Log bất cứ nơi nào bạn muốn.

### [Serilog](https://serilog.net)
Serilog cuối cùng đã tham gia bữa tiệc nhưng đã thêm một tính năng rất cần thiết: Ghi Log cấu trúc như một công dân hạng nhất. Chúng ta sẽ trở lại với điều đó.

Để sử dụng Serilog, trước tiên hãy cài đặt [NuGet](https://www.nuget.org/packages/serilog) của họ. Sau đó, thêm thiết lập trong mã (xem [tài liệu chính thức](https://github.com/serilog/serilog/wiki/Getting-Started)):

{% highlight js %}
class Program
{
	static void Main()
	{
		Log.Logger = new LoggerConfiguration()
			.MinimumLevel.Debug()
			.WriteTo.Console()
			.WriteTo.File("logs\\my_log.log", rollingInterval: RollingInterval.Day)
			.CreateLogger();
{% endhighlight %}

Và sử dụng:

{% highlight js %}
class MyClass
{

	public void Foo()
	{
		Log.Debug("Foo started");
		// structured logging:
		Log.Debug("Requesting from URL {A} with {B}", myUrl, myPayload);
	}
}
{% endhighlight %}

Vì vậy, nếu bạn nghĩ rằng NLog đơn giản như vậy, Serilog có thể giúp việc thiết lập trở nên dễ dàng hơn. Serilog cũng hỗ trợ một nhóm lớn các [targets (Sinks)](https://github.com/serilog/serilog/wiki/Provided-Sinks) ra khỏi hộp.

<del>Về mặt hiệu suất, Serilog dường như nhanh hơn khoảng hai lần so với NLog theo [Benchmark](https://www.darylcumbo.net/serilog-vs-nlog-benchmarks/) này.</del>  
Về mặt hiệu suất, NLog dường như nhanh hơn Serilog theo các [Benchmark](https://github.com/panchengtao/LoggingPerformance/issues/1) này.


## Which to choose?
Trước hết, cả 3 framework đều tốt và cung cấp một giá trị khá giống nhau. Trước khi trả lời câu hỏi này, hãy để một số nghiên cứu phổ biến. Nhìn vào thống kê gói NuGet trong [6 tuần qua](https://www.nuget.org/stats/packages) (đến ngày 11 tháng 8 năm 2019), chúng ta có thể thấy như sau:

![Looking at NuGet package statistics](http://boxxv.com/img/posts/logs-in-nuget.png "Looking at NuGet package statistics")

Serilog đứng đầu ở vị trí thứ 3, NLog đứng thứ hai ở vị trí thứ 20 và log4net đứng ở vị trí thứ 28. Một tỷ lệ khá đáng kể ủng hộ Serilog.
Đến ngày 10 tháng 02 năm 2020, Serilog đứng đầu ở vị trí thứ 1, NLog đứng thứ hai ở vị trí thứ 24 và log4net đứng ở vị trí thứ 33.

Google Trends vẽ một bức tranh rất khác:

![Google Trends](http://boxxv.com/img/posts/logs-google-trends.png "Google Trends")

Theo đó, NLog và log4net đang cạnh tranh vị trí đầu tiên, và Serilog đứng thứ 3 với tỷ lệ khá thấp.

Một thống kê thú vị khác là số lượng câu hỏi trong StackOverflow. Theo các [tags](https://stackoverflow.com/tags), log4net có khoảng 3794 câu hỏi, NLog có khoảng 2065 câu hỏi và Serilog với 977.

Hỗ trợ cũng là một cân nhắc lớn. Nhìn vào các gói NuGet, chúng ta có thể thấy rằng các gói [NLog](https://www.nuget.org/packages/nlog/) và [Serilog](https://www.nuget.org/packages/serilog/) được phát hành một vài lần một tháng. Trong khi đó [log4net](https://www.nuget.org/packages/log4net/) được phát hành một hoặc hai lần một năm.

**Phán quyết**: Do thiết lập khó khăn hơn, hỗ trợ ghi Log có cấu trúc kém hơn, bảo trì ít hơn và hiệu suất kém hơn, tôi không khuyến nghị sử dụng `log4net` cho các dự án mới. Có những ngoại lệ cho quy tắc này. Ví dụ: bạn có thể có một ứng dụng tùy chỉnh được thực hiện mà bạn không muốn viết lại cho một framework khác.

Đối với việc chọn `Serilog` hoặc `NLog`, tôi nghĩ cả hai lựa chọn đều tốt. Serilog dường như có sự hỗ trợ tốt hơn cho việc ghi Log có cấu trúc, trong khi NLog dường như có hiệu suất tốt hơn. Cả hai đều phổ biến và duy trì tốt. Vì vậy, tôi có thể chọn một người chiến thắng rõ ràng.

## Microsoft.Extensions.Logging (aka ASP.NET Core Logging)

.NET Core và ASP.NET Core đi kèm với framework ghi Log tích hợp sẵn. Khi bạn tạo một dự án ASP.NET Core mới từ mẫu mặc định, [Microsoft.Extensions.Logging](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-3.1) sẽ được đưa vào dự án. Đây là một phần lý do tại sao framework này phổ biến hơn nhiều so với các framework khác như đã thấy trong [NuGet Trends](https://nugettrends.com/packages?months=24&ids=Serilog&ids=NLog&ids=Microsoft.Extensions.Logging&ids=System.Diagnostics&ids=log4net).

ASP.NET Core Logging framework là cả một abstraction và implementation. Nó chủ yếu đảm bảo rằng bạn có thể có giao diện `ILogger<T>` trong hệ thống tiêm phụ thuộc ASP.NET Core của bạn. Bạn có thể thực hiện các thao tác sau trong bộ điều khiển của mình:

{% highlight js %}
public class MyController : Controller
{
	private readonly ILogger _logger;

	public MyController(ILogger<MyController> logger){
		logger.LogInformation("Hello world");
		_logger = logger;
	}
}
{% endhighlight %}

Log ghi vào đâu? Điều này phụ thuộc vào các **providers** của nó, mà bạn có thể chỉ định khi khởi tạo trong `Program.cs`. Providers chỉ là một tên khác cho Logging Targets. Giống như Sinks trong Serilog và Appender trong log4net.

{% highlight js %}
public static IHostBuilder CreateHostBuilder(string[] args) =>
	Host.CreateDefaultBuilder(args)
		.ConfigureLogging(logging =>
		{
			logging.ClearProviders();
			logging.AddConsole();//Adding Console provider
		})
		.ConfigureWebHostDefaults(webBuilder =>
		{
			webBuilder.UseStartup<Startup>();
		});

{% endhighlight %}

Trong trường hợp này, chúng tôi đã thêm Console provider, vì vậy tất cả các log messages sẽ ghi vào Console. Một số logging providers khác của Microsoft là: File, Debug, EventSource, TraceSource và ApplicationInsights. Nhưng bạn có thể tự thêm bất kỳ nhà cung cấp nào.


Có các logging providers cho tất cả các frameworks ghi Log cộng đồng lớn. Vì vậy, bạn có thể sử dụng **Microsoft.Extensions.Logging** để ghi Log tin nhắn với Serilog, NLog hoặc log4net. Ví dụ, đối với Serilog, nó đơn giản như việc thêm [Serilog.AspNetCore nuget package](https://www.nuget.org/packages/Serilog.AspNetCore) và thêm mã sau đây. Đầu tiên, hãy xác định Serilog’s logger trong `Program.cs`:

{% highlight js %}
public static void Main(string[] args)
{
	Log.Logger = new LoggerConfiguration()
		.Enrich.FromLogContext()
		.WriteTo.Console()
		.CreateLogger();
{% endhighlight %}

Bây giờ, thêm nó vào Host Builder:

{% highlight js %}
public static IHostBuilder CreateHostBuilder(string[] args) =>
	Host.CreateDefaultBuilder(args)
	.UseSerilog();
	.ConfigureWebHostDefaults(webBuilder =>
		{
				webBuilder.UseStartup<Startup>();
		})
{% endhighlight %}


## Có nên sử dụng Microsoft.Extensions.Logging trong tất cả các ứng dụng ASP.NET Core không?

Tôi thấy rằng các framework mới hơn, Serilog và NLog, tốt hơn so với ghi Log ASP.NET Core logging framework. Họ có nhiều tính năng hơn và khả năng sử dụng tốt hơn. Điều này bao gồm hỗ trợ ghi Log có cấu trúc tốt hơn và hỗ trợ dữ liệu theo ngữ cảnh tốt hơn. Khi bạn tích hợp Serilog hoặc NLog làm provider trong `Microsoft.Extensions.Logging`, bạn sẽ mất một số khả năng đó nếu làm việc với `ILogger` interface (mặc dù bạn có thể làm việc trực tiếp với trình ghi Log của bên thứ 3).

Phải nói rằng, tôi là một người tin tưởng lớn vào việc làm những gì phổ biến. Các nhà phát triển sẽ quen thuộc hơn với các công nghệ phổ biến, bạn sẽ có nhiều tài liệu hơn, cộng đồng lớn hơn và nhiều câu hỏi hơn về StackOverflow. Vì vậy, tôi vẫn sẽ chọn đi cùng `Microsoft.Extensions.Logging` cho các dự án mới. Nó cung cấp hầu hết các chức năng mà bạn sẽ cần và abstraction cho phép dễ dàng thay đổi nó sang một framework khác sau này.


## Logging Best Practices

Bất kể framework và logging targets bạn chọn, có một số thực tiễn tốt nhất phổ biến để làm theo.

### 1. Sử dụng Log Levels một cách thích hợp

Mỗi frameworks ghi Log liên kết theo mặc định một mức ghi Log cho mỗi thông báo. Các levels thường là **Debug**, **Info**, **Warn**, **Error**, **Fatal** hoặc tương tự. Đó là những điều quan trọng để truyền đạt các loại thông tin ghi Log. **Debug** và **Info** hiển thị thông tin gỡ lỗi và thông tin theo ngữ cảnh hữu ích để hiểu luồng hiện tại. **Warn** cho thấy một cái gì đó có lẽ là sai. **Error** cho thấy một lỗi đã xảy ra. Thông thường, chúng tôi sẽ muốn ghi thông báo lỗi khi chúng tôi bắt exceptions. **Fatal** thường có nghĩa là một lỗi lớn đã xảy ra đòi hỏi phải chấm dứt ứng dụng.


### 2. Chỉ kích hoạt các Log mức độ nghiêm trọng cao trong Production

Theo nguyên tắc thông thường, chúng tôi không muốn kích hoạt mức độ Debug và Info trong sản phẩm. Chúng tôi muốn ghi Log chỉ các thông báo Warn trở lên hoặc chỉ Error và cao hơn. Lý do là hiệu suất tốt hơn, tránh sử dụng nhiều bộ nhớ hơn và có thể tránh gửi thông tin nhạy cảm.

Đó là lý do tại sao bạn nên đảm bảo thay đổi cấu hình ghi Log của mình khi triển khai vào sản phẩm. Nó có thể dễ dàng như mệnh đề `#IF DEBUG` trong code hoặc một bước đặc biệt để thay đổi tệp cấu hình trong đường ống CI/CD của bạn.


### 3. Log Exceptions

Đối với gỡ lỗi sản phẩm, ghi Log Exceptions là rất quan trọng. Nó thường là phần thông tin quan trọng nhất mà chúng ta cần để giải quyết lỗi. Điều đó có nghĩa là cả hai trường hợp ngoại lệ được xử lý và ngoại lệ chưa được xử lý. Đối với các trường hợp ngoại lệ được xử lý, hãy đảm bảo `log.Error()` trong mệnh đề `catch`. Đối với các trường hợp ngoại lệ chưa được xử lý, bạn có thể đăng ký vào một sự kiện đặc biệt phát sinh khi ném ngoại lệ. Hoặc một phần mềm trung gian trong ASP.NET Core, như [ở đây](https://code-maze.com/global-error-handling-aspnetcore/).


### 4. Log Context

Để hiểu vấn đề sản phẩm, chúng ta cần bối cảnh. Trong khi Ngoại lệ là điều quan trọng nhất, thì Bối cảnh là thứ quan trọng thứ 2. Chúng ta cần biết Http Request, luồng hiện tại, machine hiện tại, trạng thái, thông tin người dùng, v.v.

Bạn có thể ghi Log ngữ cảnh với mọi thông báo, khi chuyển tiếp hoặc chỉ ngoại lệ. Tất cả các thư viện ghi Log hỗ trợ báo cáo về bối cảnh. Nó tốt nhất để sử dụng ghi Log có cấu trúc cho bối cảnh, vì vậy bạn sẽ có thể tìm kiếm và lọc theo nó sau này.


### 5. Use Structured Logging








Tham khảo:
- [Logging in C# .NET Modern-day Practices: The Complete Guide](https://michaelscodingspot.com/logging-in-dotnet/)
