---
layout: post
categories: ["C# & .NET"]
title: Thực hiện Kiểm tra tình trạng hệ thống trong .NET 8
subtitle: Implementing Health Checks in .NET 8
image: "img/techskills.jpg"
tags:
- Mạt Code
- lập trình
---

- [Tại sao cần kiểm tra tình trạng hệ thống trong các ứng dụng ASP.NET?](#tại-sao-cần-kiểm-tra-tình-trạng-hệ-thống-trong-các-ứng-dụng-aspnet)
  - [Hãy cùng tìm hiểu sâu hơn về ví dụ cơ sở dữ liệu để xem tại sao kiểm tra tình trạng ASP.NET lại quan trọng trên quy mô lớn hơn.](#hãy-cùng-tìm-hiểu-sâu-hơn-về-ví-dụ-cơ-sở-dữ-liệu-để-xem-tại-sao-kiểm-tra-tình-trạng-aspnet-lại-quan-trọng-trên-quy-mô-lớn-hơn)
- [Làm thế nào để triển khai kiểm tra tình trạng trong .Net 8?](#làm-thế-nào-để-triển-khai-kiểm-tra-tình-trạng-trong-net-8)
  - [Phần 1: Thiết lập kiểm tra sức khỏe cơ bản](#phần-1-thiết-lập-kiểm-tra-sức-khỏe-cơ-bản)
  - [Phần 2: Được triển khai với Kiểm tra sức khỏe](#phần-2-được-triển-khai-với-kiểm-tra-sức-khỏe)
    - [a. Kiểm tra tình trạng cơ sở dữ liệu](#a-kiểm-tra-tình-trạng-cơ-sở-dữ-liệu)
    - [b. Kiểm tra tình trạng điểm cuối từ xa](#b-kiểm-tra-tình-trạng-điểm-cuối-từ-xa)
    - [c. Kiểm tra sức khỏe trí nhớ](#c-kiểm-tra-sức-khỏe-trí-nhớ)
- [Phần kết luận](#phần-kết-luận)



![Health Checks](https://boxxv.github.io/img/2024/1_aQnoS8e5B5WGqTNS9rNfNw.webp "Health Checks")

Kiểm tra tình trạng rất quan trọng để theo dõi trạng thái của các ứng dụng và dịch vụ của bạn. Chúng cung cấp một cách nhanh chóng và tự động để xác minh rằng các thành phần và phụ thuộc của ứng dụng đang chạy trơn tru.

Bài viết này sẽ khám phá cách triển khai kiểm tra tình trạng trong ứng dụng web .NET 8.

# Tại sao cần kiểm tra tình trạng hệ thống trong các ứng dụng ASP.NET?

Kiểm tra tình trạng giúp bạn chủ động xác định các vấn đề trong ứng dụng của mình, cho phép bạn giải quyết chúng trước khi chúng ảnh hưởng đến người dùng. Việc thường xuyên kiểm tra tình trạng của các thành phần ứng dụng có thể đảm bảo hệ thống đáng tin cậy và phục hồi hơn.

Khi phát triển ứng dụng ASP.NET, ứng dụng thường dựa vào nhiều hệ thống con khác nhau, chẳng hạn như cơ sở dữ liệu, hệ thống tệp, API, v.v. Một trong những tình huống phổ biến nhất liên quan đến sự phụ thuộc vào cơ sở dữ liệu. Hầu như mọi ứng dụng đều yêu cầu tương tác liền mạch với cơ sở dữ liệu, khiến nó trở thành thành phần hệ thống quan trọng. Tuy nhiên, phát triển ứng dụng theo cách truyền thống thường bỏ qua khía cạnh này, dẫn đến khả năng hỏng hóc nếu mất kết nối với cơ sở dữ liệu vì bất kỳ lý do gì.

Hãy xem xét một kịch bản mà ứng dụng của bạn phụ thuộc vào cơ sở dữ liệu. Nếu vì nhiều lý do, kết nối đến cơ sở dữ liệu bị mất, ứng dụng có khả năng bị hỏng. Mặc dù tình huống này là một ví dụ cơ bản về lý do tại sao kiểm tra sức khỏe có lợi, nhưng nó không nắm bắt được toàn bộ phạm vi phát triển của chúng. Vì vậy,

## Hãy cùng tìm hiểu sâu hơn về ví dụ cơ sở dữ liệu để xem tại sao kiểm tra tình trạng ASP.NET lại quan trọng trên quy mô lớn hơn.

- Sẽ thế nào nếu bạn có thể kiểm tra xem cơ sở dữ liệu có khả dụng hay không trước khi thiết lập kết nối?  
— — Hãy tưởng tượng bạn có khả năng đánh giá tình trạng sức khỏe và tính khả dụng của các hệ thống con quan trọng của ứng dụng trước khi chủ động tương tác với chúng. Hãy tưởng tượng một tình huống mà thay vì gặp phải lỗi ứng dụng đột ngột do mất kết nối cơ sở dữ liệu, bạn có thể chủ động xác minh tính khả dụng của nó.

- Sẽ thế nào nếu ứng dụng của bạn có thể xử lý khéo léo tình huống không khả dụng của cơ sở dữ liệu?  
— — Hãy tưởng tượng bạn trao quyền cho ứng dụng của mình để hiển thị thông báo thân thiện với người dùng khi cơ sở dữ liệu không thể truy cập được. Thay vì thông báo lỗi khó hiểu gây nhầm lẫn cho người dùng, bạn có thể truyền đạt liền mạch tình trạng không khả dụng của một thành phần quan trọng, đảm bảo trải nghiệm người dùng tốt hơn.

- Sẽ thế nào nếu bạn có thể chuyển đổi liền mạch sang cơ sở dữ liệu dự phòng trong trường hợp không khả dụng?  
— — Hãy cân nhắc tính linh hoạt của việc hướng dẫn ứng dụng của bạn chuyển đổi liền mạch sang cơ sở dữ liệu thay thế khi cơ sở dữ liệu chính không khả dụng. Điều này không chỉ duy trì tính liên tục của ứng dụng mà còn đảm bảo rằng người dùng gặp phải sự gián đoạn tối thiểu.

- Sẽ thế nào nếu bạn có thể chỉ thị cho bộ cân bằng tải chuyển sang môi trường dự phòng dựa trên kiểm tra tình trạng?  
— — Hãy tưởng tượng bạn có khả năng truyền đạt tình trạng sức khỏe của ứng dụng của bạn đến bộ cân bằng tải. Nếu ứng dụng được coi là không khỏe do thiếu cơ sở dữ liệu hoặc bất kỳ vấn đề quan trọng nào khác, bộ cân bằng tải có thể chuyển hướng lưu lượng truy cập một cách thông minh đến môi trường dự phòng, đảm bảo tính khả dụng của dịch vụ liên tục.

**Với ASP.NET Health Checks, bạn có thể:**

- Đánh giá tình trạng sức khỏe và tính khả dụng của các hệ thống con của bạn.
- Tạo điểm cuối để thông báo cho các hệ thống khác về tình trạng ứng dụng của bạn.
- Sử dụng các điểm cuối kiểm tra tình trạng của các hệ thống khác.


# Làm thế nào để triển khai kiểm tra tình trạng trong .Net 8?

Tôi sẽ trình bày cấu hình kiểm tra sức khỏe theo hai cách trong .Net 8


## Phần 1: Thiết lập kiểm tra sức khỏe cơ bản

Mục đích của phần này là thiết lập nền tảng kiểm tra tình trạng hồ sơ của bạn.

**Các gói NuGet bắt buộc**

Đảm bảo bạn đã cài đặt gói NuGet sau:

1. [Microsoft.Extensions.Diagnostics.HealthChecks](https://www.nuget.org/packages/microsoft.extensions.diagnostics.healthchecks/)

**Thêm dịch vụ kiểm tra sức khỏe**

Trong `Program.cs`, hãy thêm các dịch vụ kiểm tra sức khỏe cần thiết vào vùng chứa Dependency Injection:

```csharp
builder.Services.AddHealthChecks(); 

//Ứng dụng trung gian
 HealthCheck.MapHealthChecks( "/api/health" );
```

Sau khi thêm những mục này vào API web .NET 8 của bạn, hãy chạy ứng dụng thành công. Điều hướng đến điểm cuối sau bằng trình duyệt, giả sử ứng dụng của bạn đang chạy tại: Để kiểm tra tình trạng API web của bạn, hãy truy cập:

[https://localhost:44333/swagger/feedbackservice/index.html](https://localhost:44333/swagger/feedbackservice/index.html)

[https://localhost:44333/api/health](https://localhost:44333/api/health)

Sau khi gọi điểm cuối, bạn sẽ thấy API web của mình “Hoạt động bình thường”.

![Health Checks](https://boxxv.github.io/img/2024/1_YHJOpkLWaJuCnjvw_IU0lw.webp "Health Checks")

Khi gọi điểm cuối này, bạn sẽ thấy API web của mình được đánh dấu là “Khỏe mạnh”. Điều quan trọng cần lưu ý là ở giai đoạn này, chúng tôi đã thiết lập các kiểm tra tình trạng cơ bản để đảm bảo tình trạng chung của ứng dụng, nhưng các kiểm tra tình trạng cụ thể cho các hệ thống con vẫn chưa được triển khai.

## Phần 2: Được triển khai với Kiểm tra sức khỏe

**Kiểm tra tình trạng tùy chỉnh để giám sát nâng cao**

Trong phần này, chúng ta sẽ đi sâu vào các ví dụ cụ thể về việc triển khai kiểm tra tình trạng tùy chỉnh để giám sát các thành phần quan trọng của API web .NET 8 của bạn. Các kiểm tra này vượt ra ngoài thiết lập cơ bản, cung cấp góc nhìn chi tiết và sâu sắc hơn về tình trạng của ứng dụng của bạn.

**Các gói NuGet bắt buộc**

Đảm bảo bạn đã cài đặt gói NuGet sau:

1. [Microsoft.Extensions.Diagnostics.HealthChecks](https://www.nuget.org/packages/microsoft.extensions.diagnostics.healthchecks/)
2. [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer)
3. [AspNetCore.HealthChecks.UI](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI)
4. [AspNetCore.HealthChecks.UI.Client](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI.Client)
5. [AspNetCore.HealthChecks.UI.InMemory.Storage](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI.InMemory.Storage)
6. [AspNetCore.HealthChecks.Uris](https://www.nuget.org/packages/AspNetCore.HealthChecks.Uris)

Lưu ý: Tôi đã tạo riêng một tệp có tên là HealthCheck.cs, và triển khai tất cả các cấu hình kiểm tra tình trạng.

### a. Kiểm tra tình trạng cơ sở dữ liệu

Kiểm tra tình trạng cơ sở dữ liệu là một khía cạnh quan trọng trong việc theo dõi tình trạng ứng dụng của bạn, đặc biệt là khi ứng dụng dựa vào cơ sở dữ liệu để lưu trữ và truy xuất dữ liệu. Kiểm tra tình trạng này đảm bảo rằng cơ sở dữ liệu không chỉ có thể truy cập được mà còn phản hồi các truy vấn.


HealthCheck.cs
```csharp
public static void ConfigureHealthChecks(this IServiceCollection services,IConfiguration configuration)
{
    services.AddHealthChecks()
        .AddSqlServer(configuration["ConnectionStrings:DefaultConnection"], healthQuery: "select 1", name: "SQL Server", failureStatus: HealthStatus.Unhealthy, tags: new[] { "Feedback", "Database" });

    //services.AddHealthChecksUI();
    services.AddHealthChecksUI(opt =>
    {
        opt.SetEvaluationTimeInSeconds(10); //time in seconds between check    
        opt.MaximumHistoryEntriesPerEndpoint(60); //maximum history of checks    
        opt.SetApiMaxActiveRequests(1); //api requests concurrency    
        opt.AddHealthCheckEndpoint("feedback api", "/api/health"); //map health check api    

    })
        .AddInMemoryStorage();
}
```

`configuration["ConnectionStrings:DefaultConnection"]` Thao tác này sẽ lấy chuỗi kết nối từ cấu hình của bạn, cho phép linh hoạt trong việc cấu hình kết nối cơ sở dữ liệu.

`failureStatus: HealthStatus.Unhealthy` Điều này cho biết nếu kiểm tra tình trạng không thành công, trạng thái tình trạng chung sẽ được đánh dấu là không lành mạnh.

Cấu hình `ConfigureHealthChecks()` bên trong `Program.cs`

```csharp
//Congiguring Health Ckeck
builder.Services.ConfigureHealthChecks(builder.Configuration);

//HealthCheck Middleware
app.MapHealthChecks("/api/health", new HealthCheckOptions()
{
    Predicate = _ => true,
    ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
});
app.UseHealthChecksUI(delegate (Options options) 
{
    options.UIPath = "/healthcheck-ui";
    options.AddCustomStylesheet("./HealthCheck/Custom.css");

});
```

Đầu ra:
Điểm cuối: `/api/health`

![Health Checks](https://boxxv.github.io/img/2024/1_OHP38NpLykmsXt37T_XYwA.webp "Health Checks")

Điểm cuối: /healthcheck-ui

![Health Checks](https://boxxv.github.io/img/2024/1_CgcgA2yhoo1Lc1E2Dyr4IQ.webp "Health Checks")


### b. Kiểm tra tình trạng điểm cuối từ xa

Tiếp theo, chúng ta sẽ triển khai kiểm tra tình trạng cho các điểm cuối từ xa và bộ nhớ.

RemoteHealthCheck.cs

```csharp
using Microsoft.Extensions.Diagnostics.HealthChecks;
using System;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;

namespace FeedbackService.Api
{
    public class RemoteHealthCheck : IHealthCheck
    {
        private readonly IHttpClientFactory _httpClientFactory;
        public RemoteHealthCheck(IHttpClientFactory httpClientFactory)
        {
            _httpClientFactory = httpClientFactory;
        }
        public async Task<HealthCheckResult> CheckHealthAsync(HealthCheckContext context, CancellationToken cancellationToken = new CancellationToken())
        {
            using (var httpClient = _httpClientFactory.CreateClient())
            {
                var response = await httpClient.GetAsync("https://api.ipify.org");
                if (response.IsSuccessStatusCode)
                {
                    return HealthCheckResult.Healthy($"Remote endpoints is healthy.");
                }

                return HealthCheckResult.Unhealthy("Remote endpoint is unhealthy");
            }
        }
    }
}
```

Kiểm tra tình trạng này theo dõi tình trạng của điểm cuối từ xa (ví dụ: API) bằng cách thực hiện yêu cầu HTTP.

### c. Kiểm tra sức khỏe trí nhớ

Cuối cùng, hãy triển khai kiểm tra tình trạng bộ nhớ để theo dõi trạng thái bộ nhớ của dịch vụ API.

MemoryHealthCheck.cs

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Extensions.Diagnostics.HealthChecks;
using Microsoft.Extensions.Options;

namespace FeedbackService.Api.HealthCheck
{
    public class MemoryHealthCheck : IHealthCheck
    {
        private readonly IOptionsMonitor<MemoryCheckOptions> _options;

        public MemoryHealthCheck(IOptionsMonitor<MemoryCheckOptions> options)
        {
            _options = options;
        }

        public string Name => "memory_check";

        public Task<HealthCheckResult> CheckHealthAsync(
            HealthCheckContext context,
            CancellationToken cancellationToken = default(CancellationToken))
        {
            var options = _options.Get(context.Registration.Name);

            // Include GC information in the reported diagnostics.
            var allocated = GC.GetTotalMemory(forceFullCollection: false);
            var data = new Dictionary<string, object>()
        {
            { "AllocatedBytes", allocated },
            { "Gen0Collections", GC.CollectionCount(0) },
            { "Gen1Collections", GC.CollectionCount(1) },
            { "Gen2Collections", GC.CollectionCount(2) },
        };
            var status = (allocated < options.Threshold) ? HealthStatus.Healthy : HealthStatus.Unhealthy;

            return Task.FromResult(new HealthCheckResult(
                status,
                description: "Reports degraded status if allocated bytes " +
                    $">= {options.Threshold} bytes.",
                exception: null,
                data: data));
        }
    }
    public class MemoryCheckOptions
    {
        public string Memorystatus { get; set; }
        //public int Threshold { get; set; }
        // Failure threshold (in bytes)
        public long Threshold { get; set; } = 1024L * 1024L * 1024L;
    }
}
```

Kiểm tra tình trạng này đánh giá trạng thái bộ nhớ của Dịch vụ phản hồi dựa trên số byte được phân bổ.

Bây giờ chúng ta hãy cấu hình `RemoteHealthCheck.cs` và `MemoryHealthCheck.cs` bên trong `HealthCheck.cs`

HealthCheck.cs

```csharp
public static void ConfigureHealthChecks(this IServiceCollection services,IConfiguration configuration)
{
    services.AddHealthChecks()
        .AddSqlServer(configuration["ConnectionStrings:Feedback"], healthQuery: "select 1", name: "SQL servere", failureStatus: HealthStatus.Unhealthy, tags: new[] { "Feedback", "Database" })
        .AddCheck<RemoteHealthCheck>("Remote endpoints Health Check", failureStatus: HealthStatus.Unhealthy)
        .AddCheck<MemoryHealthCheck>($"Feedback Service Memory Check", failureStatus: HealthStatus.Unhealthy, tags: new[] { "Feedback Service" })
        .AddUrlGroup(new Uri("https://localhost:44333/api/v1/heartbeats/ping"), name: "base URL", failureStatus: HealthStatus.Unhealthy);

    //services.AddHealthChecksUI();
    services.AddHealthChecksUI(opt =>
    {
        opt.SetEvaluationTimeInSeconds(10); //time in seconds between check    
        opt.MaximumHistoryEntriesPerEndpoint(60); //maximum history of checks    
        opt.SetApiMaxActiveRequests(1); //api requests concurrency    
        opt.AddHealthCheckEndpoint("feedback api", "/api/health"); //map health check api    

    })
        .AddInMemoryStorage();
}
```

Đầu ra:
Điểm cuối: /api/health

![Health Checks](https://boxxv.github.io/img/2024/1_SP0UQirxK3R4XjptIFyH0A.webp "Health Checks")


Điểm cuối: /healthcheck-ui

![Health Checks](https://boxxv.github.io/img/2024/1_4LleF_ymNb_rFq8ntlbEcQ.webp "Health Checks")

Vậy là bạn đã có nó! Chúng tôi đã triển khai thành công một số kiểm tra sức khỏe bên trong API web. Với các kiểm tra này, ứng dụng của bạn hiện đã được trang bị để giám sát và đảm bảo tình trạng tốt của nó. Tiếp tục xây dựng các ứng dụng mạnh mẽ và phục hồi với sức mạnh của các kiểm tra sức khỏe trong .NET 8!😍


# Phần kết luận

Việc triển khai kiểm tra sức khỏe trong ứng dụng .NET 8 của bạn là một bước quan trọng hướng tới việc xây dựng một hệ thống bền bỉ và đáng tin cậy. Với các kiểm tra sức khỏe tùy chỉnh và tích hợp, bạn có thể theo dõi trạng thái của ứng dụng và các phụ thuộc của ứng dụng, đảm bảo trải nghiệm người dùng mượt mà hơn.

Bài viết này đề cập đến những điều cơ bản về việc thêm kiểm tra sức khỏe vào ứng dụng của bạn và bạn có thể tùy chỉnh thêm dựa trên nhu cầu cụ thể của mình. Khi bạn tiếp tục phát triển ứng dụng, hãy cân nhắc thêm nhiều kiểm tra hơn để bao quát nhiều khía cạnh khác nhau về sức khỏe của hệ thống. Việc thường xuyên xem xét và cập nhật các kiểm tra sức khỏe sẽ giúp bạn duy trì một ứng dụng mạnh mẽ và phản hồi nhanh.

Để biết thông tin chi tiết hơn và cấu hình nâng cao, hãy tham khảo kho lưu trữ [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks).

Tác giả: [Jeslur Rahman](https://www.linkedin.com/in/jeslur-rahman-974a66216/) 😍

-----
- [Implementing Health Checks in .NET 8](https://medium.com/@jeslurrahman/implementing-health-checks-in-net-8-c3ba10af83c3)