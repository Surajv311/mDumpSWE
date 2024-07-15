
# Java

#### Java Int vs int 
- The key difference between the Java int and Integer types is that an int simply represents a whole number, while an Integer has additional properties and methods. 
- The Integer class is an Object while an int is a primitive type. The Integer class allows conversion to float, double, long and short, while the int doesn’t.
- The Integer is compared with .equals while the int uses two equal signs, == .

[Java Int vs int _al](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/int-vs-Integer-java-difference-comparison-primitive-object-types)

#### [Java virtual threads](https://medium.com/@RamLakshmanan/java-virtual-threads-easy-introduction-44d96b8270f8)
Java virtual threads is a new feature introduced in JDK 19. It has potential to improve an applications availability, throughput and code quality on top of reducing memory consumption.
Let’s walkthrough a typical lifecycle of a thread:

1. Thread is created in a thread pool
2. Thread waits in the pool for a new request to come
3. Once the new request comes, the thread picks up the request and it makes a backend Database call to service this request.
4. Thread waits for response from the backend Database
5. Once response comes back from the Database, the thread processes it, and sends back the response to customer
6. Thread is returned back to the thread pool

Step #2 to #6 will repeat until the application is shutdown. If you notice, the thread is actually doing real work only in step #3 and #5. In all other steps(i.e., step #1, step #2, step #4, step #6), it is basically waiting(or doing nothing). In most applications, a significant number of threads predominantly waits during most of its lifetime.

In the previous release of JVM(Java Virtual Machine), there was only one type of thread. It’s called as ‘classic’ or ‘platform’ thread. Whenever a platform thread is created, an operating system thread is allocated to it. Only when the platform thread exits(i.e., dies) the JVM, this operating system thread is free to do other tasks. Until then, it cannot do any other tasks. Basically, there is a 1:1 mapping between a platform thread and an operating system thread.

According to this architecture, OS thread will be unnecessarily locked down in step #1, step #2, step #4, step #6 of the thread’s life cycle, even though it’s not doing anything during these steps. Since OS threads are precious and finite resources, it’s time is extensively wasted in this platform threads architecture.

In order to efficiently use underlying operating system threads, virtual threads have been introduced in JDK 19. In this new architecture, a virtual thread will be assigned to a platform thread (aka carrier thread) only when it executes real work. As per the above-described thread’s life cycle, only during step #3 and step #5 virtual thread will be assigned to the platform thread(which in turn uses OS thread) for execution. In all other steps, virtual thread will be residing as objects in the Java heap memory region just like any of your application objects. Thus, they are lightweight and more efficient.

