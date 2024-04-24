
# Concurrency_vs_Parallelism

- **Concurrency** is when two or more tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. For example, multitasking on a single-core machine.
- **Parallelism** is when tasks literally run at the same time, e.g., on a multicore processor.
- Concurrent and parallel are effectively the same principle, both are related to tasks being executed simultaneously although we can say that parallel tasks should be truly multitasking, executed "at the same time" (multiple threads of execution executing simultaneously) whereas concurrent could mean that the tasks are sharing the execution thread while still appearing to be executing in parallel (managing multiple threads of execution).

Example: 
- Concurrency is like a person juggling balls with only 1 hand. Regardless of how it seems the person is only holding at most one ball at a time. Parallelism is when the juggler uses both hands.
- Concurrency is two lines of customers ordering from a single cashier (lines take turns ordering); Parallelism is two lines of customers ordering from two cashiers (each line gets its own cashier).

- As a note: Asynchronous methods aren't directly related to the previous two concepts, asynchrony is used to present the impression of concurrent or parallel tasking but effectively an asynchronous method call is normally used for a process that needs to do work away from the current application and we don't want to wait and block our application awaiting the response. 
  - Eg: For example, getting data from a database could take time but we don't want to block our UI waiting for the data. The async call takes a call-back reference and returns execution back to your code as soon as the request has been placed with the remote system. Your UI can continue to respond to the user while the remote system does whatever processing is required, once it returns the data to your call-back method then that method can update the UI (or handoff that update) as appropriate. From the user perspective, it appears like multitasking but it may not be.

[Concurrency & Parallellism _al](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism), [Concurrency, Parallellism, Asynchronous methods _al](https://stackoverflow.com/questions/4844637/what-is-the-difference-between-concurrency-parallelism-and-asynchronous-methods), [Concurrency, parallellism, threads, process, etc. _al](https://medium.com/swift-india/concurrency-parallelism-threads-processes-async-and-sync-related-39fd951bc61d)


----------------------------------------------------------------------





















