
# Python 

#### aiohttp library

aiohttp is a popular asynchronous HTTP client/server framework for Python. It allows you to make asynchronous HTTP requests and build asynchronous web applications. It is particularly useful in scenarios where you want to perform I/O-bound operations without blocking the execution of other tasks. Key features of aiohttp include:
- Asynchronous I/O: aiohttp is designed to work with Python's asyncio framework, allowing you to write asynchronous code that can efficiently handle multiple concurrent connections and I/O operations.
- Client-Side: On the client side, aiohttp provides an asynchronous HTTP client that allows you to make asynchronous HTTP requests to external APIs, websites, or other HTTP servers. This is especially useful for scenarios where you need to make multiple requests concurrently without blocking the program's execution.
- Server-Side: On the server side, aiohttp enables you to build asynchronous web applications using the aiohttp.web module. This allows you to handle incoming HTTP requests asynchronously, making it possible to handle a large number of concurrent connections efficiently.
- WebSocket Support: aiohttp also supports WebSockets, which are a communication protocol that enables two-way communication between the client and the server over a single, long-lived connection.
- Middleware and Routing: aiohttp provides features for adding middleware to the request processing pipeline and defining URL routing to handle different endpoints in your application.

Eg: In this example, the fetch_data coroutine asynchronously makes an HTTP request using aiohttp and then prints the response text. The main coroutine is run using asyncio.run() to initiate the asynchronous execution:

```
import aiohttp
import asyncio

async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    url = "https://example.com"
    data = await fetch_data(url)
    print(data)
if __name__ == "__main__":
    asyncio.run(main())

```

#### asyncio library

asyncio is a Python library that provides support for asynchronous programming, allowing you to write concurrent code that can efficiently handle multiple tasks without the need for explicit threading or multiprocessing. 

It's particularly useful for I/O-bound operations, such as networking or file I/O, where waiting for external resources can create bottlenecks. At its core, asyncio is built around the concept of coroutines, which are a form of lightweight, cooperative multitasking. 

When you use asyncio to call multiple API endpoints, you can perform non-blocking I/O operations. This means that when one API call is waiting for a response, your code can continue to execute other tasks, making efficient use of the event loop. Multiple API calls can be executed concurrently within a single event loop, and you can await their results as they complete.
asyncio is well-suited for I/O-bound operations, such as network requests and file I/O.

Few terms: 
- event loop (responsible for managing the execution of coroutines, scheduling tasks, and handling events)
- tasks (objects that represent the execution of a coroutine within the event loop. You can create tasks to run coroutines concurrently, and the event loop will manage their execution and Tasks can be created explicitly using asyncio.create_task())
- await keyword
- callbacks & futures (asyncio also provides a way to work with callbacks using Future - it represents a potential result of a coroutine, and you can attach callbacks to it that will be executed when the result is available)
- I/O operations (when a coroutine encounters an I/O operation like reading from a socket, it can await that operation without blocking the event loop, making the most efficient use of resources)
- Concurrency (managing many tasks efficiently) not parallelism (simultaneously executing tasks on multiple cores).

Example: In below code; Tasks 1 and 2 initiate API requests and await the responses concurrently. While Tasks 1 and 2 are waiting for their respective API responses, Task 3 starts its local processing. Once Tasks 1 and 2 receive their API responses, they continue and print the data. Task 3 completes its local processing after a 2-second delay. This demonstrates how different tasks can execute concurrently, and the event loop switches between them, making efficient use of time.

```
async def fetch_data(url, task_name):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            data = await response.text()
            print(f"{task_name} fetched data from {url}: {data}")

async def process_local_data(task_name):
    # Simulate some local processing or computation
    await asyncio.sleep(2)
    print(f"{task_name} completed local processing")

async def main():
    urls = [
        ("https://jsonplaceholder.typicode.com/posts/1", "Task 1"),
        ("https://jsonplaceholder.typicode.com/posts/2", "Task 2")
    ]
    # Create tasks for fetching data
    data_fetch_tasks = [fetch_data(url, task_name) for url, task_name in urls]
    # Create a task for local processing
    local_processing_task = process_local_data("Task 3")
    # Run all tasks concurrently
    await asyncio.gather(local_processing_task, *data_fetch_tasks)

if __name__ == "__main__":
    asyncio.run(main())
```

