---
layout: post
categories: ["Trí tuệ nhân tạo & Dữ liệu"]
title: AI - Lộ trình học Machine Learning Cơ Bản đến Nâng Cao
subtitle: Artificial Intelligence - A Comprehensive Guide
author: "TAn"
image: "img/lonely.jpg"
tags:
- Python
- Scripting
- Data Science
- Machine Learning
- Big Data
- Hadoop
- MapReduce
- TensorFlow
- Scikit-Learn
- NumPy
- Keras
- PyTorch
- SciPy
- Pandas
- Matplotlib
- Seaborn
- Bokeh
- Pillow
- Data Analyst
- Chuyên viên Phân tích Dữ liệu
- Data Scientist
- Nhà Khoa học Dữ liệu
- Machine Learning Engineer
- Kĩ sư Học máy
- Artificial Intelligence Engineer
- Kĩ sư Trí tuệ Nhân tạo
---

# I. Mục lục

- [I. Mục lục](#i-mục-lục)
- [II. Giới thiệu](#ii-giới-thiệu)
	- [Aritifical Intelligient](#aritifical-intelligient)
	- [Machine learning](#machine-learning)
	- [Học sâu (Deep learning)](#học-sâu-deep-learning)
	- [Ứng dụng của học máy](#ứng-dụng-của-học-máy)
	- [Ứng dụng cụ thể](#ứng-dụng-cụ-thể)
	- [Các dạng học máy](#các-dạng-học-máy)
		- [Học có giám sát (supervised learning)](#học-có-giám-sát-supervised-learning)
		- [Học không giám sát (un-supervised learning)](#học-không-giám-sát-un-supervised-learning)
		- [Học bán giám sát (semi-supervised learning)](#học-bán-giám-sát-semi-supervised-learning)
		- [Học tăng cường (reinforcement learning)](#học-tăng-cường-reinforcement-learning)
- [III. Lộ trình học machine learning](#iii-lộ-trình-học-machine-learning)
	- [1. Các kiến thức về toán học căn bản](#1-các-kiến-thức-về-toán-học-căn-bản)
	- [2. Muốn tạo AI, cần phải chuẩn bị những gì, env như thế nào](#2-muốn-tạo-ai-cần-phải-chuẩn-bị-những-gì-env-như-thế-nào)
		- [Những tool tiện lợi trong quá trình phát triển AI](#những-tool-tiện-lợi-trong-quá-trình-phát-triển-ai)
			- [Anaconda](#anaconda)
		- [Library sử dụng trong machine learning](#library-sử-dụng-trong-machine-learning)
			- [TensorFlow](#tensorflow)
		- [List software sử dụng để tạo ra AI](#list-software-sử-dụng-để-tạo-ra-ai)
			- [AutoML](#automl)
			- [Neural Network Console](#neural-network-console)
			- [AI maker](#ai-maker)
	- [3. Học gì bây giờ](#3-học-gì-bây-giờ)
		- [Học lý thuyết](#học-lý-thuyết)
			- ["RECOMMENDED COURSES" của Machine Learning cơ bản](#recommended-courses-của-machine-learning-cơ-bản)
				- [Machine Learning - Andrew Ng](#machine-learning---andrew-ng)
				- [CS224n: Natural Language Processing with Deep Learning](#cs224n-natural-language-processing-with-deep-learning)
				- [CS231n: Convolutional Neural Networks for Visual Recognition](#cs231n-convolutional-neural-networks-for-visual-recognition)
				- [CS246: Mining Massive Data Sets](#cs246-mining-massive-data-sets)
				- [CS20SI: Tensorflow for Deep Learning Research](#cs20si-tensorflow-for-deep-learning-research)
				- [Introduction to Computer Science and Programming Using Python](#introduction-to-computer-science-and-programming-using-python)
				- ["Machine Learning cơ bản", Vũ Hữu Tiệp](#machine-learning-cơ-bản-vũ-hữu-tiệp)
				- ["Machine Learning cơ bản", Vũ Hữu Tiệp](#machine-learning-cơ-bản-vũ-hữu-tiệp-1)
		- [Lập trình những thứ đã học](#lập-trình-những-thứ-đã-học)
			- [Đọc Documentation](#đọc-documentation)
			- [Xem video Youtube](#xem-video-youtube)
			- [Đọc trang tin, blog, tạp chí](#đọc-trang-tin-blog-tạp-chí)
			- [Trang web, khóa học online về Machine Learning](#trang-web-khóa-học-online-về-machine-learning)
	- [4. Cập nhật kiến thức trong lĩnh vực Machine Learning](#4-cập-nhật-kiến-thức-trong-lĩnh-vực-machine-learning)
		- [a) Blog](#a-blog)
			- [Machine Learning cơ bản](#machine-learning-cơ-bản)
			- [CS231n](#cs231n)
			- [Understanding LSTM Networks](#understanding-lstm-networks)
			- [The Unreasonable Effectiveness of Recurrent Neural Networks](#the-unreasonable-effectiveness-of-recurrent-neural-networks)
			- [Exploring LSTMs](#exploring-lstms)
			- [Toward Data Science](#toward-data-science)
			- [InsightData](#insightdata)
			- [OpenAI](#openai)
			- [WildML](#wildml)
			- [Distill.pub](#distillpub)
			- [Colah's blog](#colahs-blog)
			- [Lilianweng's blog](#lilianwengs-blog)
			- [Ruder's blog](#ruders-blog)
			- [Echen's blog](#echens-blog)
			- [AI Google Blog](#ai-google-blog)
		- [b) Newsletter](#b-newsletter)
			- [DataMachina](#datamachina)
			- [Analytic Vidhya](#analytic-vidhya)
			- [Paper with code](#paper-with-code)
			- [Data Elixir](#data-elixir)
			- [AI Weekly](#ai-weekly)
			- [Sebastian Ruder](#sebastian-ruder)
			- [Mybridge](#mybridge)
			- [...](#)
			- [HackerNews](#hackernews)
			- [Python Weekly](#python-weekly)
		- [c) Social network](#c-social-network)
			- [① Twitter](#-twitter)
				- [Yann Lecun](#yann-lecun)
				- [Ian Goodfellow](#ian-goodfellow)
				- [Fchollet](#fchollet)
				- [Jakevdp](#jakevdp)
				- [PyImageSearch](#pyimagesearch)
				- [Jeremy Phoward](#jeremy-phoward)
			- [② Medium](#-medium)
			- [③ Reddit](#-reddit)
				- [r/MachineLearning](#rmachinelearning)
			- [④ Quora](#-quora)
			- [⑤ Facebook](#-facebook)
				- [Forum Machine Learning cơ bản](#forum-machine-learning-cơ-bản)
				- [MontrealAI](#montrealai)
				- [Data Science and Big Data Vietnam](#data-science-and-big-data-vietnam)
				- [Cộng đồng xử lí ngôn ngữ tự nhiên](#cộng-đồng-xử-lí-ngôn-ngữ-tự-nhiên)
			- [⑥ Youtube](#-youtube)
				- [Two Minute Papers](#two-minute-papers)
				- [Giant Neural Network](#giant-neural-network)
				- [Deep Learning dot AI](#deep-learning-dot-ai)
				- [Hvass Laboratories](#hvass-laboratories)
				- [Code Bullet](#code-bullet)
				- [3Blue1Brown](#3blue1brown)
				- [DeepMind](#deepmind)
		- [d) Các phương tiện khác](#d-các-phương-tiện-khác)
			- [Github](#github)
			- [Google Scholar](#google-scholar)
			- [Antiny-Sanity](#antiny-sanity)
			- [Facebook Research](#facebook-research)
			- [Researchgate](#researchgate)
			- [Sun\* AI Research Team](#sun-ai-research-team)
	- [5. Nhà tuyển dụng cần gì](#5-nhà-tuyển-dụng-cần-gì)
- [Tổng kết](#tổng-kết)


Trí tuệ nhân tạo (Aritifical Intelligient), Máy học (Machine learning), Học sâu (Deep Learning) là 3 thuật ngữ rất hot trong những năm gần đây.

![Andrew Ng](https://boxxv.github.io/img/ai/383785053_3647796478810524_1790389580654847815_n.jpg "Andrew Ng")

# II. Giới thiệu

Phân biệt Artificial Intelligence, Machine Learning và Deep Learning

Sự khác nhau giữa AI, ML, DL

## Aritifical Intelligient

AI đã tồn tại trong một thời gian dài - thần thoại Hy lạp có những câu chuyện về những người máy được thiết kế để bắt chước các hành động của chúng ta. Rất sớm ở châu âu các máy tính được hình thành được gọi là "máy logic" và bằng cách tái tạo các khả năng như số học cơ bản và bộ nhớ, về cơ bản là cố gắng tạo ra một bộ não cơ học.

Được định nghĩa vào năm 1956 bởi John MacCarthy, AI bao gồm các máy có thể thực hiện các tác vụ mà có các đặc trưng của trí thông minh của con người.

AI thường được phân loại thành 1 trong 2 nhóm cơ bản - **Applied** hoặc **General**
- `Applied AI` rất phổ biến, là các hệ thống được thiết kế để giao dịch chứng khoán và cổ phiếu một cách thông minh, hoặc tự điều khiển một chiếc xe, ...
- `Generalized AI` ít phổ biến hơn, là các hệ thống hoặc các thiết bị về lý thuyết có thể xử lý mọi tác vụ, nhưng đây là nơi mà những sự tiến bộ thú vị nhất đang diễn ra hiện nay. Nó cũng là nơi dẫn đến sự phát triển của ML

## Machine learning

Về cơ bản, máy học đơn giản là cách để đạt được AI.

Được định nghĩa bởi Arthur Samuel vào năm 1959, không lâu sau khi AI được định nghĩa. Nó được định nghĩa "là khả năng để máy tự học mà không cần phải lập trình". 

Bạn có thể có AI mà không cần dùng ML, nhưng sẽ cần hàng triệu dòng code để xây dựng với các quy tắc phức tạp và các cây quyết định.

Do vậy thay cho việc code các chương trình phần mềm với các chỉ dẫn cụ thể để hoàn thành một nhiệm vụ cụ thể, thì ML là một cách đào tạo một thuật toán để nó biết cách học. 

Đào tạo bao gồm việc cho thuật toán truy xuất vào một khối lượng lớn dữ liệu và cho phép thuật toán tự phân tích, điều chỉnh và cải thiện.

Ví dụ: ML được dùng để cải tiến mạnh mẽ tầm nhìn của máy tính (khả năng của máy có thể nhận ra một đối tượng trong ảnh hoặc video). 

Bạn thu thập hàng trăm, hàng nghìn thậm chí là hàng triệu bức ảnh và sau đó cho con người phân loại chúng. Ở đây, con người có thể phân loại các bức ảnh thành 2 nhóm là nhóm có mèo và nhóm ko có mèo, xuất hiện trong ảnh.

Sau đó thuật toán sẽ xây dựng một model có thể phân loại chính xác bức ảnh nào có mèo hay ko có mèo, giống như con người. 

Một khi mà độ chính xác đủ cao thì lúc đó ML đã học được đâu là con mèo.

## Học sâu (Deep learning)

DL là một trong nhiều cách để tiếp cận đến ML. 

Các cách tiếp cận khác bao gồm cây học tập quyết đinh (decision tree learning), lập trình logic quy nạp (inductive logic programming), phân cụm (clustering), học tăng cường (reinforcement learning), và mạng Bayesian, ...

DL được lấy cảm hứng từ cấu trúc và chức năng của bộ não, ở đây là sự kết nối của các tế bào thần kinh.

Mạng thần kinh nhân tạo (Artifical Neural Networks - ANNs) là thuật toán mô phỏng cấu trúc sinh học của bộ não. Trong ANNs, có các neuron thần kinh có các lớp riêng rẽ và được kết nối với các neuron khác. 

Sự phát triển của neural network là chìa khóa để dạy máy tính nghĩ và hiểu thế giới như cách của chúng ta làm, trong khi vẫn giữ được những lợi thế như tốc độ, độ chính xác và thiếu thiên hướng.

Về cơ bản nó làm việc trên một hệ thống xác suất - dựa trên dữ liệu được cung cấp, nó có thể đưa ra các tuyên bố, quyết định hoặc tiên đoán với một mức độ chắc chắn. Việc bổ sung một vòng lặp phản hồi cho phép học - bằng cách tự nhận biết hoặc được cho biết là quyết định đúng hay sai, nó sẽ thay đổi cách tiếp cận trong tương lai.



## Ứng dụng của học máy

Có rất nhiều ứng dụng thực tế khác nhau của học máy. Hai lĩnh vực ứng dụng lớn nhất của học máy là khai phá dữ liệu (`Data Mining`) và nhận dạng mẫu (`Pattern Recognition`).

**Khai phá dữ liệu** là ứng dụng kỹ thuật học máy vào các cơ sở dữ liệu hoặc các tập dữ liệu lớn để phát hiện quy luật hay tri thức trong dữ liệu đó hoặc để dự đoán các thông tin quan tâm trong tương lai. Ví dụ, từ tập hợp hóa đơn bán hàng có thể phát hiện ra quy luật “những người mua bánh mì thường mua bơ”.

**Nhận dạng mẫu** là ứng dụng các kỹ thuật học máy để phát hiện các mẫu có tính quy luật trong dữ liệu, thường là dữ liệu hình ảnh, âm thanh. Bài toán nhận dạng mẫu cụ thể thường là xác định nhãn cho đầu vào cụ thể, ví dụ cho ảnh chụp mặt người, cần xác định đó là ai.

Cần lưu ý, khai phá dữ liệu và nhận dạng mẫu có nhiều điểm trùng nhau cả trong phạm vi nghiên cứu và ứng dụng. Điểm khác nhau chủ yếu liên quan tới lĩnh vực ứng dụng và kỹ thuật sử dụng, theo đó khai phá dữ liệu liên quan tới dữ liệu thương mại trong khi nhận dạng mẫu liên quan nhiều tới dữ liệu âm thanh, hình ảnh và được dùng nhiều trong kỹ thuật.

## Ứng dụng cụ thể

- Nhận dạng ký tự: phân loại hình chụp ký tự thành các loại, mỗi loại ứng với một ký tự tương ứng.
- Phát hiện và nhận dạng mặt người: phát hiện vùng có chứa mặt người trong ảnh, xác định đó là mặt người nào trong số những người đã có ảnh trước đó, tức là phân chia ảnh thành những loại tương ứng với những người khác nhau.
- Lọc thư rác, phân loại văn bản: dựa trên nội dung thư điện tử, chia thư thành loại “thư rác” hay “thư bình thường”; hoặc phân chia tin tức thành các thể loại khác nhau như “xã hội”, “kinh tế”, “thể thao”.v.v.
- Dịch tự động: dựa trên dữ liệu huấn luyện dưới dạng các văn bản song ngữ, hệ thống dịch tự động học cách dịch từ ngôn ngữ này sang ngôn ngữ khác. Hệ thống dịch tự động tiêu biểu dạng này là Google Translate.
- Chẩn đoán y tế: học cách dự đoán người bệnh có mắc hay không mắc một số bệnh nào đó dựa trên triệu chứng quan sát được.
- Phân loại khách hàng và dự đoán sở thích: sắp xếp khách hàng vào một số loại, từ đây dự đoán sở thích tiêu dùng của khách hàng.
- Dự đoán chỉ số thí trường: căn cứ giá trị một số tham số hiện thời và trong lịch sử, đưa ra dự đoán, chẳng hạn dự đoán giá chứng khoán, giá vàng.v.v.
- Các hệ khuyến nghị, hay hệ tư vấn lựa chọn: cung cấp một danh sách ngắn các loại hàng hóa, phim, video, tin tức v.v. mà người dùng nhiều khả năng quan tâm. Ví dụ ứng dụng loại này là phần khuyến nghị trên Youtube hay trên trang mua bán trực tuyến Amazon.
- Ứng dụng lái xe tự động: dựa trên các mẫu học chứa thông tin về các tình huống trên đường, hệ thống học máy cho phép tự ra quyết định điều khiển xe, và do vậy không cần người lái. Hiện Google đã có kế hoạch thương mại hóa xe ôtô tự động lái như vậy.

![AI](https://boxxv.github.io/img/ai/machine-learning.png "AI")

## Các dạng học máy

Khi thiết kế và xây dựng hệ thống học máy cần quan tâm tới những yếu tố sau.
– Thứ nhất, kinh nghiệm hoặc dữ liệu cho học máy được cho dưới dạng nào?
– Thứ hai, lựa chọn biểu diễn cho hàm đích ra sao? Hàm đích có thể biểu diễn dưới dạng hàm đại số thông thường nhưng cũng có thể biểu diễn dưới những dạng khác như dạng cây, dạng mạng nơ ron, công thức xác suất .v.v.

Việc sử dụng những dạng kinh nghiệm và dạng biểu diễn khác nhau dẫn tới những dạng học máy khác nhau. Có ba dạng học máy chính như sau:

### Học có giám sát (supervised learning)

Là dạng học máy trong đó cho trước tập dữ liệu huấn luyện dưới dạng các ví dụ cùng với giá trị đầu ra hay giá trị đích. Dựa trên dữ liệu huấn luyện, thuật toán học cần xây dựng mô hình hay hàm đích để dự đoán giá trị đầu ra (giá trị đích) cho các trường hợp mới.

- Nếu giá trị đầu ra là rời rạc thì học có giám sát được gọi là phân loại hay phân lớp (classification).
- Nếu đầu ra nhận giá trị liên tục, tức đầu ra là số thực, thì học có giám sát được gọi là hồi quy (regression). Trong phần tiếp theo, ta sẽ xem xét chi tiết hơn về học có giám sát.

### Học không giám sát (un-supervised learning)

Là dạng học máy trong đó các ví dụ được cung cấp nhưng không có giá trị đầu ra hay giá trị đích.

- Thay vì xác định giá trị đích, thuật toán học máy dựa trên độ tương tự giữa các ví dụ để xếp chúng thành những nhóm, mỗi nhóm gồm các ví dụ tương tự nhau. Hình thức học không giám sát như vậy gọi là phân cụm (clustering). Ví dụ, chỉ bằng cách quan sát hoặc đo chiều cao của mọi người, dần dần ta học được khái niệm “người cao” và “người thấp”, và có thể xếp mọi người vào hai cụm tương ứng.
- Ngoài phân cụm, một dạng học không giám sát phổ biến khác là phát hiện luật kết hợp (association rule). Luật kết hợp có dạng P(A | B), cho thấy xác suất hai tính chất A và B xuất hiện cùng với Ví dụ, qua phân tích dữ liệu mua hàng ở siêu thị, ta có luật P(Bơ | Bánh mỳ) =80%, có nghĩa là 80% những người mua bánh mỳ cũng mua bơ.

### Học bán giám sát (semi-supervised learning)

Học bán giám sát là việc chúng ta có một khối lượng dữ liệu đầu vào (input) mà chỉ một phần trong đó là các dữ liệu được gắn nhãn. Học bán giám sát nằm ở giữa hai loại học có giám sát và học không giám sát. Bài toán này thường phát sinh trong thực tế bởi các dữ liệu hầu như hiếm khi được gắn nhãn toàn bộ, các dữ liệu gắn nhãn thường tốn nhiều thời gian và chi phí hơn so với các dữ liệu không gắn nhãn.

### Học tăng cường (reinforcement learning)

Đối với dạng học này, kinh nghiệm không được cho trực tiếp dưới dạng đầu vào/đầu ra cho mỗi trạng thái hoặc mỗi hành động. Thay vào đó, hệ thống nhận được một giá trị khuyến khích (reward) là kết quả cho một chuỗi hành động nào đó. Thuật toán cần học cách hành động để cực đại hóa giá trị khuyển khích. Ví dụ của học khuyến khích là học đánh cờ, trong đó hệ thống không được chỉ dẫn nước đi nào là hợp lý cho từng tình huống mà chỉ biết kết quả toàn ván cờ. Như vậy, các chỉ dẫn về nước đi được cho một cách gián tiến và có độ trễ dưới dạng giá trị thưởng. Nước đi tốt là nước đi nằm trong một chuỗi các nước đi dẫn tới kết quả thắng toàn bộ ván cờ.

Trong các dạng học máy, học có giám sát là dạng phổ biến, có nhiều thuật toán liên quan và nhiều ứng dụng nhất.

# III. Lộ trình học machine learning

![AI](https://boxxv.github.io/img/2023/ai-data-scientist.jpg "AI")


## 1. Các kiến thức về toán học căn bản

   + Xác xuất thống kê
   + Giải tích
   + Đại số tuyến tính
   + vector, ma trận, đạo hàm (chain rule và production rule)
   + xác suất sử dụng không gian mẫu, xác suất có điều kiện, biến ngẫu nhiên, phân phối xác xuất...
- Kỹ năng về ngôn ngữ lập trình
   + Python
   + R
   + Lisp
   + Prolog
   + Java
- Xây dựng được các model cơ bản
   + NumPy
   + Keras
   + Tensoflow
   + Scikit Learn
- Tìm hiểu về Machine Learning thông qua các khoá học online và offline
- Trao đổi và luyện tập trên các diễn đàn
   + Github
   + Stack Overflow
   + Dev.to
   + Quora


## 2. Muốn tạo AI, cần phải chuẩn bị những gì, env như thế nào

### Những tool tiện lợi trong quá trình phát triển AI

#### Anaconda

`Anaconda`: Tập hợp rất nhiều tool tiện lợi trong quá trình phát triển machine learning và data science. Bao gồm cả môi trường phát triển với Python, và các tool editer. Có thể install các tool cần thiết từ Anaconda.

Lợi ích của Anaconda:
- Dễ dàng tải 1500+ packages về Python/R cho data science
- Quản lý thư viện, môi trường và dependency giữa các thư viện dễ dàng
- Dễ dàng phát triển mô hình machine learning và deep learning với scikit-learn, tensorflow, keras
- Xử lý dữ liệu tốc độ cao với numpy, pandas
- Hiện thị kết quả với Matplotlib, Bokeh

### Library sử dụng trong machine learning

#### TensorFlow

`TensorFlow` chính là thư viện mã nguồn mở cho machine learning nổi tiếng nhất thế giới, được phát triển bởi các nhà nghiên cứu từ Google. Việc hỗ trợ mạnh mẽ các phép toán học để tính toán trong machine learning và deep learning đã giúp việc tiếp cận các bài toán trở nên đơn giản, nhanh chóng và tiện lợi hơn nhiều.

Các hàm được dựng sẵn trong thư viện cho từng bài toán cho phép TensorFlow xây dựng được nhiều neural network. Nó còn cho phép bạn tính toán song song trên nhiều máy tính khác nhau, thậm chí trên nhiều CPU, GPU trong cùng 1 máy hay tạo ra các dataflow graph – đồ thị luồng dữ liệu để dựng nên các model. Nếu bạn muốn chọn con đường sự nghiệp trong lĩnh vực A.I. này, nắm rõ những điều cơ bản của TensorFlow thực sự rất quan trọng.

Được viết bằng C++ và thao tác interface bằng Python nên phần performance của TensorFlow cực kỳ tốt. Đối tượng sử dụng nó cũng đa dạng không kém: từ các nhà nghiên cứu, nhà khoa học dữ liệu và dĩ nhiên không thể thiếu các lập trình viên.

### List software sử dụng để tạo ra AI

Đến đây chúng ta đã nắm được phần nào về cách phát triển AI thông qua các tool, lib... . Vậy liệu có phầm mềm nào giúp chúng ra trong việc tạo AI hay không ? Chắc hẳn không ít người thắc mắc câu hỏi này. Tuỳ theo việc phát tiển theo các lĩnh vực khác nhau. Chúng tôi xin phép giói thiệu một số Web service tiện lợi dưới đây.

#### AutoML

AutoML tiện lợi trong việc tạo model

Model được ví như đầu não trong AI. Ứng với việc input data nguồn sẽ xuất ra câu trả lời tương ứng. AutoML là web service được Google cung cấp, bạn không cần có kiến thức về machine learning. Chỉ với lượng data cần tiết, có thể hoàn toàn tự động tạo model machine learning.

#### Neural Network Console

Neural Network Console là môi trường tích hợp có thể tạo ra các program Deep learning được cung cấp bởi Sony. Một ví dụ về Deep learning: Chúng ta đang muốn học sâu hơn về đối tượng "con mèo đen". Thì khi tiến hành học sâu sẽ là, nhìn con mèo đen ở trong bóng tối thì màu sắc sẽ khác con mèo đen ở nơi có ánh sáng. Mặc dù cùng là con mèo đen. Vì vậy cần phải thiết lập sao cho, độ ưu tiên liên quan đến màu sắc của con mèo ở những vùng ánh sáng khác nhau để model sẽ hiểu rõ và phân biệt một cách chính xác hơn. Đây là một ví dụ nói về mối liên hệ giữa thông tin với thông tin With neural network.

#### AI maker

Là một flatform mà khi sử dụng nó ai cũng có thể phát triển machine learning một cách nhẹ nhàng. Bạn có thể tìm hiểu sâu hơn tại : https://aimaker.io/

Tựu lại để tạo ra AI có thể hình dung gồm 3 công đoạn sau đây:  
① Chuẩn bị lượng data lớn để tiến hành cho learning.  
② Tiến hành train model bởi machine learning  
③ Đặt câu hỏi với train model và đưa ra kết qủa.


## 3. Học gì bây giờ

### Học lý thuyết

Như chia sẻ ở trên, sau khi đọc bài [Linear Regression](https://machinelearningcoban.com/2016/12/28/linearregression/), mình khá shock. Chia sẻ thật lòng, nếu bạn giỏi toán, học full Đại số tuyến tính, Giải tích 1, 2 này nọ rồi thì nên đọc blog đó của anh Tiệp - một nơi với lượng kiến thức khá đầy đủ, tiếng Việt 100%, đương nhiên độ chính xác khỏi phải bàn. Còn mình thì hơi kém, nên lúc đó hoang mang thật.

May sao, bằng 1 cách nào đấy (thực ra trong phần "RECOMMENDED COURSES" của Machine Learning cơ bản) mà mình biết đến thầy Andrew Ng và khóa [Machine Learning](https://www.coursera.org/learn/machine-learning) thần thánh. Cảm giác cách giảng của thầy học sinh cấp 3 cũng hiểu được. Mình nghĩ khóa học này của thầy Andrew Ng là cách tốt nhất để bắt đầu hành trình Machine Learning

#### "RECOMMENDED COURSES" của Machine Learning cơ bản

##### [Machine Learning](https://www.coursera.org/learn/machine-learning) - Andrew Ng
##### [CS224n: Natural Language Processing with Deep Learning](http://web.stanford.edu/class/cs224n/)
##### [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/)
##### [CS246: Mining Massive Data Sets](http://web.stanford.edu/class/cs246/)
##### [CS20SI: Tensorflow for Deep Learning Research](http://web.stanford.edu/class/cs20si/syllabus.html)
##### [Introduction to Computer Science and Programming Using Python](https://www.edx.org/learn/computer-programming/massachusetts-institute-of-technology-introduction-to-computer-science-and-programming-7)
##### ["Machine Learning cơ bản", Vũ Hữu Tiệp](https://github.com/tiepvupsu/ebookMLCB/blob/master/book_ML.pdf)
##### ["Machine Learning cơ bản", Vũ Hữu Tiệp](https://github.com/tiepvupsu/ebookMLCB/blob/master/book_ML_color.pdf)

Mình để phần này ở mục "học lý thuyết" vì đó là thứ gần như là duy nhất trong khóa học thần thánh kia. Thầy code bằng Octave, và giờ mình không chắc có doanh nghiệp nào dùng nó không nữa. Không trách thầy được, vì khóa này từ năm 2012 mà.

Vậy giờ học code thế nào?

### Lập trình những thứ đã học

2 Framework nổi tiếng nhất và được sử dụng rộng rãi nhất là `Tensorflow` và `Pytorch`. Mình thì học Tensorflow, và giờ đang học cả Pytorch trong khi thực tập. Mình sẽ không đi sâu vào chúng cả 2 ở các bài viết kế tiếp, vì có cả triệu bài viết, video, tài liệu về chúng trên Internet, từ những người giỏi hơn mình rất nhiều.

Nhưng mình sẽ đề cập chút đến cách học, vì mình mong các bạn sẽ học nhanh và nhẹ nhàng hơn những gì mình trải qua. Với mình, thường khi học một công nghệ mới trong ngành IT, sẽ có 4 công cụ thường được tìm đến (ít nhất theo những gì mình biết):

#### Đọc Documentation

Đầu tiên là documentation (hoặc paper) của công nghệ đó: thực ra nó khá nặng, và đến giờ mình vẫn khá ít dùng cách này để học kiến thức mới. Có lẽ sau này mình cũng phải dùng thôi, nhưng nếu bắt đầu học Machine Learning mà đọc docs (paper) thì dễ nản lắm, vừa khó hiểu vừa lê thê.

#### Xem video Youtube

Tiếp theo là xem video (đặc biệt Youtube) của mấy anh Ấn Độ: phải nói là tuyệt vời. Thậm chí ta có thể vừa đọc lý thuyết, vừa code theo. Mình đặc biệt recommend [https://www.youtube.com/user/krishnaik06](https://www.youtube.com/user/krishnaik06) và [https://www.youtube.com/c/codebasics](https://www.youtube.com/c/codebasics). Có đủ mọi thứ, chỉ cần thêm sự kiên nhẫn của bạn thôi. À có hơi ngại việc code theo, nhưng coi như đó là cơ hội đi, dù sao tự tay code cũng giúp nhớ lâu hơn. Nếu bạn thấy lâu quá, có thể kiếm Github của 2 anh trên, ở đó có hết code của các video. Mình biết đấy, nhưng thôi, nói làm gì, tự code đi nào 😃

#### Đọc trang tin, blog, tạp chí

Thứ 3 là các bài viết về công nghệ trên các trang tin, blog, tạp chí...: này thì copy code thoải mái, đọc cũng nhanh hơn (nhưng dù sao thì xem video, có người giảng có lẽ vẫn dễ hiểu hơn với nhiều người). Nếu bạn muốn học bằng cách này, có thể lên cách trang như `Medium` hay [Towards Data Science](https://towardsdatascience.com) (nếu bị chặn thì bật vpn hoặc lên proxysite.com nha). Nhược điểm khá nghiêm trọng là kiến thức rời rạc, ít có hệ thống, và độ khó xen lẫn. Nó không theo 1 trình tự, series như documentation hoặc các series từ dễ đến khó trên Youtube.

#### Trang web, khóa học online về Machine Learning

Cuối cùng là các trang web, khóa học online về Machine Learning: Đây có thể coi là "best solution", vì kiến thức được sắp xếp hệ thống, có cả code và lý thuyết, thậm chí có cả các cộng đồng theo sau ủng hộ (có thể hỏi đáp thắc mắc, tư vấn đủ thứ,...). Về các trang web chia sẻ kiến thức ML, mình nghĩ [Mì AI](https://miai.vn) và [Machine Learning cơ bản](https://machinelearningcoban.com) sẽ phù hợp nhất với người bắt đầu. Vẫn cần solution phù hợp hơn ư, vậy hãy đến với các khóa học online ở `Coursera`, `Udemy`, hoặc các khóa học của `Google` (ví dụ trên [link này](https://developers.google.com/learn?product=tensorflow) chẳng hạn, học ổn phết mà lại free, mỗi tội hơi ít lý thuyết)


## 4. Cập nhật kiến thức trong lĩnh vực Machine Learning

### a) Blog

#### [Machine Learning cơ bản](https://machinelearningcoban.com)
#### [CS231n](https://cs231n.github.io/convolutional-networks/)
#### [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
#### [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
#### [Exploring LSTMs](http://blog.echen.me/2017/05/30/exploring-lstms/)
#### [Toward Data Science](https://towardsdatascience.com)
#### [InsightData](https://blog.insightdatascience.com)
#### [OpenAI](https://openai.com/blog)
#### [WildML](https://dennybritz.com)
#### [Distill.pub](https://distill.pub)
#### [Colah's blog](http://colah.github.io)
#### [Lilianweng's blog](https://lilianweng.github.io)
#### [Ruder's blog](https://www.ruder.io)
#### [Echen's blog](http://blog.echen.me)
#### [AI Google Blog](https://blog.research.google)

### b) Newsletter

#### [DataMachina](https://datamachina.com)
#### [Analytic Vidhya](https://www.analyticsvidhya.com)
#### [Paper with code](https://paperswithcode.com)
#### [Data Elixir](https://dataelixir.com)
#### [AI Weekly](https://aiweekly.co)
#### [Sebastian Ruder](https://www.ruder.io)
#### [Mybridge](https://medium.mybridge.co)
#### [...]()

Một vài newsletter liên quan khác:

#### [HackerNews](https://hackernewsletter.com)
#### [Python Weekly](https://www.pythonweekly.com)

### c) Social network

#### ① Twitter

##### [Yann Lecun](https://twitter.com/ylecun)

Chief Artificial Intelligence Scientist at Facebook AI Research (FAIR)

##### [Ian Goodfellow](https://twitter.com/goodfellow_ian)

Google Brain Researcher. Tác giả cuốn sách nổi tiếng trong giới Deep Learning: [Deep Learning Book](https://www.deeplearningbook.org/)

##### [Fchollet](https://twitter.com/fchollet)

Deep Learning Researcher at Google. Tác giả thư viện Deep Learning Keras.

##### [Jakevdp](https://twitter.com/jakevdp)

Tác giả cuốn sách được recommend rất nhiều trong giới Data Science: [Python DataScience Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)

##### [PyImageSearch](https://twitter.com/PyImageSearch)

Computer Vision Researcher. Tác giả nổi tiếng trong giới Computer Vision. Tác giả 2 cuốn sách bestseller: [Deep Learning for Computer Vision](https://pyimagesearch.com/deep-learning-computer-vision-python-book/) và [Practical Computer Vision with Python and Opencv](https://pyimagesearch.com/practical-python-opencv/)

##### [Jeremy Phoward](https://twitter.com/jeremyphoward)

Founder của [fast.ai](https://www.fast.ai/), khoá MOOC về Deep Learning và thư viện mã nguồn mở nổi tiếng fastai, base trên nền Pytorch.

Các bạn có thể tham khảo những tác giả, nhân vật nổi tiếng trong giới ML, DL trong link sau: [50 AI Influencers to follow on Twitter](https://www.cognilytica.com/wp-content/uploads/2018/06/50-AI-Influencer-For-image-version-copy-2.pdf)

Hoặc mọi người có thể follow mình trên Twitter, mình tweet và retweet khá nhiều các bài post về ML, DL mà mình thấy hay và có hứng thú: [__phanhoang__](https://twitter.com/__phanhoang__)

#### ② Medium

#### ③ Reddit

##### [r/MachineLearning](https://www.reddit.com/r/MachineLearning/)

#### ④ Quora

#### ⑤ Facebook

##### [Forum Machine Learning cơ bản](https://www.facebook.com/groups/machinelearningcoban)
##### [MontrealAI](https://www.facebook.com/groups/MontrealAI/)
##### [Data Science and Big Data Vietnam](https://www.facebook.com/groups/870665749718859)
##### [Cộng đồng xử lí ngôn ngữ tự nhiên](https://www.facebook.com/groups/vietnlp)

#### ⑥ Youtube

##### [Two Minute Papers](https://www.youtube.com/user/keeroyz)

Paper review channel. 1 trong những channel mình thấy thích nhất. Channel tập trung làm các video ngắn, trên dưới 5 phút, nhằm review qua các paper đạt được các thành tựu nhất định trong thời gian gần đây.

##### [Giant Neural Network](https://www.youtube.com/channel/UCrBzGHKmGDcwLFnQGHJ3XYg)

Introduction to Neural Network. Ô này có loạt bài giới thiệu về Neural Network, các bạn có thể xem tại đây

##### [Deep Learning dot AI](https://www.youtube.com/channel/UCcIXc5mJsHVYTZR1maL5l9w)

Deep Learning course by Andrew Y. Ng (Stanford). Gồm các video bài giảng trong khoá học về Deep Learning của Andrew Y. Ng trên coursena, các bạn có thể tham khảo khoá học tại đây

##### [Hvass Laboratories](https://www.youtube.com/channel/UCbba38V6vcglqVL--8kVVmg)

Tensorflow Tutorial. Ô này có loạt bài về Tensorflow mà mình thấy vô cùng ưng ý.

##### [Code Bullet](https://www.youtube.com/channel/UC0e3QhIYukixgh5VVpKHH9Q)

Reinforcement Learning

##### [3Blue1Brown](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)

Introduction to Neural Network

##### [DeepMind](https://www.youtube.com/channel/UCP7jMXSY2xbc3KCAE0MHQ-A)

### d) Các phương tiện khác

#### [Github](https://github.com)

Bằng việc follow các tác giả nổi tiếng hay main contributor của các project, mỗi khi họ tạo mới, commit, push, cho star hay fork bất kì 1 repo sẽ đều hiện lên bảng tin bên github của bạn. 1 cách thức khác các bạn có thể thực hiện là nhấn Watch đối với những repo bạn quan tâm hoặc muốn contributor cho project đó; bất kì 1 commit nào được thực hiện trên repo gốc, bạn sẽ đều nhận được thông báo.

#### [Google Scholar](https://scholar.google.ca)

Bạn follow các tác giả mà bạn quan tâm, có thể tuỳ chọn thông báo qua email về các bài viết mới, các lời trích dẫn đến tác giả hoặc các bài viết mới liên quan đến nghiên cứu của tác giả này.

#### [Antiny-Sanity](https://arxiv-sanity-lite.com)

Gồm các paper trending theo thời gian. 1 điểm khá hay là tác giả cũng build 1 mục recommend các paper có liên quan dựa trên các paper bạn đã save lại.

#### [Facebook Research](https://research.fb.com/)

#### [Researchgate](https://www.researchgate.net/)

#### [Sun* AI Research Team](https://viblo.asia/o/sun-ai-research-team)

## 5. Nhà tuyển dụng cần gì

Sun* Inc. (Sun Asterisk Inc.) - Fresher Machine Learning (Full Time)

**Mô tả công việc**
- Tham gia nhóm phát triển sản phẩm về AI
- Phát triển, tích hợp các mô hình AI vào trong các sản phẩm phần mềm
- Triển khai, vận hành và bảo trì các sản phẩm phần mềm trong môi trường thực tế

**Yêu cầu ứng viên**
1. Hiểu và có thể vận dụng những kiến thức về:

   + Linear/Logistic Regressions, Decision Tree, K-means clustering, K-nearest neighbors, Naive Bayes, SVM,…

   + Các building blocks cho model: Linear (Dense), Convolutional layer, Activation functions, Convolutional Network, Recurrent Neural Network (GRU/LSTM), Attention, Transformers, …

   + Các khái niệm liên quan đến quá trình training: Gradient Descent, Loss functions

   + Các khái niệm liên quan đến quá trình evaluation: Metrics đánh giá, Overfitting/Underfitting, Data snooping

2. Có kinh nghiệm làm việc trong các quy trình phát triển phần mềm Agile, Scrum

3. Thành thạo ít nhất một trong các AI framework: Tensorflow, Keras, Pytorch.

4. Thành thạo ít nhất một trong các backend framework: Django, Flask

5. Có kinh nghiệm về database (SQL / NoSQL/ GraphQL)

6. Có kiến thức cơ bản hoặc sử dụng: Git, REST API, Docker

7. Tiếng Anh tốt, đọc được paper, hiểu và giải thích lại được

Ngoài ra, các yếu tố sau là điểm cộng:

Có các kiến thức cơ bản về unit-test và integration-test

Có kinh nghiệm về multi-threading, multi-processing, Airflow, MLflow, Model Pruning và Model Compression

Đã từng tham gia đóng góp, contribute hoặc tự phát triển các bộ công cụ mã nguồn mở (OSS)

Đã từng thực hiện triển khai và quản lý version của mô hình lên hệ thống, cấu hình server.

**Quyền lợi**
Mức lương : VNĐ 8.500.000 – 10.500.000/tháng (Gross)

[https://www.topcv.vn/tim-viec-lam-machine-learning](https://www.topcv.vn/tim-viec-lam-machine-learning)

# Tổng kết

Bài viết khá ngắn, với mong muốn chỉ là tóm gọn các nội dung cơ bản của Machine Learning và ứng dụng tuyệt vời của nó hiện tại và tương lai của chúng ta. Rất mong sẽ còn được gặp lại các bạn trong những phần tiếp theo của series về machine learning, cám ơn.

-----
Tham khảo
- [Sự khác nhau giữa AI, ML, DL](https://www.linkedin.com/pulse/s%E1%BB%B1-kh%C3%A1c-nhau-gi%E1%BB%AFa-ai-ml-dl-hu%C3%A2n-b%C3%B9i-%C4%91%C3%ACnh)
- [Con đường trở thành Master Artificial Intelligence (AI)](https://viblo.asia/p/con-duong-tro-thanh-master-artificial-intelligence-ai-aWj53LooK6m)
- [Hiểu về trí tuệ nhân tạo chỉ với 5 phút cuộc đời](https://viblo.asia/p/hieu-ve-tri-tue-nhan-tao-chi-voi-5-phut-cuoc-doi-E375z4x1ZGW)
- [Làm thế nào để luôn cập nhật kiến thức trong lĩnh vực Machine Learning](https://viblo.asia/p/question-lam-the-nao-de-luon-cap-nhat-kien-thuc-trong-linh-vuc-machine-learning-maGK7mBxlj2)
- [[Deeplearning-1] Giải thích Machine Learning và Deep Learning bằng ngôn ngữ đại chúng](https://viblo.asia/p/deeplearning-1-giai-thich-machine-learning-va-deep-learning-bang-ngon-ngu-dai-chung-PAoJe5aAJ1j)
- [Hỡi các ML Learners, nhà tuyển dụng cần gì?](https://viblo.asia/p/hoi-cac-ml-learners-nha-tuyen-dung-can-gi-gGJ59ryxKX2)
- [[ML System Design] Tổng quan về Machine Learning System Design](https://viblo.asia/p/ml-system-design-tong-quan-ve-machine-learning-system-design-3P0lP8Lnlox)
- [Tóm tắt vài mô hình Text-To-Speech (p1) - Tacotron và Tacotron2](https://viblo.asia/p/tom-tat-vai-mo-hinh-text-to-speech-p1-tacotron-va-tacotron2-E375zApqlGW)
- [Tóm tắt vài mô hình Text-To-Speech (p2) - FastSpeech](https://viblo.asia/p/tom-tat-vai-mo-hinh-text-to-speech-p2-fastspeech-jvElaRVx5kw)
- [Tóm tắt vài mô hình Text-to-Speech (p3) - FastSpeech2](https://viblo.asia/p/tom-tat-vai-mo-hinh-text-to-speech-p3-fastspeech2-6J3ZgRvBKmB)
- [Tóm tắt vài mô hình Text-to-Speech (p4) - GlowTTS](https://viblo.asia/p/tom-tat-vai-mo-hinh-text-to-speech-p4-glowtts-Do754LBJ5M6)
- [Evaluating and Testing models - có vẻ phức tạp hơn bạn nghĩ](https://viblo.asia/p/evaluating-and-testing-models-co-ve-phuc-tap-hon-ban-nghi-vlZL9bRZVQK)
- [Sun* AI Research Team](https://sun-ai.viblo.asia)
- [Sun* AI Research Team](https://viblo.asia/o/sun-ai)
- [Viblo AI](https://ai.viblo.asia)

-----
Machine Learning
- [Học máy (machine learning) là gì? Ứng dụng và phân loại](https://lytuong.net/hoc-may-machine-learning-la-gi/)
- [Lộ Trình Học Machine Learning Python Cho Newbies](https://www.mcivietnam.com/blog-detail/lo-trinh-hoc-python-machine-learning-cho-newbies/)
- [Machine Learning - Tổng quan về Machine Learning](https://viblo.asia/p/machine-learning-tong-quan-ve-machine-learning-RQqKLxaOK7z)
- [Tất tần tật về Machine Learning và ứng dụng trong những ngành công nghiệp lớn](https://viblo.asia/p/tat-tan-tat-ve-machine-learning-va-ung-dung-trong-nhung-nganh-cong-nghiep-lon-gDVK2pOjlLj)
- [Ai cũng có thể hiểu được Machine Learning 🤖👶Phần 1: Tại sao Machine Learning lại được quan tâm hơn bao giờ hết](https://viblo.asia/p/ai-cung-co-the-hieu-duoc-machine-learning-phan-1-tai-sao-machine-learning-lai-duoc-quan-tam-hon-bao-gio-het-RQqKLArrZ7z)
- [20+ Resources To Learn and Start Your Career In Artificial Intelligence (AI)](https://viblo.asia/p/20-resources-to-learn-and-start-your-career-in-artificial-intelligence-ai-YWOZr23PZQ0)
- [Tự học Machine Learning với 4 khoá học online hoàn toàn miễn phí](https://viblo.asia/p/tu-hoc-machine-learning-voi-4-khoa-hoc-online-hoan-toan-mien-phi-1VgZvOw2lAw)
- [Cùng đi học Machine Learning - Phần 1 - Machine Learning là cái gì ?](https://viblo.asia/p/cung-di-hoc-machine-learning-phan-1-machine-learning-la-cai-gi-maGK78ExZj2)
- [Cùng đi học Machine Learning - Phần 2 - Machine Learning Algorithms](https://viblo.asia/p/cung-di-hoc-machine-learning-phan-2-machine-learning-algorithms-m68Z0OMdKkG)
- [10 sự thật thú vị về Machine Learning mà bạn nên biết](https://viblo.asia/p/10-su-that-thu-vi-ve-machine-learning-ma-ban-nen-biet-gGJ59e4a5X2)
- [Tìm niềm cảm hứng để bắt đầu học Deep Learning](https://viblo.asia/p/tim-niem-cam-hung-de-bat-dau-hoc-deep-learning-bWrZnPo95xw)
- [Bóc trần hệ thống gợi ý của Twitter - một cú lừa ngày cá tháng tư???](https://viblo.asia/p/boc-tran-he-thong-goi-y-cua-twitter-mot-cu-lua-ngay-ca-thang-tu-7ymJXx8qJkq)
- [[Paper Explain] Clustering trong Computer Vision: Hướng đi mới thay thế CNN và Transformer?](https://viblo.asia/p/paper-explain-clustering-trong-computer-vision-huong-di-moi-thay-the-cnn-va-transformer-0gdJz7pvLz5)
- [Machine Learning với Javascript](https://viblo.asia/p/machine-learning-voi-javascript-1VgZvwvmlAw)
- [Trả lời một số câu hỏi interview Machine Learning & Deep Learning](https://viblo.asia/p/tra-loi-mot-so-cau-hoi-interview-machine-learning-deep-learning-BQyJKmjWVMe)
- [Machine Learning & Deep Learning Interview Questions (P1)](https://viblo.asia/p/machine-learning-deep-learning-interview-questions-p1-63vKjOXbZ2R)

- [Machine Learning hoạt động như thế nào? Thần thoại và sự thật](https://viblo.asia/p/machine-learning-hoat-dong-nhu-the-nao-than-thoai-va-su-that-bJzKm76rl9N)
- [Fact vs. Fiction: How Does Machine Learning Actually Work?](https://www.expert.ai/blog/how-does-machine-learning-work/)
- [Soon We Won't Program Computers. We'll Train Them Like Dogs](https://www.wired.com/2016/05/the-end-of-code/)
- [IBM Watson | Full Q&A | Oxford Union](https://youtu.be/rXVoRyIGGhU)
- [Lộ Trình Tự Học Lập Trình PYTHON Cho Người Mới Bắt Đầu](https://youtu.be/O5AsvA9OGhM)
- [Khóa học lập trình Python miễn phí. Đăng ký, Download Free](https://chiasepremium.com/khoa-hoc-lap-trinh-python-mien-phi/)

Video
- [AI For Everyone - Andrew Ng](https://www.coursera.org/learn/ai-for-everyone)
- [Machine learning Vietsub - Andrew Ng](https://www.youtube.com/playlist?list=PLDpRz2wA0qZzTcDLeXP5PSCfmQ96l9-Qr)
- [Tự Học Data Science Cho Người Mới Bắt Đầu](https://www.youtube.com/playlist?list=PLJcWUrckOCKKwjjHALg6fnyQCHv8z92rs)
- [Supervised Machine Learning: Regression and Classification](https://www.coursera.org/learn/machine-learning)

Thực hành
- [Chihuahua or muffin? My search for the best computer vision API](https://www.freecodecamp.org/news/chihuahua-or-muffin-my-search-for-the-best-computer-vision-api-cbda4d6b425d/)
- [Dùng thử xem Machine Learning có gì ghê gớm](https://viblo.asia/p/dung-thu-xem-machine-learning-co-gi-ghe-gom-m68Z08jMZkG)
- ["Hello World" Machine Learning Project in Python Step-By-Step](https://viblo.asia/p/hello-world-machine-learning-project-in-python-step-by-step-RQqKLER6Z7z)

- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p1)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp1-eW65G8nxKDO)
    1. Why Is Python Best For AI?
    2. Demand for AI
    3. What Is Artificial Intelligence?
    4. Types Of Artificial Intelligence
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p2)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp2-eW65G89LKDO)
    1. Machine Learning Basics
    2. Types Of Machine Learning
    3. What Problems Can Machine Learning Solve?
    4. Machine Learning Process Steps
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p3)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp3-gDVK2mbA5Lj)
    1. Machine Learning With Python
    2.  Limitations Of Machine Learning
    3.  Why Deep Learning?
    4.  How Deep Learning Works?
    5.  What Is Deep Learning?
    6.  Deep Learning Use Case
    7.  What Is A Perceptron?
    8.  Multilayer Perceptrons
- [Hướng dẫn toàn diện về Trí tuệ nhân tạo với Python (Dịch.p4)](https://viblo.asia/p/huong-dan-toan-dien-ve-tri-tue-nhan-tao-voi-python-dichp4-Ljy5VyqVlra)
    1.  Deep Learning With Python
    2.  Introduction To Natural Language Processing (NLP)
    3.  Natural Language Processing Applications
    4.  Thuật ngữ trong xử lý ngôn ngữ tự nhiên
- [Artificial Intelligence With Python: A Comprehensive Guide](https://www.edureka.co/blog/artificial-intelligence-with-python/)