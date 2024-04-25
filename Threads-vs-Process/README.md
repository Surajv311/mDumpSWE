
# Threads_vs_Process

Process means any program is in execution. Thread means a segment of a process. The process takes more time to terminate. The thread takes less time to terminate. Process takes more time for creation. It takes less time for creation. 

Processes and threads can be considered similar, but a big difference is that a process is much larger than a thread. For that reason, it is not good to have switching between processes. There is too much information in a process that would have to be saved and reloaded each time the CPU decides to switch processes. A thread on the other hand is smaller and so it is better for switching. A process may have multiple threads that run concurrently, meaning not at the same exact time, but run together and switch between them. The context switching here is better because a thread won't have as much information to store/reload.

Another explanation: 

Firstly, a program is an executable file. 

It contains the code, or a set of processor instructions, that is stored as a file on disk. When the code in a program is loaded into memory and executed by the processor, it becomes a process. An active process also includes the  resources the program needs to run. These resources are managed  by the operating system. Some examples are processor registers, program counters, stack pointers, memory pages assigned to  the process for its heap and stack, etc. There is an important property of a process that is worth mentioning. Each process has its own memory address space. One process cannot corrupt the  memory space of another process. This means that when one process malfunctions, other processes keep running. Chrome is famous for taking advantage of this process isolation by running each tab in its own process. When one tab misbehaves due to a bug or a malicious attack, other tabs are unaffected. 

A thread is the unit of execution within a process. 

A process has at least one thread. It is called the main thread. It is not uncommon for a  process to have many threads. Each thread has its own stack. Earlier we mentioned registers, program counters,  and stack pointers as being part of a process. It is more accurate to say that those things belong to a thread. 

Threads within a process share a memory address space. It is possible to communicate between threads using that shared memory space. However, one misbehaving thread could bring down the entire process. The operating system run a thread or process on a CPU by context switching. During a context switch, one process is switched out of the CPU so another process can run. The operating system stores the  states of the current running process so the process can be restored  and resume execution at a later point. It then restores the previously saved states of a different process and resumes execution for that process. Context switching is expensive. It involves saving and loading of registers, switching out memory pages, and updating various kernel data structures. Switching execution between threads also requires context switching. 

It is generally faster to switch context  between threads than between processes. There are fewer states to track, and more importantly, since threads share the same memory address space, there is no need to switch out virtual memory pages, which is one of the most expensive operations during a context switch. 

Context switching is so costly there are other mechanisms to try to minimize it. Some examples are fibers and coroutines. These mechanisms trade complexity for even lower context-switching costs. In general, they are cooperatively scheduled, that is, they must yield control for others to run. In other words, the application itself handles task scheduling. It is the responsibility of the application to make sure a long-running task is broken up by yielding periodically. 
[Process vs Thread _al](https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread), [Process vs Thread _vl](https://www.youtube.com/watch?v=4rLW7zg21gI)

----------------------------------------------------------------------





















