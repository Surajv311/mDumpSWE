
# FastApi_Celery 

- FastApi
  - FastAPI is a modern, fast (high-performance), web framework for building APIs with Python based on standard Python type hints.
  - FastAPI applications use Uvicorn because it's an ASGI server that enables asynchronous processing, which is essential for FastAPI's high performance. 
  - When an API request is made from a browser to a FastAPI application, it passes through several layers: 
    - Browser makes an HTTP request (e.g., clicking a button, form submission, AJAX call)
    - DNS Resolution translates domain name to IP address
    - Network Infrastructure (routers, switches, load balancers) routes the request to server
    - Web Server (Nginx/Apache) receives the initial HTTP request
      - Handles SSL termination
      - May perform initial authentication/authorization
      - Often serves static files directly
      - Acts as a reverse proxy for dynamic content
    - Process Manager / WSGI/ASGI Server (Gunicorn)
      - Master process receives the proxied request
      - Delegates to one of its worker processes
    - Worker Process (Uvicorn worker inside Gunicorn)
      - Converts HTTP to ASGI event format
      - Manages the asynchronous event loop
    - ASGI Application (FastAPI)
      - Middleware processes request
      - Router matches URL to endpoint
      - Dependency injection runs 
      - Request validation occurs
      - Endpoint handler executes business logic
      - Response is generated and serialized
    - The response travels back through the same layers in reverse
  - WSGI was the original standard interface between web servers and Python web applications. It was designed to solve a major problem: before WSGI, each Python web framework required its own custom server implementation. WSGI's key limitation is that it's synchronous - each request must fully complete before the next one can be processed, which becomes inefficient for I/O-bound operations.
  - ASGI evolved from WSGI to solve the synchronous limitation by: Supporting asynchronous request handling, Enabling WebSockets and other protocols beyond HTTP, Allowing long-lived connections, Supporting concurrent request processing.
  - FastAPI uses Uvicorn as it is a lightning-fast ASGI server implementation. 
  - Uvicorn/Gunicorn workers: 
    - Uvicorn Architecture: 
      - Single Process Model: By default, Uvicorn runs as a single process with a single thread that manages an event loop
      - Event Loop: Uses uvloop (a fast drop-in replacement for asyncio) to handle concurrent connections
      - HTTP Protocol Server: Implements HTTP/1.1 and HTTP/2 protocols
      - Lifespan Protocol: Manages application startup/shutdown events
      - Uvicorn alone doesn't have a built-in worker model - it's a single-process server that leverages async I/O for concurrency, not multiple processes.
    - Gunicorn Architecture:
      - Gunicorn (often paired with Uvicorn) provides the multi-process architecture. 
      - Master Process: Coordinates and manages worker processes
      - Worker Processes: Handle actual requests (when using with FastAPI, these are typically Uvicorn workers)
      - Worker Class: Determines how each worker handles connections (sync, async, etc.)
    - When you increase the number of workers in a Gunicorn/Uvicorn setup for your FastAPI application:
    - Positive Effects:
      - Increased CPU Utilization: Each worker can utilize a separate CPU core, increasing overall throughput for CPU-bound tasks
      - Higher Concurrent Request Handling: More workers can handle more simultaneous requests
      - Fault Isolation: If one worker crashes, others can continue serving requests
      - Minimized Impact of Blocking Operations: If one worker gets blocked, others can still process requests
    - Potential Drawbacks:
      - Increased Memory Usage: Each worker is a separate process with its own memory space, increasing the overall memory footprint
      - Connection Pool Contention: Workers might compete for database connections if not properly configured
      - Shared State Complexity: Data that needs to be shared between workers must be stored externally (Redis, database, etc.)
      - Diminishing Returns: Adding workers beyond the number of available CPU cores generally doesn't improve performance
    - Here's how you'd typically run a FastAPI application with Gunicorn and Uvicorn workers: `gunicorn main:app --workers 4 --worker-class uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000`
    - Each worker is an independent Uvicorn process with its own event loop, managing its set of client connections and running the FastAPI application.
    - 

- Celery 
  - Celery is a robust, distributed task queue written in Python that enables developers to execute tasks outside the main application flow.
  - Celery is an open-source task queue system that allows you to execute work outside the Python web application’s HTTP request-response cycle. A task queue’s input is a unit of work called a task. Dedicated worker processes constantly monitor task queues for new work to perform.
  - Architecture on a top level: 
    - Task Queue: Celery implements a distributed task queue to handle work outside the request-response cycle
    - Workers: Separate processes that consume tasks from queues and execute them asynchronously
    - Broker: Message system (like RabbitMQ, Redis) that passes tasks from applications to workers
    - Backend: Optional storage system to track results and task states
  - [All about Celery _al](https://priyanshuguptaofficial.medium.com/everything-about-celery-b932c4c533af)








---------------------------