---
layout: post
title: "Điều khiển PLC bằng C#: Các phương thức TCP/IP và OPC UA"
subtitle: "Controlling PLC with C#: TCP/IP and OPC UA Methods"
date: 2026-09-29 10:11:12
tags:
- PLC
- OPC UA
- TCP
- Csharp
---

- [Tổng quan](#tổng-quan)
- [Phương pháp 1: TCP/IP Socket Communication](#phương-pháp-1-tcpip-socket-communication)
  - [Triển khai TCP Client bằng C#](#triển-khai-tcp-client-bằng-c)
  - [Siemens S7 ISO-on-TCP Message Structure](#siemens-s7-iso-on-tcp-message-structure)
- [Phương pháp 2: OPC UA Communication](#phương-pháp-2-opc-ua-communication)
  - [Ví dụ về Đọc/Ghi OPC UA](#ví-dụ-về-đọcghi-opc-ua)
- [Các tham số kết nối dành riêng cho PLC](#các-tham-số-kết-nối-dành-riêng-cho-plc)
- [Các thư viện được khuyến nghị theo thương hiệu PLC](#các-thư-viện-được-khuyến-nghị-theo-thương-hiệu-plc)
  - [Allen-Bradley (EtherNet/IP)](#allen-bradley-ethernetip)
  - [Siemens S7](#siemens-s7)
- [Các vấn đề thường gặp và giải pháp](#các-vấn-đề-thường-gặp-và-giải-pháp)
- [Các bước xác minh](#các-bước-xác-minh)
- [FAQ](#faq)
- [Kết luận](#kết-luận)


## Tổng quan

Việc điều khiển PLC từ C# đòi hỏi phải thiết lập giao tiếp công nghiệp, sử dụng phương thức truyền tin trực tiếp qua socket `TCP/IP` hoặc giao thức `OPC UA` (Open Platform Communications Unified Architecture). Bài hướng dẫn này trình bày cả hai phương pháp kèm theo các ví dụ mã nguồn thực tế.

> Yêu cầu tiên quyết: Đảm bảo PLC của bạn có cổng kết nối Ethernet (ví dụ: Allen-Bradley 1756-EN2T, Siemens CP 343-1) và nằm cùng mạng với máy tính dùng để phát triển phần mềm.

## Phương pháp 1: TCP/IP Socket Communication

Giao tiếp TCP/IP trực tiếp hoạt động hiệu quả với các PLC Siemens S7 khi sử dụng các giao thức như `ISO-on-TCP` (RFC1006). Phương pháp này đòi hỏi người thực hiện phải tự định dạng khung tin nhắn và có kiến ​​thức về giao thức.

### Triển khai TCP Client bằng C#

```csharp
using System;
using System.Net.Sockets;
using System.Text;

public class PLC_TCP_Client
{
    private TcpClient _client;
    private NetworkStream _stream;
    
    public bool Connect(string ipAddress, int port)
    {
        try
        {
            _client = new TcpClient(ipAddress, port);
            _stream = _client.GetStream();
            return true;
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Connection failed: {ex.Message}");
            return false;
        }
    }
    
    public byte[] SendReceive(byte[] data)
    {
        if (_stream == null) return null;
        
        _stream.Write(data, 0, data.Length);
        byte[] buffer = new byte[1024];
        int bytesRead = _stream.Read(buffer, 0, buffer.Length);
        
        if (bytesRead > 0)
        {
            byte[] response = new byte[bytesRead];
            Array.Copy(buffer, response, bytesRead);
            return response;
        }
        return null;
    }
    
    public void Disconnect()
    {
        _stream?.Close();
        _client?.Close();
    }
}
```

### Siemens S7 ISO-on-TCP Message Structure

Giao tiếp Siemens S7 yêu cầu cấu trúc phần đầu (header) cụ thể (theo chuẩn RFC1006):

```csharp
// ISO-on-TCP Header (7 bytes) + S7 Protocol
byte[] s7Request = new byte[] 
{
    0x03, 0x00, 0x00, 0x1F, 0x02, 0xF0, 0x80,   // RFC1006 Header
    0x32, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00,   // S7 Header
    0x0E, 0x00, 0x00, 0x04, 0x01, 0x12, 0x04,   // Job PDU
    0x10, 0x00,                                 // DB Read
    0x00, 0x01, 0x00, 0x00,                     // DB Number, Start
    0x00, 0x01                                  // Length (1 word)
};
```


## Phương pháp 2: OPC UA Communication

OPC UA cung cấp khả năng giao tiếp PLC được chuẩn hóa và không phụ thuộc vào nhà cung cấp. Các thư viện được khuyến nghị:

- **.NET OPC Foundation SDK** (UA-.NETStandardLibrary) - Chính thức, hỗ trợ đầy đủ các tính năng của OPC UA
- **QuickOPC** (OpcLabs) - Thương mại, API dễ sử dụng hơn
- **OPC_NET_API** (GitHub) - Giải pháp thay thế mã nguồn mở

### Ví dụ về Đọc/Ghi OPC UA

```csharp
using Opc.Ua;
using Opc.Ua.Client;
using Opc.Ua.Configuration;

public class OPC_UA_Client
{
    private Session _session;
    
    public async Task Connect(string endpointUrl)
    {
        var config = new ApplicationConfiguration
        {
            ApplicationName = "C# PLC Client",
            ApplicationUri = "urn:CSharpPLCClient",
            SecurityConfiguration = new SecurityConfiguration(),
            TransportConfiguration = new TransportConfiguration()
        };
        
        var selectedEndpoint = CoreClientUtils.SelectEndpoint(endpointUrl, false);
        _session = await Session.Create(
            config, 
            new EndpointDescription(selectedEndpoint), 
            false, 
            "PLC Session", 
            60000, 
            new UserIdentity(new AnonymousIdentityToken()),
            null
        );
    }
    
    public DataValue ReadTag(string nodeId)
    {
        var nodesToRead = new ReadValueIdCollection
        {
            new ReadValueId { NodeId = nodeId, AttributeId = Attributes.Value }
        };
        
        _session.Read(null, 0, TimestampsToReturn.Both, nodesToRead, out var results, out _);
        return results[0];
    }
    
    public void WriteTag(string nodeId, object value)
    {
        var nodesToWrite = new WriteValueCollection
        {
            new WriteValue
            {
                NodeId = nodeId,
                AttributeId = Attributes.Value,
                Value = new DataValue(new Variant(value))
            }
        };
        
        _session.Write(null, nodesToWrite, out var results, out _);
    }
}
```


## Các tham số kết nối dành riêng cho PLC

| PLC Family                    | Protocol    | Default Port | Library/Method         |
| ----------------------------- | ----------- | ------------ | ---------------------- |
| Allen-Bradley Logix (CIP)     | EtherNet/IP | 44818        | LibPlcTag, AdvancedHMI |
| Siemens S7-300/400/1200/1500  | ISO-on-TCP  | 102          | S7.Net, Sharp7         |
| Schneider Modicon             | Modbus TCP  | 502          | NModbus4, EasyModbus   |
| Omron NJ/NX                   | EtherNet/IP | 44818        | OmronFins              |
| Mitsubishi iQ-F/iQ-R          | MC Protocol | 5001/5002    | MelsecMcNet            |

| Hãng PLC                     | Giao thức phổ biến              | Địa chỉ/biến số                | Ghi chú                                  |
| ---------------------------- | ------------------------------- | ------------------------------ | ---------------------------------------- |
| Allen-Bradley (Rockwell)     | EtherNet/IP (CIP)               | Tag-based (Motor_Speed, Valve1)| Dùng tag theo tên, không theo vùng nhớ   |
| Siemens (S7-1200, 1500, 300) | S7 Protocol, OPC UA             | DB1.DBW0, DB1.DBD4…            | Có thư viện Snap7, S7.Net                |
| Schneider                    | Modbus, OPC UA                  | %MW100, %M10…                  | Chuẩn Modbus                             |
| Omron (CJ, CS, NX, NJ, CP1)  | FINS, CIP (EtherNet/IP), Modbus | DM100, CIO10, W0…              | FINS (UDP/TCP), mới thì EtherNet/IP (CIP)|
| Mitsubishi (FX, Q, iQ-R, …)  | MC Protocol, Modbus             | D100, M10, X0…                 | Có driver MC Protocol                    |
| Inovance (H3U, H5U, …)       | Modbus RTU/TCP, OPC             | D100, M10, C100…               | Chủ yếu dùng Modbus, giống Mitsubishi    |
| Delta                        | Modbus, DVP Protocol            | D100, M10, C0…                 | Phổ biến, rẻ                             |
| Keyence                      | KV Protocol, EtherNet/IP        | DM, MR…                        | Có phần mềm riêng                        |


## Các thư viện được khuyến nghị theo thương hiệu PLC

### Allen-Bradley (EtherNet/IP)

**LibPlcTag.NET** (free, open-source):

```csharp
using PlcTag;

var tag = new Tag("MyTagName", 1, 1, "192.168.1.10", 1); // Campbell, DB, IP, Size
tag.Read();
var value = tag.Value;
tag.Write(value);
```

**AdvancedHMI** (miễn phí, Windows Forms): Hỗ trợ giao tiếp trực tiếp qua driver với các dòng Allen-Bradley SLC, MicroLogix, CompactLogix và ControlLogix.

### Siemens S7

**S7.Net** (open-source):

```csharp
using S7.Net;

var plc = new Plc(CpuType.S71200, "192.168.1.10", 0, 1);
plc.Open();

// Read DB1.DBW0 (INT)
var intValue = plc.Read("DB1.DBW0");

// Write DB1.DBW2 (INT)
plc.Write("DB1.DBW2", (short)42);

plc.Close();
```

**Sharp7** (mã nguồn mở): Dành cho `S7-1200/1500` với hiệu suất được tối ưu hóa.


## Các vấn đề thường gặp và giải pháp

| Issue                       | Cause      | Solution     |
| --------------------------- | --------------- | ---------- |
| Connection timeout          | Tường lửa chặn cổng kết nối, hoặc sai địa chỉ IP | Mở các cổng `102/502/44818` trong Windows Firewall; kiểm tra kết nối IP tới PLC. |
| Permission denied (Siemens) | Thiếu quyền PG/PC interface | Thiết lập "Access Path" thành `TCP/IP Native` trong TIA Portal → Options → Set PG/PC Interface. |
| Invalid node ID (OPC)       | Định danh OPC UA node không hợp lệ | Trước tiên, hãy sử dụng OPC UA Client (UAExpert) để duyệt và xác minh cấu trúc node. |
| PLC not responding          | Địa chỉ IP được cấp phát qua DHCP đã thay đổi | Gán địa chỉ IP tĩnh cho cổng Ethernet của PLC. |


## Các bước xác minh

1. Ping địa chỉ IP của PLC để xác nhận kết nối mạng
2. Sử dụng Wireshark hoặc TCPView để kiểm tra các gói tin bắt tay TCP
3. Kiểm thử bằng các công cụ của nhà sản xuất (RSLinx cho AB, TIA Portal cho Siemens) để xác nhận PLC chấp nhận kết nối từ bên ngoài
4. Triển khai cơ chế thử lại (retry logic) bằng C# để đảm bảo hoạt động ổn định


## FAQ

> Thư viện nào tốt nhất để giao tiếp giữa PLC Allen-Bradley và C#?

LibPlcTag (miễn phí, mã nguồn mở) hỗ trợ tất cả các dòng Logix thông qua giao thức EtherNet/IP trên cổng 44818. AdvancedHMI cung cấp các điều khiển Windows Forms giúp phát triển HMI nhanh chóng.

> Tôi có thể điều khiển trực tiếp PLC Siemens S7-1200 bằng C# không?

Có. Hãy sử dụng thư viện Sharp7 (cho dòng S7-1200/1500) hoặc S7.Net với cổng TCP 102. Đảm bảo rằng tính năng giao tiếp PUT/GET đã được kích hoạt trong TIA Portal tại mục CPU Properties → Protection → Connection Mechanisms.

> Cổng mặc định cho giao tiếp Modbus TCP là gì?

Cổng 502. Hãy sử dụng các thư viện như NModbus4 hoặc EasyModbus để đọc/ghi các thanh ghi giữ liệu (holding registers) (sử dụng mã hàm 0x03, 0x06, 0x10).

> Tôi có cần dùng OPC UA để giao tiếp với PLC không?

Không. OPC UA thường được khuyến nghị cho việc tích hợp cấp doanh nghiệp và giao tiếp đa nhà cung cấp (không phụ thuộc vào hãng cụ thể). Để điều khiển trực tiếp bằng C#, hãy sử dụng các thư viện dành riêng cho từng hãng (như LibPlcTag, S7.Net) vì chúng cung cấp API đơn giản hơn và hiệu suất tốt hơn.

> Làm thế nào để đọc các tag từ PLC ControlLogix 1756-L73?

Sử dụng LibPlcTag với định dạng đường dẫn tag: 1,192.168.1.10/MyTagName (trong đó 1 là Campbell, tiếp theo là địa chỉ IP và tên tag). Đảm bảo rằng kết nối CIP đã được kích hoạt trên mô-đun EN2T.


## Kết luận

Là C# developer, bạn không cần quan tâm đến logic bên trong PLC (kỹ sư tự động hóa lo phần đó).

Việc chính của bạn:
- Hiểu PLC giao tiếp bằng giao thức gì.
- Biết dữ liệu nằm ở đâu (địa chỉ/Tag/DB).
- Viết app để đọc/ghi – hiển thị – xử lý – lưu trữ – tích hợp dữ liệu. # Workflow: PLC ↔ C# App ↔ Database/Cloud


-----
Tham khảo:
- [Controlling PLC with C#: TCP/IP and OPC UA Methods](https://industrialmonitordirect.com/blogs/knowledgebase/controlling-plc-with-c-tcpip-and-opc-ua-methods#section-2)
- [C# Developer làm gì khi làm việc với PLC đã lập trình sẵn?](https://dev.to/kimhieuwork/c-developer-lam-gi-khi-lam-viec-voi-plc-da-lap-trinh-san-42m8)
- [Scada C# với Tất cả PLC](https://tuhocplc.com/course/scada-c-voi-tat-ca-plc/)
- []()