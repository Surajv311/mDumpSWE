
# CPU_Threads_vs_Cores

- Core is an individual physical processing unit, while threads are virtual sequences of instructions. Think of threads as conveyor belts of products that are being sent to the worker (which is the core).
- Hardware on the CPU is a physical core & a logical core is more like code it exists, i.e threads.
- If a CPU has more threads than cores, say 4 cores, 8 threads so 2 threads per core, in such case, the core would be context switching between each thread to process the task. It cannot process both at the same time, some downtime will be there due to switching. This is also an example of what we call - concurrent execution.
- On a single-core CPU, you're only ever going to have one thread running at a time, but on a multi-core CPU, it's possible to run more than one thread simultaneously. 
- If your threads don't do I/O, synchronization, etc., and there's nothing else running, 1 thread per core will get you the best performance. However that very likely not the case. Adding more threads usually helps, but after some point, they cause some performance degradation.

[Cores vs threads _vl](https://www.youtube.com/watch?v=hwTYDQ0zZOw), [Cores, threads difference in graphic design _vl](https://www.youtube.com/watch?v=VCUvknmi5QA), [Threads per core performance _al](https://stackoverflow.com/a/10670440/24099524)


----------------------------------------------------------------------





