[asyncio history _vl](https://www.youtube.com/playlist?list=PLhNSoGM2ik6SIkVGXWBwerucXjgP1rHmB), 
[asyncio gather _al](https://www.educative.io/answers/what-is-asynciogather), 
[asyncio python _al](https://superfastpython.com/python-asyncio/)

- Note: 
  - If you don't use await in an async function in Python, the function will still be executed, but it won't pause the execution flow to wait for the result of the coroutine it calls. This can lead to unexpected behavior if you rely on the result of the coroutine or if you expect certain operations to be completed before proceeding.
  - aiohttp is faster than native asyncio (from gpt): Technical aspects of why aiohttp can be faster than using native asyncio directly for HTTP-related tasks:
    - Optimized Event Loop Integration: aiohttp integrates tightly with the asyncio event loop but adds additional optimizations tailored for HTTP traffic. This includes optimized handling of I/O events specifically for HTTP connections, reducing the overhead associated with generic event loop operations.
    - HTTP Parsing and Serialization: aiohttp utilizes efficient C-extensions for parsing and serializing HTTP messages. This low-level optimization ensures that the CPU cycles are minimized for these critical operations. The use of http_parser (a C library) allows for faster parsing compared to pure Python implementations.
    - Efficient Buffer Management: aiohttp implements advanced buffer management techniques to handle incoming and outgoing HTTP data. This includes strategies such as pooling buffers to reduce memory allocation overhead and using memoryviews to avoid unnecessary data copying.
    - Connection Pooling: aiohttp provides built-in connection pooling which allows for the reuse of TCP connections for multiple HTTP requests. This reduces the overhead of establishing new TCP connections, which involves several round trips and can be a significant bottleneck in high-throughput scenarios.
    - Custom I/O Handling: aiohttp has custom implementations for I/O operations, leveraging asyncio's transport and protocol abstractions but with optimizations for typical HTTP workloads. For example, it uses SelectorEventLoop efficiently to manage multiple socket connections concurrently.
    - Zero-Copy Sendfile Support: aiohttp can leverage the sendfile system call (where supported by the operating system), which allows for zero-copy file transfers directly from disk to network socket. This significantly reduces CPU usage and increases throughput for serving static files.
    - Concurrency Control: aiohttp includes mechanisms for controlling concurrency and limiting the number of simultaneous connections or requests, which helps prevent resource exhaustion and maintains performance under load. This is implemented through semaphore-based controls that are more sophisticated than basic asyncio primitives.
    - Protocol-Specific Optimizations: aiohttp optimizes the handling of specific HTTP features such as chunked transfer encoding, keep-alive connections, and HTTP/1.1 pipelining. These optimizations ensure that common patterns in HTTP communication are handled with minimal overhead.
    - Custom Executors for Blocking Operations: For operations that cannot be made non-blocking, aiohttp provides mechanisms to offload them to separate threads or processes using custom executors. This integration ensures that the main event loop remains responsive, which is crucial for handling high concurrency.
    - Memory Management: aiohttp implements various memory management techniques to minimize the footprint and avoid fragmentation. This includes efficient use of memory pools and careful management of object lifecycles to reduce garbage collection overhead.
  - By building on top of asyncio and adding these layers of optimizations and specialized handling, aiohttp is able to achieve higher performance for HTTP-related tasks than using asyncio directly. These enhancements allow aiohttp to handle a large number of concurrent HTTP requests more efficiently, making it a preferred choice for web applications and services that require high throughput and low latency.

#### concurrent.futures.ThreadPoolExecutor library

ThreadPoolExecutor is part of the concurrent.futures module and provides a way to run functions concurrently using threads.
When you use ThreadPoolExecutor, you create a pool of worker threads, and each task you submit is executed in a separate thread. This allows you to parallelize CPU-bound tasks.

Unlike asyncio, ThreadPoolExecutor does not inherently provide non-blocking I/O. When you make API calls using ThreadPoolExecutor, each call blocks the calling thread until it receives a response. This may lead to less efficient CPU usage in I/O-bound scenarios. ThreadPoolExecutor is well-suited for CPU-bound operations where you want to parallelize tasks that do not involve waiting for external resources.

In summary, asyncio is designed for asynchronous programming and excels at I/O-bound operations with non-blocking behavior, while ThreadPoolExecutor is more suitable for CPU-bound tasks where parallelism is needed but not necessarily non-blocking behavior. The choice between them depends on your specific use case and whether you need true asynchronous behavior or parallelism.

Example: In below code; fetch_data and process_local_data are functions that fetch data from URLs and perform local processing, respectively. In the main function, we create a list of URLs with their associated task names. We create a ThreadPoolExecutor with a maximum of 2 worker threads. We submit tasks to the executor using executor.submit(). We wait for all tasks to complete using future.result(). This code achieves concurrency using threads, where Tasks 1 and 2 fetch data concurrently, and Task 3 performs local processing. The ThreadPoolExecutor manages the thread pool for us.

```
def fetch_data(url, task_name):
    response = requests.get(url)
    data = response.text
    print(f"{task_name} fetched data from {url}: {data}")

def process_local_data(task_name):
    # Simulate some local processing or computation
    import time
    time.sleep(2)
    print(f"{task_name} completed local processing")

def main():
    urls = [
        ("https://jsonplaceholder.typicode.com/posts/1", "Task 1"),
        ("https://jsonplaceholder.typicode.com/posts/2", "Task 2")
    ]
    # Create a ThreadPoolExecutor with 2 threads
    with ThreadPoolExecutor(max_workers=2) as executor:
        # Submit tasks for fetching data
        data_fetch_tasks = [executor.submit(fetch_data, url, task_name) for url, task_name in urls]
        # Submit the local processing task
        local_processing_task = executor.submit(process_local_data, "Task 3")
        # Wait for all tasks to complete
        for future in data_fetch_tasks + [local_processing_task]:
            future.result()

if __name__ == "__main__":
    main()
```

Note: You can combine asyncio with ThreadPoolExecutor to achieve asynchronous programming with multi-threading for certain use cases. This can be particularly useful when you have both I/O-bound and CPU-bound tasks that need to run concurrently.

Example: 

```
async def io_bound_task():
    # Perform I/O-bound task (e.g., make HTTP requests)
    await asyncio.sleep(1)
    print("I/O-bound task completed")

def cpu_bound_task():
    # Perform CPU-bound task (e.g., heavy computation)
    import time
    time.sleep(1)
    print("CPU-bound task completed")

async def main():
    # Create a ThreadPoolExecutor with 2 threads
    with ThreadPoolExecutor(max_workers=2) as executor:
        # Submit CPU-bound tasks to the ThreadPoolExecutor
        cpu_tasks = [executor.submit(cpu_bound_task) for _ in range(2)]
        # Await asyncio tasks for I/O-bound operations
        await asyncio.gather(io_bound_task(), io_bound_task())

if __name__ == "__main__":
    asyncio.run(main())
```

#### Basic Data structures

- List [], Tuple (), Set {}, Dictionary {“”:””,“”:_,..}
- The list allows duplicate elements. Tuple allows duplicate elements. The Set will not allow duplicate elements. The dictionary doesn’t allow duplicate keys.

```
Example: [1, 2, 3, 4, 5]
Example: (1, 2, 3, 4, 5)
Example: {1, 2, 3, 4, 5}
Example: {1: “a”, 2: “b”, 3: “c”, 4: “d”, 5: “e”}
```

  - A list is mutable i.e we can make any changes in the list. And ordered. 
  - A tuple is immutable i.e we can not make any changes in the tuple. And ordered. 
  - A set is mutable i.e we can make any changes in the set, but elements are not duplicated. And unordered. 
  - A dictionary is mutable, but Keys are not duplicated. And ordered (Python 3.7x) 

#### Context Managers 

In any programming language, the usage of resources like file operations or database connections is very common. But these resources are limited in supply. Therefore, the main problem lies in making sure to release these resources after usage. If they are not released then it will lead to resource leakage and may cause the system to either slow down or crash. It would be very helpful if users have a mechanism for the automatic setup and teardown of resources. In Python, it can be achieved by the usage of context managers which facilitate the proper handling of resources. Managing resources properly is often a tricky problem. It requires both a setup phase and a teardown phase. The latter phase requires you to perform some cleanup actions, such as closing a file, releasing a lock, or closing a network connection. If you forget to perform these cleanup actions, then your application keeps the resource alive. This might compromise valuable system resources, such as memory and network bandwidth.

A context manager is an object that supports the context management protocol, which means it defines methods __enter__() and __exit__(). When you use a context manager with the with statement, it automatically calls __enter__() before entering the block and __exit__() after exiting the block. This allows you to perform setup and cleanup actions in a convenient and reliable way. The contextlib module provides utilities for working with context managers. The contextlib.contextmanager decorator allows you to define a generator function that serves as a context manager. This decorator simplifies the creation of context managers by handling the __enter__() and __exit__() methods for you. In summary, the with statement is used to invoke the context manager's __enter__() and __exit__() methods, while contextlib provides utilities, such as the contextmanager decorator, to create context managers more easily.

```
In this case: 
file = open("hello.txt", "w")
file.write("Hello, World!")
file.close()
```

This implementation doesn’t guarantee the file will be closed if an exception occurs during the .write() call. In this case, the code will never call .close(), and therefore your program might leak a file descriptor. In Python, you can use two general approaches to deal with resource management. You can wrap your code in: try … finally construct

The Python 'with' construct creates a runtime context that allows you to run a group of statements under the control of a context manager. It is the primary method used to call a context manager. Eg: with SomeContextManager as context_variable:`. 

A with statement does not create a scope (like if, for and while do not create a scope either). As a result, Python will analyze the code and see that you made an assignment in the with statement, and thus that will make the variable local (to the real scope). A with statement is only used for context management purposes. It forces (by syntax) that the context you open in the with is closed at the end of the indentation.

[Scope of with statement _al](https://stackoverflow.com/questions/45100271/scope-of-variable-within-with-statement?rq=1)
[Context manager python _al](https://realpython.com/python-with-statement/)
[enter exit functions _al](https://stackoverflow.com/questions/1984325/explaining-pythons-enter-and-exit ), 
[context manager python _al](https://www.pythonmorsels.com/what-is-a-context-manager/),
[python with statement _al](https://stackoverflow.com/questions/3012488/what-is-the-python-with-statement-designed-for)

#### Try catch block 
- Try: This block will test the excepted error to occur 
- Except:  Here you can handle the error 
- Else: If there is no exception then this block will be executed 
- Finally: Finally block always gets executed either exception is generated or not

#### Python Global Interpreter Lock

The GIL, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter. 

As a note: Before the interpreter takes over, Python performs three other steps: lexing, parsing, and compiling. Together, these steps transform the source code from lines of text into byte code containing instructions that the interpreter can understand. The interpreter's job is to take these code objects and follow the instructions. [How python interpretor works _al](https://stackoverflow.com/questions/70514761/how-does-python-interpreter-actually-interpret-a-program)

This means that only one thread can be in a state of execution at any point in time. The impact of the GIL isn’t visible to developers who execute single-threaded programs, but it can be a performance bottleneck in CPU-bound and multi-threaded code.

Problem which GIL solved: Python uses **reference counting** for memory management. It means that objects created in Python have a reference count variable that keeps track of the number of references that point to the object. When this count reaches zero, the memory occupied by the object is released. The problem was that this reference count variable needed protection from race conditions where two threads increase or decrease its value simultaneously. If this happens, it can cause either leaked memory that is never released or, even worse, incorrectly release the memory while a reference to that object still exists. This can cause crashes or other “weird” bugs in your Python programs. This reference count variable can be kept safe by adding locks to all data structures that are shared across threads so that they are not modified inconsistently. But adding a lock to each object or groups of objects means multiple locks will exist which can cause another problem—Deadlocks (deadlocks can only happen if there is more than one lock). Another side effect would be decreased performance caused by the repeated acquisition and release of locks. The GIL is a single lock on the interpreter itself which adds a rule that execution of any Python bytecode requires acquiring the interpreter lock. This prevents deadlocks (as there is only one lock) and doesn’t introduce much performance overhead. But it effectively makes any CPU-bound Python program single-threaded. The GIL, although used by interpreters for other languages like Ruby, is not the only solution to this problem. Some languages avoid the requirement of a GIL for thread-safe memory management by using approaches other than reference counting, such as garbage collection. On the other hand, this means that those languages often have to compensate for the loss of single threaded performance benefits of a GIL by adding other performance boosting features like JIT compilers.

Reason why GIL chosen: A lot of extensions were being written for the existing C libraries whose features were needed in Python. To prevent inconsistent changes, these C extensions required a thread-safe memory management which the GIL provided. The GIL is simple to implement and was easily added to Python. It provides a performance increase to single-threaded programs as only one lock needs to be managed. C libraries that were not thread-safe became easier to integrate. And these C extensions became one of the reasons why Python was readily adopted by different communities. As you can see, the GIL was a pragmatic solution to a difficult problem that the CPython developers faced early on in Python’s life.

Impact on multi thread python programs: When you look at a typical Python program—or any computer program for that matter—there’s a difference between those that are CPU-bound in their performance and those that are I/O-bound. CPU-bound programs are those that are pushing the CPU to its limit. This includes programs that do mathematical computations like matrix multiplications, searching, image processing, etc. I/O-bound programs are the ones that spend time waiting for Input/Output which can come from a user, file, database, network, etc. I/O-bound programs sometimes have to wait for a significant amount of time till they get what they need from the source due to the fact that the source may need to do its own processing before the input/output is ready, for example, a user thinking about what to enter into an input prompt or a database query running in its own process. Hence whether you run a program leveraging single thread or multi-thread, the runtime would be same. 

Why GIL not removed yet: The developers of Python receive a lot of complaints regarding this but a language as popular as Python cannot bring a change as significant as the removal of GIL without causing backward incompatibility issues. Removing the GIL would have made Python 3 slower in comparison to Python 2 in single-threaded performance and you can imagine what that would have resulted in. You can’t argue with the single-threaded performance benefits of the GIL. So the result is that Python 3 still has the GIL. But Python 3 did bring a major improvement to the existing GIL— We discussed the impact of GIL on “only CPU-bound” and “only I/O-bound” multi-threaded programs but what about the programs where some threads are I/O-bound and some are CPU-bound? In such programs, Python’s GIL was known to starve the I/O-bound threads by not giving them a chance to acquire the GIL from CPU-bound threads. This was because of a mechanism built into Python that forced threads to release the GIL after a fixed interval of continuous use and if nobody else acquired the GIL, the same thread could continue its use. The problem in this mechanism was that most of the time the CPU-bound thread would reacquire the GIL itself before other threads could acquire it. This was researched by David Beazley. This problem was fixed in Python 3.2 in 2009 by Antoine Pitrou who added a mechanism of looking at the number of GIL acquisition requests by other threads that got dropped and not allowing the current thread to reacquire GIL before other threads got a chance to run. 

How to deal: The most popular way is to use a multi-processing approach where you use multiple processes instead of threads. Each Python process gets its own Python interpreter and memory space so the GIL won’t be a problem. Python has a multiprocessing module which lets us create processes easily. [Python GIL _al](https://realpython.com/python-gil/)

Hence in short, 
- Pros: The GIL ensures thread safety in CPython by allowing only one running thread at a time to execute Python bytecode (thereby, no deadlock, race conditions, etc.)
- Cons: High intense CPU task threads are impacted as GIL allows only for single thread execution at any point of time. 
Multiple threads within a ThreadPool are subject to the global interpreter lock (GIL), whereas multiple child processes in the Pool are not subject to the GIL.

The GIL only affects threads within a single process. The multiprocessing module is in fact an alternative to threading that lets Python programs use multiple cores. [Python GIL _vl](https://www.youtube.com/watch?v=XVcRQ6T9RHo), [Does Py need GIL _vl](https://www.youtube.com/watch?v=EYgDP8cYlLo&ab_channel=CodePersist)

Note: Deepen your understanding on multi-threading in Python despite GIL either by hovering over to [Running multi-thread code in Pyspark in Spark README section _al](https://github.com/Surajv311/mDumpSWE/tree/main/Spark) or directly the [ref blog _al](https://superfastpython.com/threadpoolexecutor-vs-gil/).

#### Function annotations

Python is a dynamically typed language instead of a statically typed language. This means that instead of defining data types beforehand, they are determined at runtime based on the values variables contain. Annotations are merely added as information for the one reading the code. Python does not inherently implement checks on annotations. Eg: 

```
def addition(num1: int, num2: float) -> float:
    return num1 + num2

def testing():
    a: int = 78
    b: float = 34.5
    addition(a, b)

if __name__ == "__main__":
    testing()
```

[Annotations _al](https://www.educative.io/answers/how-annotations-are-used-in-python)

#### Asterisk Operator

In PySpark and Python, the * (asterisk) operator can have different meanings and uses, depending on the context. Here are some of the common usages:
- Unpacking/Spreading Operator: When used in function arguments or function calls, the * operator is used to unpack or spread the elements of an iterable (such as a list, tuple, or set) into individual arguments. For example:

```
def my_function(a, b, c):
    print(a, b, c)
my_list = [1, 2, 3]
my_function(*my_list)  # Output: 1 2 3
```

- Multiplication Operator: In mathematical expressions, the * operator is used for multiplication. For example: `c = a * b`
- Wildcard Import: In Python, the * operator can be used in an import statement to import all symbols (functions, classes, variables) from a module. This is known as a "wildcard import". For example: `from module_name import *`. However, using wildcard imports is generally discouraged as it can lead to name clashes and make the code harder to read and maintain.
- Repeated Sequence: In Python, the * operator can be used to repeat a sequence (such as a string or a list) a certain number of times. For example: `print('hello' * 3)  # Output: hellohellohello`
- Argument Lists: In function definitions, the * operator can be used to accept an arbitrary number of positional arguments. These arguments are then collected into a tuple. For example:

```
def my_function(*args):
    print(args)
my_function(1, 2, 3)  # Output: (1, 2, 3)
```

- Keyword Arguments: Similar to the usage in argument lists, the * operator can be used in function definitions to accept an arbitrary number of keyword arguments. These arguments are then collected into a dictionary. For example:
```
def my_function(**kwargs):
    print(kwargs)
my_function(a=1, b=2, c=3)  # Output: {'a': 1, 'b': 2, 'c': 3}
```

#### Classmethod and Staticmethod 

- In Python, classmethod and staticmethod are two types of methods that can be defined inside a class. They both have special behaviors and use cases compared to regular instance methods.
- @classmethod: A class method is a method that is bound to the class itself rather than to any specific instance of the class. It takes the class (cls) as its first parameter instead of the instance (self). You denote a class method using the @classmethod decorator. The primary use case for class methods is to define methods that operate on the class itself, rather than on instances of the class. These methods can be used as alternative constructors or to access or modify class-level attributes. Example:

```
class MyClass:
    class_attr = 0

    @classmethod
    def class_method(cls):
        return cls.class_attr

# Calling class method
print(MyClass.class_method())  # Output: 0
```

- @staticmethod: A static method is a method that doesn't depend on the instance or the class. It behaves like a regular function but belongs to the class's namespace. It does not take either the instance (self) or the class (cls) as its first parameter. You denote a static method using the @staticmethod decorator. Static methods are typically used when a method does not need to access or modify any instance or class attributes. They are often used for utility functions that logically belong to the class but do not require access to any instance or class variables. Example:

```
class MyClass:
    @staticmethod
    def static_method(x, y):
        return x + y

# Calling static method
print(MyClass.static_method(3, 4))  # Output: 7
```

- In summary: Use @classmethod when you want a method to operate on the class itself and have access to class-level attributes.
Use @staticmethod when you want a method that does not depend on instance or class state and behaves like a regular function but belongs to the class's namespace.

#### Otherspython 

- Use Pytest to test Python unit tests code: https://docs.pytest.org/en/7.1.x/how-to/usage.html
- What does __name__ == "__main__" do?: It allows you to execute code when the file runs as a script. In other words, remember in C++ code we had main() function, when we ran the file, the default function used to execute. Similar analogy. [init main info _al](https://stackoverflow.com/questions/419163/what-does-if-name-main-do)
- [Python logging causing latencies? _al](https://stackoverflow.com/questions/24791395/python-logging-causing-latencies)
- Inner functions: A function which is defined inside another function is known as inner function or nested function. Nested functions are able to access variables of the enclosing scope. Inner functions are used so that they can be protected from everything happening outside the function. [Inner functions _al](https://www.geeksforgeeks.org/python-inner-functions/)
- init function, self object, constructor: Self represents the instance of the class. By using the **self**  we can access the attributes and methods of the class in Python. **Constructors** are used to initializing the object’s state. The task of constructors is to initialize(assign values) to the data members of the class when an object of the class is created. The Default **__init__** Constructor used in Python. [Python init tutorial _vl](https://www.youtube.com/watch?v=WIP3-woodlU&ab_channel=Telusko)

```
class mynumber:
  def __init__(self, value):
    self.value = value
  def print_value(self):
    print(self.value)
    obj1 = mynumber(17)
    obj1.print_value()
```

- `getattr() function`: The getattr() function is used to access the attribute value of an object and also gives an option of executing the default value in case of unavailability of the key. [getattr in py _al](https://www.geeksforgeeks.org/python-getattr-method/)
- `isinstance() function`: The isinstance() function returns True if the specified object is of the specified type, otherwise False. If the type parameter is a tuple, this function will return True if the object is one of the types in the tuple. Eg: isinstance(object, type)
- `*args` and `**kwargs` are special keyword which allows function to take variable length argument. 
  - `*args` passes variable number of non-keyworded arguments and on which operation of the tuple can be performed.

```
def adder(*num):
    sum = 0
    for n in num:
        sum = sum + n
    print("Sum:",sum)

adder(3,5)
adder(4,5,6,7)
adder(1,2,3,5,6)
```

  - `**kwargs` passes variable number of keyword arguments dictionary to function on which operation of a dictionary can be performed.

```
def intro(**data):
    print("\nData type of argument:",type(data))
    for key, value in data.items():
        print("{} is {}".format(key,value))

intro(Firstname="Sita", Lastname="Sharma", Age=22, Phone=1234567890)
intro(Firstname="John", Lastname="Wood", Email="johnwood@nomail.com", Country="Wakanda", Age=25, Phone=9876543210)
```

- StringIO Module in Python is an in-memory file-like object. This object can be used as input or output to the most function that would expect a standard file object. Eg: 

```
from io import StringIO  

string ='Hello and welcome to GeeksForGeeks.'
 
# Using the StringIO method to set as file object.
file = StringIO(string) 
 
# Retrieve the entire content of the file.
print(file.getvalue())
```

[stringio python _al](https://www.geeksforgeeks.org/stringio-module-in-python/)

- Positional arguments and keyword arguments to functions python: 

```
rectangle_area(1, 2) # positional arguments
rectangle_area(width=2, height=1) # keyword arguments
```

- Single quotes vs double quotes in Python - There is no difference. 
- [Integer cache maintained by Python interpretor _al](https://stackoverflow.com/questions/15171695/whats-with-the-integer-cache-maintained-by-the-interpreter)

```
Consider running in python shell: 

>>> a = 1
>>> b = 1
>>> a is b
True
>>> a = 257
>>> b = 257
>>> a is b
False

But if it is run in a py file (or joined with semi-colons), the result is different:
>>> a = 257; b = 257; a is b
True

Why so?
Python caches integers in the range [-5, 256], so integers in that range are usually but not always identical. What you see for 257 is the Python compiler optimizing identical literals when compiled in the same code object. When typing in the Python shell each line is a completely different statement, parsed and compiled separately, but if its in a file - the behaviour is different. 
```

- `'wb'` in Python code: The wb indicates that the file is opened for writing in binary mode. When writing in binary mode, Python makes no changes to data as it is written to the file. In text mode (when the b is excluded as in just w or when you specify text mode with wt), however, Python will encode the text based on the default text encoding. Additionally, Python will convert line endings (\n) to whatever the platform-specific line ending is, which would corrupt a binary file like an exe or png file. Text mode should therefore be used when writing text files (whether using plain text or a text-based format like CSV), while binary mode must be used when writing non-text files like images. [wb in python _al](https://stackoverflow.com/questions/2665866/what-does-wb-mean-in-this-code-using-python)

- Try catch except finally block: 
  - The try block lets you test a block of code for errors.
  - The except block lets you handle the error. - Its like catch block
  - The else block lets you execute code when there is no error.
  - The finally block lets you execute code, regardless of the result of the try- and except blocks.

- Scope of variable in if/while in Python: Python variables are scoped to the innermost function, class, or module in which they're assigned. Control blocks like `if` and `while` blocks don't count, so a variable assigned inside an if is still scoped to a function, class, or module.

- Why is __init__() always called after __new__() in Py?:
  - Use __new__ when you need to control the creation of a new instance.
  - Use __init__ when you need to control initialization of a new instance.
  - __new__ is the first step of instance creation. It's called first, and is responsible for returning a new instance of your class.
  - In contrast, __init__ doesn't return anything; it's only responsible for initializing the instance after it's been created.
  - [__init__, __new__ _al](https://stackoverflow.com/questions/674304/why-is-init-always-called-after-new)
- In the String module, Template Class allows us to create simplified syntax for output specification. The format uses placeholder names formed by $ with valid Python identifiers (alphanumeric characters and underscores).
  - Eg: `t = Template('x is $x'), then say t.substitute({'x' : 1})`
- pyproject.toml is the specified file format of PEP 518 which contains the build system requirements of Python projects. This solves the build-tool dependency chicken and egg problem, i.e. pip can read pyproject.toml and what version of setuptools or wheel one may need.

----------------------------------------------------------------------





















