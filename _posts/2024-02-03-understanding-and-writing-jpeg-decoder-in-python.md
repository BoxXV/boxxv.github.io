---
layout: post
title: Hiểu và giải mã hình ảnh JPEG bằng Python
subtitle: Understanding and Decoding a JPEG Image using Python
image: "img/2024/reverse_engineering_intro_featured.jpg"
tags:
- Reverse Engineering
- JPEG
- Python
---
# Mục lục

- [Mục lục](#mục-lục)
- [Giới thiệu](#giới-thiệu)
- [Different parts of a JPEG](#different-parts-of-a-jpeg)
- [Bắt đầu tập tin và kết thúc tập tin](#bắt-đầu-tập-tin-và-kết-thúc-tập-tin)
- [Tổng kết](#tổng-kết)

Chào mọi người! 👋 Hôm nay chúng ta sẽ tìm hiểu thuật toán nén JPEG. Một điều mà nhiều người không biết là JPEG không phải là một định dạng mà là một thuật toán. Hình ảnh JPEG bạn nhìn thấy hầu hết ở định dạng JFIF (Định dạng trao đổi tệp JPEG) sử dụng nội bộ thuật toán nén JPEG. Đến cuối bài viết này, bạn sẽ hiểu rõ hơn nhiều về cách thuật toán JPEG nén dữ liệu và cách bạn có thể viết một số mã Python tùy chỉnh để giải nén nó. Chúng tôi sẽ không đề cập đến tất cả các sắc thái của định dạng JPEG (như quét lũy tiến) mà chỉ đề cập đến định dạng đường cơ sở cơ bản khi viết bộ giải mã của chúng tôi.

# Giới thiệu

Tại sao phải viết một bài khác trên JPEG khi đã có hàng trăm bài viết trên internet? Chà, thông thường khi bạn đọc các bài viết về JPEG, tác giả chỉ cung cấp cho bạn thông tin chi tiết về định dạng trông như thế nào. Bạn không triển khai bất kỳ mã nào để thực hiện việc giải nén và giải mã thực tế. Ngay cả khi bạn viết mã, nó vẫn ở dạng C/C++ và không thể truy cập được đối với nhiều người. Tôi dự định thay đổi điều đó bằng cách chỉ cho bạn cách bộ giải mã JPEG cơ bản hoạt động bằng Python 3. Tôi sẽ dựa trên mã được cấp phép MIT này nhưng sẽ sửa đổi nhiều để tăng khả năng đọc và dễ hiểu. Bạn có thể tìm thấy mã đã sửa đổi cho bài viết này trên repo GitHub của tôi.

# Different parts of a JPEG

Hãy bắt đầu với bức ảnh đẹp này của Ange Albertini. Nó liệt kê tất cả các phần khác nhau của một tệp JPEG đơn giản. Hãy nhìn vào nó. Chúng ta sẽ khám phá từng phân khúc. Bạn có thể phải tham khảo hình ảnh này khá nhiều lần khi đọc hướng dẫn này.

![Reverse Engineering](https://boxxv.github.io/img/2024/JPEGRGB_dissected.png "Reverse Engineering")

Ở mức rất cơ bản, hầu hết mọi tệp nhị phân đều chứa một vài điểm đánh dấu (hoặc tiêu đề). Bạn có thể coi những điểm đánh dấu này giống như dấu trang. Chúng rất quan trọng trong việc hiểu tệp và được các chương trình như tệp (trên Mac/Linux) sử dụng để cho chúng tôi biết chi tiết về tệp. Các điểm đánh dấu này xác định nơi lưu trữ một số thông tin cụ thể trong một tệp. Hầu hết các điểm đánh dấu được theo sau bởi thông tin độ dài cho đoạn đánh dấu cụ thể. Điều này cho chúng ta biết đoạn cụ thể đó dài bao nhiêu.

# Bắt đầu tập tin và kết thúc tập tin

Điểm đánh dấu đầu tiên chúng tôi quan tâm là `FF D8`. Nó cho chúng ta biết đây là điểm bắt đầu của hình ảnh. Nếu không thấy nó, chúng ta có thể cho rằng đây là một tập tin khác. Một điểm đánh dấu quan trọng không kém khác là `FF D9`. Nó cho chúng ta biết rằng chúng ta đã đến cuối tệp hình ảnh. Mỗi điểm đánh dấu, ngoại trừ `FFD0` đến `FFD9` và `FF01`, ngay sau đó là bộ xác định độ dài sẽ cung cấp cho bạn độ dài của đoạn đánh dấu đó. Đối với các điểm đánh dấu bắt đầu và kết thúc tệp hình ảnh, mỗi điểm sẽ luôn dài hai byte.

Trong suốt hướng dẫn này, chúng ta sẽ làm việc với hình ảnh này:

![Reverse Engineering](https://boxxv.github.io/img/2024/profile.jpg "Reverse Engineering")

Hãy viết một số mã để xác định các điểm đánh dấu này.

```python
from struct import unpack

marker_mapping = {
    0xffd8: "Start of Image",
    0xffe0: "Application Default Header",
    0xffdb: "Quantization Table",
    0xffc0: "Start of Frame",
    0xffc4: "Define Huffman Table",
    0xffda: "Start of Scan",
    0xffd9: "End of Image"
}

class JPEG:
    def __init__(self, image_file):
        with open(image_file, 'rb') as f:
            self.img_data = f.read()
    
    def decode(self):
        data = self.img_data
        while(True):
            marker, = unpack(">H", data[0:2])
            print(marker_mapping.get(marker))
            if marker == 0xffd8:
                data = data[2:]
            elif marker == 0xffd9:
                return
            elif marker == 0xffda:
                data = data[-2:]
            else:
                lenchunk, = unpack(">H", data[2:4])
                data = data[2+lenchunk:]            
            if len(data)==0:
                break        

if __name__ == "__main__":
    img = JPEG('profile.jpg')
    img.decode()    

# OUTPUT:
# Start of Image
# Application Default Header
# Quantization Table
# Quantization Table
# Start of Frame
# Huffman Table
# Huffman Table
# Huffman Table
# Huffman Table
# Start of Scan
# End of Image
```


# Tổng kết

Chúc bạn thành công!

-----
Tham khảo:
- [Decoding binary data structure](https://reverseengineering.stackexchange.com/questions/15969/decoding-binary-data-structure)
- [Understanding and Decoding a JPEG Image using Python](https://yasoob.me/posts/understanding-and-writing-jpeg-decoder-in-python/)
- [DCode™ – Timestamp Decoder](https://www.digital-detective.net/dcode/)
- [图片的 Metadata 与网站性能优化](https://github.com/shfshanyue/blog/blob/master/web-performance/image-metadata.md)
