
# Generators_Iterables_Coroutines

- A **generator** function is a type of function that uses the **yield** keyword to create an **iterator**. It generates values lazily one at a time, allowing you to iterate over a potentially infinite sequence without storing the entire sequence in memory. Generators are memory-efficient and useful when you need to produce a stream of values on-the-fly. Generators are run with normal iteration (e.g., using for loops) and produce values one by one. 
  - **Iterable** is anything like a list or set or range or dict-view, with a built-in protocol for visiting each element inside the list/ set in a certain order. If the compiler detects the yield keyword anywhere inside a function, that function no longer returns via the return statement. Instead, it immediately returns a lazy 'pending list' 'object' called a generator. 
    - A generator is iterable. Basically, whenever the yield statement is encountered, the function pauses and saves its state, then emits "the next return value in the 'list'" according to the python iterator protocol. We lose the convenience of a container, but gain the power of a series that's computed as needed, and arbitrarily long. Yield is lazy, it puts off computation. A function with a yield in it doesn't actually execute at all when you call it. It returns an iterator object that remembers where it left off. Each time you call next() on the iterator (this happens in a for-loop) execution inches forward to the next yield. return raises StopIteration and ends the series (this is the natural end of a for-loop). Yield is versatile. Data doesn't have to be stored all together, it can be made available one at a time. It can be infinite. As an analogy, return and yield are twins. return means 'return and stop' whereas 'yield` means 'return, but continue'. [Yield in python _al](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python). Eg:

```
def countdown(n):
    while n > 0:
        yield n
        n -= 1
for num in countdown(5):
    print(num)
```

- A **coroutine** function is an asynchronous function that uses the **async** and **await** keywords to manage asynchronous operations. Coroutines can be paused and resumed, allowing other coroutines or tasks to execute while waiting for I/O operations. Inside a coroutine, you can use the await keyword to indicate points where the coroutine can pause and allow other tasks to run. They are particularly useful for I/O-bound operations, such as network requests, where waiting for external resources can lead to inefficiencies. Coroutines are run within an event loop using asyncio and can pause and resume during execution. Eg:

```
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

In summary, yield is used in generator functions to produce a sequence of values lazily, while await is used in asynchronous coroutines to pause the execution of the coroutine while waiting for an asynchronous operation to complete. generators for lazy iteration and coroutines for efficient asynchronous programming.


----------------------------------------------------------------------





















