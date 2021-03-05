---
title: "The HTTP/2 Optimization Revolution"
date: "2020-08-20"
categories: 
  - "optimization"
  - "tech"
tags: 
  - "compressing"
  - "development"
  - "front-end"
  - "http2"
  - "minify"
  - "ssl"
  - "tls"
---

HTTP/2 is the second iteration of HTTP (Hypertext Transfer Protocol), which it is also backwards-compatible with. The changes introduced in HTTP/2 affects how developers optimize websites and servers for speed and efficiency. Beyond shrinking and compressing images, minimizing page and script file sizes, you can also switch to HTTP/2.

Switching to HTTP/2 allows you to benefit from the immediate performance that you can gain from it, and because it is backwards compatible with HTTP/1. In order to optimize page-loading performance in HTTP/1, you would concatenate assets together into one large file because each additional HTTP request would add latency and thus make the page load slower. In HTTP/2, this may no longer be the best practice.

HTTP/2 has a huge impact on front end performance. It can provide up to a 2x increase in site load time! This speed increase is attributed to a couple of new features that are available in HTTP/2.

The first is that HTTP/2 encodes HTTP requests and responses in binary instead of plaintext. Binary is less error-prone and it is more efficient to parse. Secondly, HTTP/2 can send multiple resources over a single TCP connection. Previously, browsers could open multiple TCP connections through domain sharing, which could potentially congest network traffic. In HTTP/2, multiplexing allows your browser to fire multiple requests at once on the same TCP connection and asynchronously receive responses. Another feature is stream prioritization, which gives us the ability to tell a server to allocate resources and bandwidth to prioritized data streams, ensuring optimal delivery of high priority content to clients. Furthermore,

What does this mean for developers? First, you'll no longer have to concatenate assets. This old optimization technique of reducing the number of HTTP requests is no longer necessary since HTTP/2 uses multiplexing! Now, you can download multiple resources on a single TCP connection! Similarly, you no longer have to split web page resources over multiple domains to maximize the number of concurrent TCP requests over HTTP/1. This is no longer necessary because HTTP/2 now has multiplexing. Furthermore, you can stop inlining assets. The assumption with HTTP/1 is that embedding CSS and JS files in your HTML document will improve page loading speed because it will reduce file numbers and server requests. In HTTP/2, this will reduce your page speed optimization from caching and break any improvement from stream optimization since all embedded script and content will get the same priority level as your HTML content.
