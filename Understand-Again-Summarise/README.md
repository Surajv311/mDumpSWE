
# Understand-Again-Summarise

Misc:

Spark domain: 
https://stackoverflow.com/questions/77266953/number-of-files-generated-by-spark
https://www.reddit.com/r/dataengineering/comments/te0m0x/pandas_on_spark_vs_pyspark_dataframe/
https://medium.com/analytics-vidhya/horizontal-parallelism-with-pyspark-d05390aa1df5: 
As soon as we call with the function multiple tasks will be submitted in parallel to spark executor from pyspark-driver at the same time and spark executor will execute the tasks in parallel provided we have enough cores
Note this will work only if we have required executor cores to execute the parallel task
For example if we have 100 executors cores(num executors=50 and cores=2 will be equal to 50*2) and we have 50 partitions on using this method will reduce the time approximately by 1/2 if we have threadpool of 2 processes. But on the other hand if we specified a threadpool of 3 we will have the same performance because we will have only 100 executors so at the same time only 2 tasks can run even though three tasks have been submitted from the driver to executor only 2 process will run and the third task will be picked by executor only upon completion of the two tasks.
https://stackoverflow.com/questions/58235076/what-is-the-difference-between-predicate-pushdown-and-projection-pushdown

https://superfastpython.com/threadpoolexecutor-vs-gil/: 
The presence of the GIL in Python impacts the ThreadPoolExecutor.
The ThreadPoolExecutor maintains a fixed-sized pool of worker threads that supports concurrent tasks, but the presence of the GIL means that most tasks will not run in parallel.
You may recall that concurrency is a general term that suggests an order independence between tasks, e.g. they can be completed at any time or at the same time. Parallel might be considered a subset of concurrency and explicitly suggests that tasks are executed simultaneously.
The GIL means that worker threads cannot run in parallel, in most cases.
Specifically, in cases where the target task functions are CPU-bound tasks. These are tasks that are limited by the speed of the CPU in the system, such as working no data in memory or calculating something.
Nevertheless, worker threads can run in parallel in some special circumstances, one of which is when an IO task is being performed.
These are tasks that involve reading or writing from an external resource.
Examples include: Reading or writing a file from the hard drive; Reading or writing to standard output, input, or error (stdin, stdout, stderr); Printing a document; Downloading or uploading a file; Querying a server; Querying a database; Taking a photo or recording a video; And so much more.
When a Python thread executes a blocking IO task, it will release the GIL and allow another Python thread to execute.
This still means that only one Python thread can execute Python bytecodes at any one time. But it also means that we will achieve seemingly parallel execution of tasks if tasks perform blocking IO operations.


