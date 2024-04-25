
# Dask

Dask is a parallel and distributed computing library that scales the existing Python and PyData ecosystem. Dask scales Python code from multi-core local machines to large distributed clusters in the cloud. 

Dask consists of three main components: a **client**, a **scheduler**, and one or more **workers** (they communicate using messages): 

- As an engineer, you’ll communicate directly with the Dask Client. It sends instructions to the scheduler and collects results from the workers.
- The Scheduler is the midpoint between the workers and the client. It tracks metrics, and allows the workers to coordinate. 
- The Workers are threads, processes, or separate machines in a cluster. They execute the computations from the computation graph. Each worker contains a ThreadPool that it uses to evaluate tasks as requested by the scheduler. It stores the results of these tasks locally and serves them to other workers or clients on demand, it can also reach out to other workers to gather the necessary dependencies if needed. 

A **Dask graph** is a dictionary mapping keys to computations:
```
{'x': 1,
 'y': 2,
 'z': (add, 'x', 'y'), // Computation function
 'w': (sum, ['x', 'y', 'z']), // Some computation being performed 
 'v': [(sum, ['w', 'z']), 2]}
```
- A key is any hashable value that is not a task. 
- A task is a tuple (allowed duplicates, ordered, immutable i.e we can not make any changes in it) with a callable first element. Tasks represent atomic units of work meant to be run by a single worker. 

The size of the Dask graph depends on two things:
- The number of tasks.
- The size of each task.

```
Having either lots of smaller tasks or some overly large tasks can lead to the same outcome: the size in bytes of the serialized task graph becomes too big for the Scheduler to handle. 
```

After we create a dask graph, we use a scheduler to run it. The entry point for all schedulers is a get function. Dask currently implements a few different schedulers (Single machine & Distributed Schedular - 2 family of schedular):

```
dask.threaded.get: a scheduler backed by a **thread pool**
dask.multiprocessing.get: a scheduler backed by a **process pool**
dask.get: a synchronous scheduler, good for debugging
distributed.Client.get: a distributed scheduler for executing graphs on multiple machines. This lives in the external distributed project.
```

- In dask this function: map_partitions(func, *args[, meta, ...]) Apply Python function on each DataFrame partition.
- compute() method in dask: Dask does lazy evaluation, just like spark. This function will block until the computation is finished, going straight from a lazy dask collection to a concrete value in local memory. For example a Dask array turns into a NumPy array and a Dask dataframe turns into a Pandas dataframe. The entire dataset must fit into memory before calling this operation.
- [Dask df best practices _al](https://docs.dask.org/en/latest/dataframe-best-practices.html), in short: Reduce and then use pandas, Use the Index, Avoid Full-Data Shuffling, Persist Intelligently, Repartition to Reduce Overhead, Joins, Use Parquet format data. 
- [Strategy to partition dask df _al](https://stackoverflow.com/questions/44657631/strategy-for-partitioning-dask-dataframes-efficiently)


----------------------------------------------------------------------





