- Java Green Threads vs Virtual Threads _al
  - Green Threads had an N:1 mapping with OS Threads. All the Green Threads run on a single OS Thread. With Virtual Threads, multiple virtual threads can run on multiple native threads (n:m mapping). Java's green threads all shared one OS thread (M:1 scheduling) and were eventually outperformed by platform threads (Java's Native Threads) implemented as wrappers for OS threads (1:1 scheduling). Virtual threads employ M:N scheduling, where a large number (M) of virtual threads is scheduled to run on a smaller number (N) of OS threads; (Or)
  - Traditional threads in Java are akin to workers in our factory analogy. Each thread represents a separate path of execution, allowing your program to perform multiple operations simultaneously. Java threads are managed by the Java Virtual Machine (JVM) and are mapped to native operating system threads. This means that each Java thread is, in most cases, a direct representation of a thread in your operating system. When you create a thread in Java, the JVM requests the underlying operating system to allocate resources for that thread. This includes memory for the thread’s stack and CPU time for execution. Threads are crucial for any application that requires multitasking. For instance, a web server handles multiple client requests simultaneously, with each request potentially being handled by a separate thread. One of the main challenges with traditional threading is resource management. Each thread consumes significant memory and processing power. Context switching, where the CPU switches between different threads, can be resource-intensive, especially when there are many threads. This can lead to performance issues in heavily multi-threaded applications. As we’ve seen, traditional threads in Java are powerful but come with their own set of challenges. Virtual Threads, introduced as part of Project Loom, are a new kind of thread in Java. Unlike traditional threads, which are mapped one-to-one with operating system (OS) threads, virtual threads are lightweight and managed entirely by the Java Virtual Machine (JVM). They are sometimes referred to as “user-mode threads” or “green threads,” distinguishing them from the “kernel-mode threads” used by the OS. Virtual threads are created in the JVM, which then schedules them for execution. These threads can be suspended and resumed very efficiently by the JVM, especially during I/O operations. In traditional threading, a thread waiting for an I/O operation is typically inactive but still consumes resources. Virtual threads, however, are suspended without consuming resources, allowing other threads to utilize the CPU. The JVM’s ability to handle many virtual threads simultaneously enables a more efficient use of system resources, particularly in I/O-bound applications. Benefits: Resource Efficiency, Simplified Concurrency, Improved Application Performance.
  - [green/virtual threads _al](https://sachinthah.medium.com/understanding-java-virtual-threads-a-beginners-guide-7ad4c14304e7), [java virtual threads article 2 _al](https://medium.com/@RamLakshmanan/java-virtual-threads-easy-introduction-44d96b8270f8), [java virtual threads article 3 _al](https://medium.com/@souravdas08/java-virtual-threads-3057911143cc), [java virtual threads article 4 _al](https://stackoverflow.com/questions/74639116/what-is-the-difference-between-green-threads-and-virtual-threads).

#### Java enum

The Enum in Java is a data type which contains a fixed set of constants. Eg: 

```
class EnumExample1{  
//defining the enum inside the class  
public enum Season { WINTER, SPRING, SUMMER, FALL }  
//main method  
public static void main(String[] args) {  
//traversing the enum  
for (Season s : Season.values())  
System.out.println(s);  
}}  
```

#### JIT Compiler 
Bytecode is one of the most important features of java that aids in cross-platform execution. The way of converting bytecode to native machine language for execution has a huge impact on its speed of it. 

These bytecodes have to be interpreted or compiled to proper machine instructions depending on the instruction set architecture. Moreover, these can be directly executed if the instruction architecture is bytecode based. Interpreting the bytecode affects the speed of execution. 

In order to improve performance, JIT compilers interact with the Java Virtual Machine (JVM) at run time and compile suitable bytecode sequences into native machine code. While using a JIT compiler, the hardware is able to execute the native code, as compared to having the JVM interpret the same sequence of bytecode repeatedly and incurring overhead for the translation process. This subsequently leads to performance gains in the execution speed, unless the compiled methods are executed less frequently. 

The JIT compiler is able to perform certain simple optimizations while compiling a series of bytecode to native machine language. Some of these optimizations performed by JIT compilers are data analysis, reduction of memory accesses by register allocation, translation from stack operations to register operations, elimination of common sub-expressions, etc. 

The greater the degree of optimization done, the more time a JIT compiler spends in the execution stage. Therefore it cannot afford to do all the optimizations that a static compiler is capable of, because of the extra overhead added to the execution time and moreover its view of the program is also restricted.

#### Othersjava

- Jackson Object Mapper method can be used to serialize any Java value as a byte array.
- The Java Persistence API (JPA) is used to persist data between Java object and relational database. 
- Object Relational Mapping (ORM) is a functionality which is used to develop and maintain a relationship between an object and relational database by mapping an object state to database column. It is capable to handle various database operations easily such as inserting, updating, deleting etc.
- Garbage Collection is process of reclaiming the runtime unused memory automatically. Java garbage collection is an automatic process.
- When can singleton class in java be compromised?: 
  - A java singleton class is a class that can have only one object (an instance of the class) at a time. After the first time, if we try to instantiate the Java Singleton classes, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.
  - The primary purpose of a java Singleton class is to restrict the limit of the number of object creations to only one. This often ensures that there is access control to resources, for example, socket or database connection.
  - The singleton pattern can break if: [Break a singleton pattern in Java _al](https://stackoverflow.com/questions/20421920/what-are-the-different-ways-we-can-break-a-singleton-pattern-in-java), [Singleton Pattern prevent from Reflection, Serialization and Cloning _al](https://www.geeksforgeeks.org/prevent-singleton-pattern-reflection-serialization-cloning/)
  - Eg: 

```
class Singleton {
    // Static variable reference of single_instance of type Singleton
    private static Singleton single_instance = null;
    public String s;
 
    // Here we will be creating private constructor restricted to this class itself
    private Singleton()
    {
        s = "Hello I am a string part of Singleton class";
    }
    // Static method to create instance of Singleton class
    public static synchronized Singleton getInstance()
    {
        if (single_instance == null)
            single_instance = new Singleton();
 
        return single_instance;
    }
}
```

- Reflection in Java, is an API that is used to examine or modify the behavior of methods, classes, and interfaces at runtime. [Java reflection _al](https://www.geeksforgeeks.org/reflection-in-java/)


----------------------------------------------------------------------





















