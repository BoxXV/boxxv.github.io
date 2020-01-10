---
layout: post
title: 8 ways to Stream IP Camera to web browser
image: /img/hello_world.jpeg
tags:
- Embedded
- IoT
- Raspberry Pi
- HTML5
---
## There are three streaming protocols / technology in HTML5
- Live streaming, `low latency` - **WebRTC** - **Websocket**
- VOD and Live streaming, `high latency` - **HLS**

### 1. WebRTC
In fact WebRTC is SRTP(secure RTP protocol). Thus we can say that video tag supports RTP(SRTP) indirectly via WebRTC.

Therefore to get RTP stream on your Chrome, Firefox or another HTML5 browser, you need a WebRTC server which will deliver the SRTP stream to browser.

### 2. Websocket
It is TCP based, but with lower latency than HLS. Again you need a Websocket server.


### 3. HLS
Most popular high-latency streaming protocol for VOD(pre-recorded video).


-----
## 8 ways to Stream IP Camera to web browser
### 1. Method 1 – RTMP
Các trình duyệt không hỗ trợ giao thức RTMP, nhưng đoán xem ai làm gì? Flash Player trung thành cũ hoạt động đủ tốt mặc dù nó không hỗ trợ tất cả các trình duyệt, vì vậy nó có thể hiển thị luồng video.

### 2. Method 2 – RTMP wrapped to HTML5
### 3. Method 3 – RTMFP
### 4. Method 4 – RTMFP wrapped to HTML5
### 5. Method 5 – WebRTC
### 6. Method 6 – Websockets
### 7. Method 7 – HLS
### 8. Method 8 – Android application, WebRTC
### 9. 
### 10. 


HLS Streaming of RTSP Stream by Nginx and Apache Tomcat  
https://dzone.com/articles/hls-streaming-by-nginx-and-apche-tomcat  

How to Use the NGINX RTMP Module to Setup a Streaming Server  
https://www.servermania.com/kb/articles/nginx-rtmp/  

Serversetup a NGINX Server with the RTMP Module on Windows  
https://github.com/illuspas/nginx-rtmp-win32  
https://github.com/luowei/nginx-rtmp-sample  
https://github.com/search?q=nginx-rtmp  

http://nginx-rtmp.blogspot.com/2013/06/windows-support-in-101.html