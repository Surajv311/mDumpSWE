
# ASGI_vs_WSGI 

- A Web Server is a server capable of receiving HTTP requests, interpreting them, processing the corresponding HTTP Responses and sending them to the appropriate clients (Web Browsers). Example: Apache Web Server.
  - WSGI (Web Server Gateway Interface):
   - WSGI is a specification for how web servers communicate with Python web applications or frameworks. 
   - In WSGI, the web server receives an HTTP request from a client (like a web browser) and forwards it to a WSGI application. 
   - The WSGI application is a Python callable (such as a function or object) that processes the request and returns an HTTP response.
   - WSGI applications typically follow a synchronous execution model, meaning they handle one request at a time and block until the request is completed. 
   - Most traditional Python web frameworks, like Flask and Django, are built on top of WSGI.
  - ASGI (Asynchronous Server Gateway Interface):
    - ASGI is an evolution of WSGI designed to support asynchronous and real-time web applications.
    - ASGI provides a more flexible protocol that can handle both synchronous and asynchronous processing of HTTP requests.
    - In ASGI, the web server receives an HTTP request and forwards it to an ASGI application, which can be either synchronous or asynchronous.
    - ASGI applications can handle multiple requests concurrently and are well-suited for long-lived connections, such as WebSockets and server-sent events.
    - ASGI servers support asynchronous frameworks like Quart, FastAPI, and Starlette, as well as traditional synchronous frameworks with ASGI adapters.
  - In technical terms, WSGI and ASGI are specifications that define how Python web applications interact with web servers. WSGI follows a synchronous execution model, while ASGI supports both synchronous and asynchronous processing of HTTP requests, making it more versatile for modern web applications. ASGI enables real-time communication and better scalability, especially for applications with high concurrency or long-lived connections.
  - Is wsgi a load balancer then?:  No, WSGI is not a load balancer. WSGI (Web Server Gateway Interface) is a specification for how web servers communicate with Python web applications or frameworks. It defines the protocol for handling HTTP requests and responses between the web server and the Python application. A load balancer, on the other hand, is a separate component of a network infrastructure that distributes incoming network traffic across multiple servers. Its purpose is to improve the performance, reliability, and scalability of web applications by evenly distributing the workload among multiple servers. While WSGI defines how a Python web application interacts with a web server, a load balancer sits in front of multiple servers and routes incoming requests to the appropriate server based on various criteria, such as server availability, response time, or server load. In a typical web application deployment, a load balancer would sit in front of multiple web servers running WSGI-compliant applications. The load balancer distributes incoming requests across these servers to ensure efficient utilization of resources and high availability of the application. Each web server then communicates with the Python application through the WSGI interface.  

[cgi _al](https://en.wikipedia.org/wiki/Common_Gateway_Interface), [webservers _al](https://docs.python.org/2/howto/webservers.html)

----------------------------------------------------------------------





