Threads vs Processes: 
Traditionally (e.g. in the 1980s), processes in many OS's were only allowed to have exactly one thread, but as OS's become more sophisticated, that restriction was relaxed.
A process is a sort of container that holds multiple threads. 2 processes cannot run on a single core. Context switching between processes is heavy.
It has a concept of IPC (Inter Process Communication) which is an overhead. 
Similarly, 1 thread per core gives most optimal performance, else it would also context switch though switch in threads is lighter. 
Both processes and threads are independent sequences of execution. The typical difference is that threads (of the same process) run in a shared memory space (since it's part/unit within a process), while processes run in separate memory spaces.
A process can have anywhere from one thread to many - Linux doesn't have a separate threads per process limit. 
In general, linux: number of threads = total virtual memory / (stack size*1024*1024)
But you can alter the default threads limit of a process.
For CPU-bound tasks - Multiprocessing useful, for I/O-bound tasks Multithreading useful. 
The GIL simplifies thread management and protects against race conditions and memory corruption in Python. The threading module uses threads, the multiprocessing module uses processes. The difference is that threads run in the same memory space, while processes have separate memory. This makes it a bit harder to share objects between processes with multiprocessing. Since threads use the same memory, precautions have to be taken or two threads will write to the same memory at the same time. This is what the global interpreter lock is for. The GIL in cPython does not protect your program state. It protects the interpreter's state.
(gpt): The OS has a scheduler that manages process and thread execution. 
- Processes: The OS can schedule different processes on different CPU cores. For example, if you have a quad-core CPU, four different processes can run simultaneously on each core.
- Threads: The OS can also schedule different threads of the same process on different CPU cores, but due to the GIL in Python, only one thread per process can execute Python code at a time.
(Ignore below links as content from then is summarized above)
https://stackoverflow.com/questions/1713554/threads-processes-vs-multithreading-multi-core-multiprocessor-how-they-are
https://stackoverflow.com/questions/76608946/does-a-process-or-thread-run-on-a-core
https://stackoverflow.com/questions/8916723/can-two-processes-simultaneously-run-on-one-cpu-core
https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread
https://www.baeldung.com/linux/max-threads-per-process
https://stackoverflow.com/questions/344203/maximum-number-of-threads-per-process-in-linux
https://www.tutorialspoint.com/what-is-the-maximum-number-of-threads-per-process-in-linux
https://stackoverflow.com/questions/3044580/multiprocessing-vs-threading-python


aiohttp is faster than native asyncio:
(gpt):
Technical aspects of why aiohttp can be faster than using native asyncio directly for HTTP-related tasks:
Optimized Event Loop Integration: aiohttp integrates tightly with the asyncio event loop but adds additional optimizations tailored for HTTP traffic. This includes optimized handling of I/O events specifically for HTTP connections, reducing the overhead associated with generic event loop operations.
HTTP Parsing and Serialization: aiohttp utilizes efficient C-extensions for parsing and serializing HTTP messages. This low-level optimization ensures that the CPU cycles are minimized for these critical operations. The use of http_parser (a C library) allows for faster parsing compared to pure Python implementations.
Efficient Buffer Management: aiohttp implements advanced buffer management techniques to handle incoming and outgoing HTTP data. This includes strategies such as pooling buffers to reduce memory allocation overhead and using memoryviews to avoid unnecessary data copying.
Connection Pooling: aiohttp provides built-in connection pooling which allows for the reuse of TCP connections for multiple HTTP requests. This reduces the overhead of establishing new TCP connections, which involves several round trips and can be a significant bottleneck in high-throughput scenarios.
Custom I/O Handling: aiohttp has custom implementations for I/O operations, leveraging asyncio's transport and protocol abstractions but with optimizations for typical HTTP workloads. For example, it uses SelectorEventLoop efficiently to manage multiple socket connections concurrently.
Zero-Copy Sendfile Support: aiohttp can leverage the sendfile system call (where supported by the operating system), which allows for zero-copy file transfers directly from disk to network socket. This significantly reduces CPU usage and increases throughput for serving static files.
Concurrency Control: aiohttp includes mechanisms for controlling concurrency and limiting the number of simultaneous connections or requests, which helps prevent resource exhaustion and maintains performance under load. This is implemented through semaphore-based controls that are more sophisticated than basic asyncio primitives.
Protocol-Specific Optimizations: aiohttp optimizes the handling of specific HTTP features such as chunked transfer encoding, keep-alive connections, and HTTP/1.1 pipelining. These optimizations ensure that common patterns in HTTP communication are handled with minimal overhead.
Custom Executors for Blocking Operations: For operations that cannot be made non-blocking, aiohttp provides mechanisms to offload them to separate threads or processes using custom executors. This integration ensures that the main event loop remains responsive, which is crucial for handling high concurrency.
Memory Management: aiohttp implements various memory management techniques to minimize the footprint and avoid fragmentation. This includes efficient use of memory pools and careful management of object lifecycles to reduce garbage collection overhead.
By building on top of asyncio and adding these layers of optimizations and specialized handling, aiohttp is able to achieve higher performance for HTTP-related tasks than using asyncio directly. These enhancements allow aiohttp to handle a large number of concurrent HTTP requests more efficiently, making it a preferred choice for web applications and services that require high throughput and low latency.

Linux: 
https://unix.stackexchange.com/questions/727101/why-do-processes-on-linux-crash-if-they-use-a-lot-of-memory-yet-still-less-than

Pyspark Window functions - Learn about it - Google
https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application.html
https://joydipnath.medium.com/how-to-determine-executor-core-memory-and-size-for-a-spark-app-19310c60c0f7
https://sparkbyexamples.com/spark/spark-tune-executor-number-cores-and-memory/
https://community.cloudera.com/t5/Support-Questions/How-to-decide-spark-submit-configurations/m-p/226197
https://www.linkedin.com/pulse/apache-spark-things-keep-mind-while-setting-up-executors-deka

Go Memory model: 
https://go.dev/ref/mem

Misc (websites, linkedin, medium blogs, etc etc need to read) domain: 
https://news.ycombinator.com/
https://sachidisanayaka98.medium.com/how-chrome-browser-use-process-threads-643dff8ad32c
https://www.linkedin.com/posts/hnaser_in-the-beginning-for-the-os-to-write-to-activity-7163388923916861441-t1vw?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_the-big-win-of-using-threads-instead-of-processes-activity-7161147178546069506-yehp?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_fragmentation-is-a-very-interesting-topic-activity-7156142414989037568-6C96?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_today-i-learned-how-the-linux-option-netipv4-activity-7150555792662740992-w8fL?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_i-just-learned-that-in-addition-to-the-mapping-activity-7148454941404110848-8m4D?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_i-am-fascinated-by-gos-compiler-escape-analysis-activity-7144747978224746496-z-YZ?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_glad-mongo-fixed-this-in-62-so-prior-to-activity-7135553971066175489-nwm7?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_why-does-it-take-time-for-dns-to-resolve-activity-7134793549526528001-xjL0?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_a-connection-pool-is-always-a-good-idea-especially-activity-7134109245909725184-qaUE?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_graphql-was-invented-by-facebook-mainly-because-activity-7127490321701056513-DSxX?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_the-recent-cloudflare-api-outage-on-november-activity-7126989541537677312-upGW?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_http3-is-taking-over-the-world-but-consider-activity-7116186211039285248-Bae7?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_i-got-asked-how-vpn-works-on-x-so-here-is-activity-7110641803984322560--ONA?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_fun-networking-fact-http-related-pglocks-activity-7108275178979160064-gAVu?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_its-fascinating-to-know-how-jit-just-in-activity-7101992901496229888-_777?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_postgres-has-weak-locks-those-are-table-activity-7078250396678303744-p6WU?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_normally-when-you-write-to-disk-the-writes-activity-7067253338395852800-r2JY?utm_source=share&utm_medium=member_desktop
https://bugs.mysql.com/bug.php?id=109595
https://www.youtube.com/watch?v=lCb5BkJOOVI&list=PLQnljOFTspQU0ICDe-cL1EwXC4GDSayKY&index=43
https://medium.com/@hnasr/the-journey-of-a-request-to-the-backend-c3de704de223
https://blog.jcole.us/2014/04/16/the-basics-of-the-innodb-undo-logging-and-history-system/
https://medium.com/@hnasr/how-slow-is-select-8d4308ca1f0c
https://medium.com/@hnasr/what-happens-when-databases-crash-74540fd97ea9
https://www.linkedin.com/pulse/how-troubleshoot-long-postgres-startup-nikolay-samokhvalov/
https://keefmck.blogspot.com/2023/04/why-ssds-lie-about-flush.html?m=1
https://tontinton.com/posts/scheduling-internals/
https://stackoverflow.com/questions/1518711/how-does-free-know-how-much-to-free
https://blog.allegro.tech/2024/03/kafka-performance-analysis.html
https://www.youtube.com/watch?v=d86ws7mQYIg
https://www.linkedin.com/pulse/builder-design-pattern-prateek-mishra
Youtube/Linkedin/Twitter articles: Alex Xu, Arpit Bhayani, Hussaein Nasser - to watch/update
Substack/email articles

----------------------------------------------------------------------

Short notes from any book I'm reading: 
- 

----------------------------------------------------------------------

