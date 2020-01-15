---
layout: post
title: 8 ways to Stream IP Camera to web browser
image: "img/hello_world.jpeg"
tags:
- Embedded
- IoT
- Raspberry Pi
- HTML5
---

## There're three streaming protocols/technology in HTML5
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
It is hard to find those willing to keep coding on Action Script 3 these days. So, there is a method with an HTML wrapping that allows controlling the RTMP player from JavaScript. In this variant the flash is loaded to the HTML page only to display picture and play sound.

### 3. Method 3 – RTMFP
The RTMFP protocol also works inside the Flash Player. The difference from RTMP is that RTMFP works on top of the UDP, so it is much more suitable for low latency broadcasting.

### 4. Method 4 – RTMFP wrapped to HTML5
This way is identical to method 2 except that during initialization we set the RTMFP protocol for the underlying Flash (swf object).

### 5. Method 5 – WebRTC
In this case we do not use Flash at all, and the video stream is played using means of the browser itself, without using third-party plugins. This method works both in Chrome and Firefox Android browsers, where Flash is not available. WebRTC results in the lowest latency, less than 0.5 seconds.

### 6. Method 6 – Websockets
WebRTC and Flash do not cover all browsers and platforms. For instance, the iOS Safari browser does not support them.

### 7. Method 7 – HLS
When RTSP is converted to HLS, a video stream is divided to segments that are happily downloaded from the server and displayed in the HLS player.

### 8. Method 8 – Android application, WebRTC
The application retrieves the stream from the server via WebRTC. To goal of the server here is to convert RTSP to WebRTC and feed the result to the mobile application.

### 9. Method 9 – iOS application, WebRTC
Just like its Android brethren, the iOS application fetches a video stream from the server via WebRTC.


-----
HLS Streaming of RTSP Stream by Nginx and Apache Tomcat  
https://dzone.com/articles/hls-streaming-by-nginx-and-apche-tomcat  

How to Use the NGINX RTMP Module to Setup a Streaming Server  
https://www.servermania.com/kb/articles/nginx-rtmp/  

Serversetup a NGINX Server with the RTMP Module on Windows  
https://github.com/illuspas/nginx-rtmp-win32  
https://github.com/luowei/nginx-rtmp-sample  
https://github.com/search?q=nginx-rtmp  

http://nginx-rtmp.blogspot.com/2013/06/windows-support-in-101.html