
# HTTP Request - HTTP 1 & 2 

HTTP is a method for encoding and transporting data between a client and a server. It is a request/response protocol: clients issue requests and servers issue responses with relevant content and completion status info about the request. HTTP is self-contained, allowing requests and responses to flow through many intermediate routers and servers that perform load balancing, caching, encryption, and compression.

HTTP is an application layer protocol relying on lower-level protocols such as TCP and UDP.

In general, an HTTP request is divided into 3 parts: 
- A request line: We place the HTTP method to be used, the URI of the request and the HTTP protocol to be used. HTTP methods indicate what kind of action our client wants to perform, whether he wants to read a resource, or if he wants to send information to the API, etc. The URI refers to the address where the resource is located. And the HTTP protocol refers to which HTTP protocol will be used, this is because there are several versions of the HTTP protocol, at the time of writing this post, the most common protocol is HTTP/1.1, however, there are other more recent revisions , like the HTTP/2.0 revision. Eg: `GET /api/authors HTTP/1.1` - means we are requesting a resource from endpoint. 
- A set of header fields: Headers are metadata that are sent in the request to provide information about the request. Each header is specified with a name, then two points, and then followed by the value of that header. Eg: `Host: en.wikipedia.org`, or `Cache-Control: no-cache`. The Host and Cache-Control headers are standard headers, which already have a well-defined purpose. However, we are free to use our own custom headers.  
- A body, which is optional: The Request Body is where we put additional information that we are going to send to the server. In the body of the request we are free to place virtually whatever we want. From the username and password of a person trying to login to our system, to the answers of a complex form of a survey. The body is quite important, because it represents, in many cases, the content per se that one wants to transmit. We note that GET requests do not use a body, because one does not tend to send many complex data when reading information. In the case of the POST method, we usually use the body of the request to place what we want to send. Eg: `Hello`

Clubbing all examples: 

```
HTTP Request: GET /api/autores HTTP/1.1
Headers: 
Host: en.wikipedia.org
Cache-Control: no-cache
Example of Request body for POST request: 
{
    "Name": "Test",
    "Age": 123
}
```

[Anatomy of HTTP request _al](https://gavilan.blog/2019/01/03/anatomy-of-an-http-request/)

When the client sends us an HTTP request, server responds with an HTTP response. The HTTP response also has its own structure, which is quite similar to the structure of the request. These parts are: `Status line`, `Header`, `Body (optional)`. Eg:

``` 
HTTP/1.1 200 OK
Date: Thu, 29 Mar 2024 19:43:07 IST
Server: gws
Accept-Ranges: bytes
Content-Length: 68894
Content-Type: text/html; charset=UTF-8
<!doctype html><html …
```

- HTTP stands for hypertext transfer protocol, and it is the basis for almost all web applications. More specifically, HTTP is the method computers and servers use to request and send information. For instance, when someone navigates to cloudflare.com on their laptop, their web browser sends an HTTP request to the Cloudflare servers for the content that appears on the page. Then, Cloudflare servers send HTTP responses with the text, images, and formatting that the browser displays to the user.
- The first usable version of HTTP was created in 1997. Because it went through several stages of development, this first version of HTTP was called HTTP/1.1. This version is still in use on the web. In 2015, a new version of HTTP called HTTP/2 was created. In particular, HTTP/2 is much faster and more efficient than HTTP/1.1. One of the ways in which HTTP/2 is faster is in how it prioritizes content during the loading process.
- In the context of web performance, prioritization refers to the order in which pieces of content are loaded. Suppose a user visits a news website and navigates to an article. Should the photo at the top of the article load first? Should the text of the article load first? Should the banner ads load first? Prioritization affects a webpage's load time. For example, certain resources, like large JavaScript files, may block the rest of the page from loading if they have to load first. More of the page can load at once if these render-blocking resources load last. In HTTP/2, developers have hands-on, detailed control over prioritization. This allows them to maximize perceived and actual page load speed to a degree that was not possible in HTTP/1.1. HTTP/2 offers a feature called weighted prioritization. This allows developers to decide which page resources will load first, every time. In HTTP/2, when a client makes a request for a webpage, the server sends several streams of data to the client at once, instead of sending one thing after another. This method of data delivery is known as multiplexing. Developers can assign each of these data streams a different weighted value, and the value tells the client which data stream to render first.
- Other differences: 
  - Multiplexing: HTTP/1.1 loads resources one after the other, so if one resource cannot be loaded, it blocks all the other resources behind it. In contrast, HTTP/2 is able to use a single TCP connection to send multiple streams of data at once so that no one resource blocks any other resource. HTTP/2 does this by splitting data into binary-code messages and numbering these messages so that the client knows which stream each binary message belongs to.
  - Server push: Typically, a server only serves content to a client device if the client asks for it. However, this approach is not always practical for modern webpages, which often involve several dozen separate resources that the client must request. HTTP/2 solves this problem by allowing a server to "push" content to a client before the client asks for it. The server also sends a message letting the client know what pushed content to expect - eg: Table of contents.
  - Header compression: Small files load more quickly than large ones. To speed up web performance, both HTTP/1.1 and HTTP/2 compress HTTP messages to make them smaller. However, HTTP/2 uses a more advanced compression method called **HPACK** that eliminates redundant information in HTTP header packets. This eliminates a few bytes from every HTTP packet. Given the volume of HTTP packets involved in loading even a single webpage, those bytes add up quickly, resulting in faster loading.
- HTTP/3 is the next proposed version of the HTTP protocol. HTTP/3 does not have wide adoption on the web yet, but it is growing in usage. The key difference between HTTP/3 and previous versions of the protocol is that HTTP/3 runs over QUIC instead of TCP. QUIC is a faster and more secure transport layer protocol that is designed for the needs of the modern Internet.
[http 1.1 and 2.0 _al](https://www.cloudflare.com/en-gb/learning/performance/http2-vs-http1.1/)

- RFC 2616 is basically HTTP 1.1 protocol. 

----------------------------------------------------------------------





















