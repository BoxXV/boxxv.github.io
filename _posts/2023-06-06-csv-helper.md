---
layout: post
title: Ghi vào tệp CSV bằng C# với CsvHelper
subtitle: Handling CSV Files in ASP.NET Core Web APIs
image: "img/technology.png"
tags:
- CSV
- CsvHelper
- multi-thread
- .NET
- C#
---

![CsvHelper](https://boxxv.github.io/img/2023/csv-helper.png "CsvHelper")

Thoạt nghe qua thì việc đọc file CSV không có vẻ gì là khó khăn, nhưng thực tế thì mọi thứ không đơn giản như vậy. Đúng là code để đọc dữ liệu từ file CSV không quá phức tạp. Nhưng việc đảm bảo rằng đoạn code đó type-safe, nhanh, và dễ tùy biến thì lại không hề dễ dàng. Đó là lý do vì sao ta nên sử dụng những thư viện có sẵn như [CsvHelper](https://github.com/JoshClose/CsvHelper).

Các bạn có thể tải code ví dụ trong bài này từ link dưới đây. [https://github.com/duongntbk/CsvHelperDemo](https://github.com/duongntbk/CsvHelperDemo)


### Cài đặt CsvHelper

Chạy lệnh dưới đây để cài CsvHelper.

```bat
dotnet add package CsvHelper --version 30.0.1
```


### Đọc file CSV bằng CsvHelper

Ta sẽ dùng file CSV dưới đây làm ví dụ. File này có 3 cột với dạng chữ và 1 cột với dạng số.

```
FirstName,LastName,Age,IsActive
John,Doe,30,Yes
Jane,Doe,31,No
Duong,Nguyen,31,Yes
```

Ta sẽ map từng dòng trong file đó với object thuộc lớp `Person`.

{% highlight js %}
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int? Age { get; set; }
    public string IsActive { get; set; }
}
{% endhighlight %}

Dưới đây là code đọc file CSV sử dụng CsvHelper.

{% highlight js %}
var fileName = @"<đường dẫn tới file CSV>";
var configuration = new CsvConfiguration(CultureInfo.InvariantCulture)
{
    Encoding = Encoding.UTF8, // File của ta dùng encoding UTF-8.
    Delimiter = "," // Ký tự phân cách giữa các trường là dấu phẩy.
};

using (var fs = File.Open(fileName, FileMode.Open, FileAccess.Read, FileShare.Read))
{
    using (var textReader = new StreamReader(fs, Encoding.UTF8))
    using (var csv = new CsvReader(textReader, configuration))
    {
        var data = csv.GetRecords<Person>();
        
        foreach (var person in data)
        {
            // Xử lý dữ liệu trong từng dòng
        }
    }
}
{% endhighlight %}

Biến data sẽ có kiểu là `IEnumerable<Person>`. CsvHelper sẽ tự động map từng cột trong file CSV với property cùng tên trong lớp `Person`. Ví dụ: giá trị trong cột FirstName sẽ được map với `Person.FirstName`. Ta có thể duyệt qua các phần tử trong data để đọc dữ liệu của từng dòng trong file CSV.


### Các tùy biến khi đọc file

Lớp CsvConfiguration có chứa nhiều tùy biến cho việc đọc file CSV. Dưới đây là một số tùy biến quan trọng.

- HasHeaderRecord: nếu giá trị này là true thì dòng đầu tiên sẽ được coi là dòng tên cột. Giá trị mặc định của tùy biến này là true. Có thể các bạn sẽ nghĩ tất nhiên phải có dòng tên cột, nếu không thì làm sao CsvHelper map được cột với property? Câu trả lời sẽ có ở phần sau.
- Quote: ký tự quote trong file CSV file. Giá trị mặc định là ".
- IgnoreBlankLines: nếu giá trị này là true thì các dòng trống sẽ bị bỏ qua. Giá trị mặc định là true.
- Delimiter: ký tự phân cách giữa các trường. Giá trị mặc định là , (vì CSV là viết tắt của COMMA-separated values).
- DetectDelimiter: nếu giá trị này là true thì CsvHelper sẽ tự động phát hiện ký tự phân tách mà không dùng giá trị của Delimiter. Giá trị mặc định là false.
- Encoding: kiểu encoding mà file CSV sử dụng.


### Map cột trong file CSV với property trong lớp Person một cách thủ công

#### Map cột bằng tên

Trong quá trình làm việc ở Nhật, tôi thường xuyên phải xử lý file CSV với tên cột bằng Tiếng Nhật, ví dụ như file dưới đây.

```
姓,名,年齢,アクティブ
Doe,John,30,Yes
Doe,Jane,31,No
Nguyen,Duong,31,Yes
```

Như đã nói trong phần trước, trong trường hợp đơn giản nhất thì CsvHelper sẽ tự động map cột trong file CSV với property cùng tên. Nhưng ta không nên dùng Tiếng Nhật để đặt tên cho property trong lớp Person. Vậy ta phải làm thế nào? Lớp ClassMap sẽ giúp ta giải quyết vấn đề này. Ta cần tạo một lớp mới kế thừa từ ClassMap và dùng nó để bảo CsvHelper map cột nào với property nào.

{% highlight js %}
public class PersonMapByName : ClassMap<Person>
{
    public PersonMapByName()
    {
        Map(p => p.FirstName).Name("名");
        Map(p => p.LastName).Name("姓");
        Map(p => p.Age).Name("年齢");
        Map(p => p.IsActive).Name("アクティブ");
    }
}
{% endhighlight %}

Sau đó ta chỉ cần đăng ký PersonMapByName với CsvHelper trước khi gọi hàm csv.GetRecords.

{% highlight js %}
csv.Context.RegisterClassMap<PersonMapByName>();
var data = csv.GetRecords<Person>();
{% endhighlight %}

Ta cũng có thể bỏ qua không map một hay nhiều cột của file CSV. Ví dụ: lớp dưới đây chỉ map cột 姓 và 名 mà không map cột 年齢 và アクティブ.

{% highlight js %}
public class PersonMapByName : ClassMap<Person>
{
    public PersonMapByName()
    {
        Map(p => p.FirstName).Name("名");
        Map(p => p.LastName).Name("姓");
    }
}
{% endhighlight %}


#### Map cột bằng số thứ tự

Để dùng được cách ở trên, tên của các cột trong file CSV phải không trùng nhau. Nếu có 2 hay nhiều cột trùng tên thì giá trị của cột đầu tiên sẽ được map với property. Ví dụ: file dưới đây có 2 cột cùng tên là IsActive, lúc này giá trị Yes/No sẽ được dùng thay vì True/False.

```
FirstName,LastName,Age,IsActive,IsActive
John,Doe,30,Yes,True
Jane,Doe,31,No,False
Duong,Nguyen,31,Yes,True
```

Nếu muốn dùng giá trị True/False thì ta cần map cột bằng số thứ tự. Cách map cột bằng số thứ tự rất giống cách map cột bằng tên, điểm khác biệt duy nhất là ta gọi hàm nào sau hàm Map. Hãy xem đoạn code dưới đây.

{% highlight js %}
public class PersonMapByIndex : ClassMap<Person>
{
    public PersonMapByName()
    {
        Map(p => p.FirstName).Index(0); // Số thứ tự các cột bắt đầu từ 0
        Map(p => p.LastName).Index(1);
        Map(p => p.Age).Index(2);
        Map(p => p.IsActive).Index(4); // Số thứ tự của cột IsActive với giá trị True/False là 4
    }
}
{% endhighlight %}


Hơn nữa, ta có thể dùng lẫn cách map cột bằng thứ tự và bằng tên. Nhưng nhớ là nếu đã map thủ công thì ta phải map tất cả các cột, nếu cột nào ta không map thì CsvHelper sẽ bỏ qua cột đó.

{% highlight js %}
public class PersonMapByIndex : ClassMap<Person>
{
    public PersonMapByName()
    {
        Map(p => p.FirstName).Name("FirstName"); // Map bằng tên
        Map(p => p.LastName); // Map tự động với property cùng tên
        Map(p => p.Age).Index(2); // Map bằng số thứ tự
        Map(p => p.IsActive).Index(4); // Map bằng số thứ tự
    }
}
{% endhighlight %}

<ins>Chú ý</ins>: nếu file CSV của ta không có dòng tên cột thì bắt buộc ta phải dùng cách map cột bằng số thứ tự. Lúc này, ta cần phải đặt giá trị HasHeaderRecord là false.


### Chuyển giá trị trong file CSV từ kiểu này sang kiểu khác

Có lẽ các bạn cũng để ý là propery Age trong lớp Person có kiểu là Integer, nhưng file CSV lại chỉ có thể chứa dữ liệu dạng chữ. CsvHelper có thể chuyển dữ liệu từ kiểu string sang các kiểu cơ bản trong .NET (Boolean, Int32, Int64, Enum,…). Các bạn có thể xem danh sách các converter được CsvHelper hỗ trợ tại link này.

Nếu như kiểu ta muốn chuyển đổi không phải là kiểu cơ bản thì sao? Hoặc giả sử nó là kiểu cơ bản, nhưng giá trị trong file CSV lại không đúng theo chuẩn thì sao? Lúc này, ta cần tự mình viết lớp converter. Ta sẽ dùng lại file CSV ví dụ của phần trước.

```
FirstName,LastName,Age,IsActive
John,Doe,30,Yes
Jane,Doe,31,No
Duong,Nguyen,31,Yes
```

Lần này ta sẽ map nó với lớp dưới đây, để ý là IsActive bây giờ có kiểu là bool.

{% highlight js %}
public class PersonV2
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int? Age { get; set; }
    public bool IsActive { get; set; }
}
{% endhighlight %}

#### A custom type converter

Tuy bool là kiểu cơ bản trong .NET nhưng converter mặc định của CsvHelper chỉ xử lý được giá trị True/False. Trong khi đó file CSV của ta lại chứa Yes/No. Vì thế ta phải kế thừa lớp DefaultTypeConverter và định nghĩa lại hàm ConvertFromString.

{% highlight js %}
public class CustomBooleanConverter : DefaultTypeConverter
{
    public override object ConvertFromString(string text, IReaderRow row, MemberMapData memberMapData)
    {
        return text.Equals("Yes", StringComparison.OrdinalIgnoreCase);
    }
}
{% endhighlight %}

Nếu như ta muốn ghi dữ liệu vào file CSV thì ta còn phải định nghĩa lại cả hàm ConvertToString. Dưới đây là cách để chuyển giá trị từ kiểu boolean về lại thành Yes/No (giá trị không phải là boolean sẽ gây là lỗi).

{% highlight js %}
public override string ConvertToString(object value, IWriterRow row, MemberMapData memberMapData)
{
    if (value is bool boolVal)
    {
        return boolVal ? "Yes" : "No";
    }

    throw new ArgumentException("Giá trị phải có kiểu là boolean");
}
{% endhighlight %}

#### Đăng ký converter của ta với CsvHelper

Như đã thấy, converter của ta sẽ chuyển giá trị Yes (không phân biệt chữ hoa chữ thường) thành true; còn tất cả các giá trị khác sẽ được chuyển thành false. Bước tiếp theo là sử dụng converter này bằng cách gọi hàm TypeConverter.

{% highlight js %}
public class PersonMapWithConverter : ClassMap<PersonV2>
{
    public PersonMapWithConverter()
    {
        Map(p => p.FirstName);
        Map(p => p.LastName);
        Map(p => p.Age);
        Map(p => p.IsActive).TypeConverter<CustomBooleanConverter>();
    }
}
{% endhighlight %}

Lưu ý là ta cũng có thể gọi hàm TypeConverter sau khi map cột bằng tên hoặc số thứ tự.

{% highlight js %}
Map(p => p.IsActive).Name("IsActive").TypeConverter<CustomBooleanConverter>();
{% endhighlight %}

Hoặc

{% highlight js %}
Map(p => p.IsActive).Index(3).TypeConverter<CustomBooleanConverter>();
{% endhighlight %}

Sau đó ta có thể đăng ký PersonMapWithConverter với CsvHelper một cách bình thường.

{% highlight js %}
csv.Context.RegisterClassMap<PersonMapWithConverter>();
var data = csv.GetRecords<PersonV2>();
{% endhighlight %}


### Đọc file CSV một cách không đồng bộ

CsvHelper cũng cho phép ta đọc file CSV một cách không đồng bộ. Thay vì dùng hàm GetRecords, ta có thể dùng hàm GetRecordsAsync. Giá trị trả về sẽ có kiểu là IAsyncEnumerable<T>.

{% highlight js %}
var fileName = @"<đường dẫn tới file CSV>";
var configuration = new CsvConfiguration(CultureInfo.InvariantCulture)
{
    Encoding = Encoding.UTF8, // File của ta dùng encoding UTF-8.
    Delimiter = "," // Ký tự phân cách giữa các trường là dấu phẩy.
};

using (var fs = File.Open(fileName, FileMode.Open, FileAccess.Read, FileShare.Read))
{
    using (var textReader = new StreamReader(fs, Encoding.UTF8))
    using (var csv = new CsvReader(textReader, configuration))
    {
        var data = csv.GetRecordsAsync<Person>();
        
        await foreach (var person in data) // Duyệt phần tử của data một cách không đồng bộ
        {
            // Xử lý dữ liệu trong từng dòng
        }
    }
}
{% endhighlight %}

Khi dùng IAsyncEnumerable và await foreach, vòng lặp của ta sẽ không block trong khi đợi đọc phần tử tiếp theo từ data.

### Kết thúc

Tôi đã dùng `CsvHelper` trong nhiều dự án thực tế, và thư viện này có thể xử lý nhưng file CSV với hàng chục ngàn dòng một cách dễ dàng. Nếu file của bạn có tới vài triệu dòng thì có thể bạn sẽ gặp vấn đề về bộ nhớ. Nhưng trước lúc đó thì `CsvHelper` với sự đơn giản của nó vẫn là một lựa chọn khả thi.


-----
Tham khảo:
- [Writing to CSV-file from multiple threads](https://gunnarpeipman.com/write-csv-from-multiple-threads/)