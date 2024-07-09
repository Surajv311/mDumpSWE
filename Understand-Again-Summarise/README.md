
# Understand-Again-Summarise

Misc:
https://www.chiark.greenend.org.uk/~sgtatham/quasiblog/coroutines-philosophy/

Linux: 
https://unix.stackexchange.com/questions/727101/why-do-processes-on-linux-crash-if-they-use-a-lot-of-memory-yet-still-less-than
To list all users in a Linux system, you can read the /etc/passwd file. Each line in this file represents a user account, and the first field in each line is the username.

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
Java book: 

Together, the Java Virtual Machine and Java API form a "platform" for which all Java programs are compiled. In addition to being called the Java runtime system, the combination of the Java Virtual Machine and Java API is called the Java Platform.
<>
At the heart of Javaís network-orientation is the Java Virtual Machine, which supports all three prongs of Javaís network-oriented architecture: platform independence, security, and network-mobility.
The Java Virtual Machine is an abstract computer.
although all Java Virtual Machines must be able to execute Java bytecodes, they may use any technique to execute them. Also, the specification is flexible enough to allow a Java Virtual Machine to be implemented either completely in software or to varying degrees in hardware.
A Java Virtual Machineís main job is to load class files and execute the bytecodes they contain.
the Java Virtual Machine contains a class loader, which loads class files from both the program and the Java API. Only those class files from the Java API that are actually needed by a running program are loaded into the virtual machine. The bytecodes are executed in an execution engine, which is one part of the virtual machine that can vary in different implementations. On a Java Virtual Machine implemented in software, the simplest kind of execution engine just interprets the bytecodes one at a time. Another kind of execution engine, one that is faster but requires more memory, is a just-in-time compiler. In this scheme, the bytecodes of a method are compiled to native machine code the first time the method is invoked. The native machine code for the method is then cached, so it can be re-used the next time that same method is invoked. On a Java Virtual Machine built on top of a chip that executes Java bytecodes natively, the execution engine is actually embedded in the chip.
img of the engine <>
Sometimes the Java Virtual Machine is called the Java interpreter; however, given the various ways in which bytecodes can be executed, this term can be misleading. 
A Java method is written in the Java language, compiled to bytecodes, and stored in class files. A native method is written in some other language, such as C, C++, or assembly, and compiled to the native machine code of a particular processor. Native methods are stored in a dynamically linked library whose exact form is platform specific. While Java methods are platform independent, native methods are not. When a running Java program calls a native method, the virtual machine loads the dynamic library that contains the native method and invokes it.
You can use native methods to give your Java programs direct access to the resources of the underlying operating system. Their use, however, will render your program platform specific. This is because the dynamic libraries containing the native methods are platform specific. In addition, the use of native methods may render your program specific to a particular implementation of the Java Platform. One native method interface--the Java Native Interface, or JNI--enables native methods to work with any Java Platform implementation on a particular host computer. Vendors of the Java Platform, however, are not required to support JNI. They may provide their own proprietary native method interfaces in addition to (or in place of) JNI.
Java gives you a choice. If you want to access resources of a particular host that are unavailable through the Java API, you can write a platform-specific Java program that calls native methods. If you want to keep your program platform independent, however, you must call only Java methods and access the system resources of the underlying operating system through the Java API.

-----

Learning java book quick review:
The Java programming language, developed at Sun Microsystems under the guidance of Net luminaries James Gosling and Bill Joy, is designed to be a machine-independent programming language that is both safe enough to traverse networks and powerful enough to replace native executable code.
Initially, most of the enthusiasm for Java centered around its capabilities for building embedded applications for the World Wide Web; these applications are called applets. Applets could be independent programs in themselves, or sophisticated frontends to programs running on a server. More recently, interest has shifted to other areas. With Java 2, Java has the most sophisticated toolkit for building graphical user interfaces. 
Java is both a compiled and an interpreted language. Java source code is turned into simple binary instructions, much like ordinary microprocessor machine code. However, whereas C or C++ source is refined to native instructions for a particular model of processor, Java source is compiled into a universal format—instructions for a virtual machine.
Compiled Java byte-code, also called J-code, is executed by a Java runtime interpreter. The runtime system performs all the normal activities of a real processor, but it does so in a safe, virtual environment. It executes the stack-based instruction set and manages a storage heap. It creates and manipulates primitive datatypes, and loads and invokes newly referenced blocks of code. Most importantly, it does all this in accordance with a strictly defined open specification that can be implemented by anyone who wants to produce a Java-compliant virtual machine.
The Java interpreter is relatively lightweight and small; it can be implemented in whatever form is desirable for a particular platform. On most systems, the interpreter is written in a fast, natively compiled language like C or C++. The interpreter can be run as a separate application, or it can be embedded in another piece of software, such as a web browser.
All of this means that Java code is implicitly portable.

(gpt:)
I have a doubt related to java jvm. Correctly and detail my unerstanding if required: When I write a piece of c/c++ code - this code is turned into machine understandable bytecode which later runs on top of our computer processors directly. Hence c/c++ code is very computer hardware dependent to rely on speed and any other features. On the other hand, if we execute a java, code, it also is compied first which means turned into machine code, later this machine code enters the jvm whcih acts like a processor - basically jvm can be a software layer on top of an OS or we could also have specialized java specific chips in physical system having this jvm. Now, since this jvm is abstracted out, we run our machine code on the jvm which essentially does all tha handling of underlying physical processor or the os. So is my understanding correct? Also, why jvm is called interpretor then? 
Your understanding of how C/C++ and Java code are executed is mostly correct, but there are some nuances to clarify. Let's break it down:

C/C++ Code Execution
Compilation: When you write C/C++ code, it is compiled by a compiler into machine code (also called native code). This machine code is specific to the architecture of the computer's CPU (e.g., x86, ARM).
Execution: This machine code is executed directly by the computer's processor. Because it is compiled to run on a specific hardware architecture, it is very efficient but also hardware-dependent.
Java Code Execution
Compilation: When you write Java code, it is compiled by the Java compiler (javac) into bytecode, which is a platform-independent intermediate representation. This bytecode is not specific to any particular CPU architecture.
JVM (Java Virtual Machine):
Interpretation: The JVM can execute bytecode by interpreting it, which means reading and executing each instruction one at a time. This is why the JVM is often referred to as an interpreter.
Just-In-Time Compilation (JIT): Modern JVMs also use a technique called Just-In-Time (JIT) compilation. During execution, the JVM can compile frequently executed bytecode into native machine code for the host CPU. This native code is then executed directly by the CPU, improving performance.
Specialized Java Hardware
While the JVM is typically implemented as a software layer running on top of an operating system, there have been efforts to create hardware that can execute Java bytecode directly. These specialized chips are not common but theoretically possible.

Key Points
Hardware Dependence: C/C++ is directly compiled to machine code specific to the hardware, leading to efficient but hardware-dependent executables. Java is compiled to bytecode, which is hardware-independent, and relies on the JVM to handle execution.
JVM as an Interpreter: The JVM interprets bytecode, allowing Java to be platform-independent. It can also compile bytecode to native code at runtime for better performance.
Abstracted Execution: The JVM abstracts the underlying hardware and OS, providing a consistent execution environment across different platforms.
Why the JVM is Called an Interpreter
The term "interpreter" refers to the JVM's ability to execute bytecode directly, instruction by instruction, without needing to compile it to native machine code first. This allows for immediate execution of Java programs but can be slower compared to fully compiled code. The JIT compilation feature adds complexity, allowing parts of the bytecode to be compiled into native code during execution, thus bridging the gap between interpreted and fully compiled languages.

In summary, your understanding is on the right track, with the JVM acting as an abstraction layer that interprets and sometimes compiles Java bytecode to native code for execution.


in c++: 
Compilation: When you write C/C++ code, it is compiled by a compiler into machine code (also called native code). This machine code is specific to the architecture of the computer's CPU (e.g., x86, ARM).
Execution: This machine code is executed directly by the computer's processor. Because it is compiled to run on a specific hardware architecture, it is very efficient but also hardware-dependent.
can this machine code be executed in some other computer's processor with different settings? is there a possibility?
When C/C++ code is compiled into machine code, the resulting executable is tailored to the specific architecture and operating system for which it was compiled. This means the machine code is designed to run on a particular type of CPU (e.g., x86, ARM) and OS (e.g., Windows, Linux).

Running Machine Code on a Different Architecture
Direct Execution: Machine code compiled for one architecture cannot be executed directly on a different architecture. For example, a program compiled for an x86 CPU will not run on an ARM CPU because the instruction sets are different.

Compatibility Layers and Emulation:

Compatibility Layers: Some systems provide compatibility layers that allow executables compiled for one OS to run on another, provided the underlying CPU architecture is the same. For example, Wine on Linux can run Windows applications compiled for x86.
Emulators: Emulation software can simulate one CPU architecture on another, allowing machine code compiled for one type of processor to run on a different type. For instance, QEMU can emulate various CPU architectures, enabling execution of machine code designed for ARM on an x86 processor, albeit with a performance penalty.
Cross-Compilation
If you need to run C/C++ code on multiple architectures, the typical approach is to use cross-compilation:

Cross-Compilers: These are compilers that run on one architecture but generate machine code for another. For example, you can use an x86 machine to cross-compile a program for ARM.
Portable Code: By ensuring your source code adheres to standards and avoids architecture-specific features, you can compile the same code for different architectures using appropriate cross-compilers.
Virtual Machines and Containers
Virtual Machines (VMs): These can run different operating systems on the same hardware, allowing you to run executables compiled for different OSs on the same physical machine, provided the CPU architecture matches.
Containers: Tools like Docker allow you to package applications with their dependencies, ensuring they run consistently across different environments. However, the underlying architecture still needs to be compatible.
Conclusion
Machine code generated from C/C++ is specific to the CPU architecture and OS it was compiled for. To run this code on a different architecture, you would need:

Emulation to simulate the original architecture.
Recompilation of the source code for the target architecture.
Cross-compilation using a cross-compiler to generate the appropriate machine code for the target architecture.
Each approach has its trade-offs in terms of complexity, performance, and compatibility.

Just-In-Time Compilation (JIT): i did not understand
Just-In-Time (JIT) compilation is a key feature in many modern runtime environments, including the Java Virtual Machine (JVM). It helps improve the performance of interpreted languages by dynamically compiling parts of the bytecode into native machine code at runtime. Here's a detailed explanation:

What is JIT Compilation?
Interpretation vs. Compilation:

Interpreted Languages: Each line of code is read and executed one at a time by an interpreter. This can be slower because the interpretation process adds overhead.
Compiled Languages: The entire program is compiled into native machine code before execution, leading to faster runtime performance since the machine code runs directly on the CPU.
JIT Compilation: JIT compilation combines the benefits of both interpreted and compiled languages. It involves compiling bytecode into native machine code on the fly, during program execution. This allows for optimizations based on the actual runtime behavior of the application.

How JIT Compilation Works in the JVM
Bytecode Execution: When you run a Java program, the JVM starts by interpreting the bytecode. This means it reads and executes the bytecode instructions one at a time.

Hotspot Detection: The JVM monitors the execution of the bytecode and identifies "hotspots" – parts of the code that are executed frequently. These hotspots are good candidates for JIT compilation because they can benefit the most from optimization.

Compilation: Once a hotspot is identified, the JVM's JIT compiler compiles that part of the bytecode into native machine code. This machine code can be executed directly by the CPU, which is much faster than interpreting the bytecode.

Optimization: The JIT compiler can apply various optimizations that are only possible because it knows the actual runtime behavior of the application. For example, it can inline functions, optimize loops, and eliminate dead code.

Execution: After compilation, the JVM replaces the interpreted bytecode with the compiled native code. Subsequent executions of that code run much faster because they are now running as optimized native code.

Benefits of JIT Compilation
Performance: JIT compilation can significantly improve the performance of Java applications by converting frequently executed bytecode into optimized native code.
Portability: Java bytecode remains platform-independent, while the JIT compiler generates platform-specific native code at runtime.
Adaptive Optimization: The JIT compiler can optimize code based on the actual execution patterns and conditions, something that static compilers (used in languages like C/C++) cannot do.
Example
Consider a simple Java method:

java
Copy code
public int add(int a, int b) {
    return a + b;
}
When you run a Java program containing this method:

The JVM initially interprets the bytecode for the add method.
If the add method is called frequently, the JVM identifies it as a hotspot.
The JIT compiler then compiles the bytecode for the add method into native machine code.
Future calls to the add method will use the compiled native code, resulting in faster execution.

 When you run a Java program, the JVM starts by interpreting the bytecode. This means it reads and executes the bytecode instructions one at a time: So does jvm execute this on top of a machine? if that is the case, what benefit have we achieved with jvm, we have rather added another layer on top of running our code and made it slower?
The Java Virtual Machine (JVM) indeed adds an additional layer between your Java code and the underlying hardware, which may initially seem to make execution slower. However, the JVM provides several key benefits that outweigh this initial overhead:

Benefits of the JVM
Platform Independence:

Write Once, Run Anywhere: Java bytecode can run on any platform with a compatible JVM, making Java applications highly portable. You don't need to recompile your code for different operating systems or hardware architectures.
Security:

The JVM provides a secure execution environment. It includes features like bytecode verification and sandboxing to protect against malicious code execution.
Memory Management:

The JVM manages memory allocation and garbage collection, which helps prevent memory leaks and other related issues. This automatic memory management simplifies development and enhances application stability.
Performance Optimizations:

Just-In-Time (JIT) Compilation: As discussed earlier, the JVM can dynamically compile and optimize bytecode into native machine code at runtime, which significantly improves performance after the initial interpretation phase.
Adaptive Optimization: The JVM can optimize code based on runtime profiling, making it possible to tailor optimizations to the actual usage patterns of the application.
Extensive Libraries and Tools:

The JVM ecosystem includes a vast array of libraries, frameworks, and tools that simplify development and improve productivity. These resources can significantly reduce development time and effort.
Addressing the Initial Interpretation Overhead
While it's true that the JVM starts by interpreting bytecode, the initial overhead is usually mitigated by the following factors:

JIT Compilation:

The JVM quickly identifies frequently executed code (hotspots) and compiles them into optimized native code, reducing the performance gap between interpreted and fully compiled languages.
Modern JVMs use tiered compilation, starting with simple and fast optimizations and progressively applying more complex and time-consuming ones as the code continues to be executed frequently.
Startup Optimization:

Techniques like ahead-of-time (AOT) compilation can be used to compile some parts of the code before runtime, reducing the need for interpretation and JIT compilation during startup.
Caching:

Compiled native code is cached and reused, so repeated executions of the same code don't incur the same interpretation overhead.
Real-World Performance
In many real-world applications, the performance of Java applications running on the JVM can be comparable to, or even exceed, that of statically compiled languages like C or C++. This is due to the sophisticated runtime optimizations and the ability to adapt to the actual usage patterns of the application.

Conclusion
While the JVM adds an extra layer of abstraction, its benefits in terms of platform independence, security, memory management, and runtime optimizations make it a powerful and versatile execution environment. The initial performance overhead of interpretation is mitigated by JIT compilation and other optimizations, leading to high-performance applications in practice.
--------------------

(back to book)

The fundamental unit of Java code is the class. As in other object-oriented languages, classes are application components that hold executable code and data. Compiled Java classes are distributed in a universal binary format that contains Java byte-code and other class information. Classes can be maintained discretely and stored in files or archives on a local system or on a network server. Classes are located and loaded dynamically at runtime, as they are needed by an application.

Java has a number of fundamental classes that contain architecture-dependent methods. These native methods serve as the gateway between the Java virtual machine and the real world. They are implemented in a natively compiled language on the host platform. They provide access to resources such as the network, the windowing system, and the host filesystem. The rest of Java is written entirely in Java, and is therefore portable. This includes fundamental Java utilities like the Java compiler and Sun's HotJava web browser, which are also Java applications and are therefore available on all Java platforms.

Historically, interpreters have been considered slow, but because the Java interpreter runs compiled byte-code, Java is a relatively fast interpreted language. More importantly, Java has also been designed so that software implementations of the runtime system can optimize their performance by compiling byte-code to native machine code on the fly. This is called just-in-time compilation. Sun claims that with just-in-time compilation, Java code can execute nearly as fast as native compiled code and maintain its transportability and security. There is only one true performance hit that compiled Java code will always suffer for the sake of security — array bounds checking. But on the other hand, some of the basic design features of Java place more information in the hands of the compiler, which allows for certain kinds of optimizations not possible in C or C++.
The latest twist in compilation techniques is a new virtual machine that Sun calls HotSpot. The problem with a traditional just-in-time compilation is that optimizing code takes time, and is extremely important for good performance on modern computer hardware. So a just-in-time compiler can produce decent results, but can never afford to take the time necessary to do a good job of optimization. HotSpot uses a trick called "adaptive compilation" to solve this problem. If you look at what programs actually spend their time doing, it turns out that they spend almost all
of their time executing a relatively small part of the code again and again. The chunk of code that is executed repeatedly may only be a small percent of the total program, but its behavior determines the program's overall performance.
To take advantage of this fact, HotSpot starts out as a normal Java byte code interpreter, but with a difference: it measures (profiles) the code as it is executing, to see what parts are being executed repeatedly. Once it knows which parts of the code are crucial to the performance, HotSpot compiles those sections—and only those sections—into true machine code. Since it only compiles a small portion of the program into machine code, it can afford to take the time necessary to optimize those portions. The rest of the program may not need to be compiled at all—just interpreted—saving memory and time.
The technology for doing this is very complex, but the idea is essentially simple: optimize the parts of the program that need to go fast, and don't worry about the rest. Another advantage of using an adaptive compiler at runtime is that it can make novel kinds of optimizations that a static (compile time only) compiler cannot dream of.

--
detour: 

The Compiler and Interpreter, both have similar works to perform. Interpreters and Compilers convert the Source Code (HLL) to Machine Code (understandable by Computer).
A compiler translates code written in a high-level programming language into a lower-level language like assembly language, object code and machine code (binary 1 and 0 bits). It converts the code ahead of time before the program runs.
An interpreter translates the code line-by-line when the program is running. Interpreters, more often than not are smaller than compilers. 
Compilers can contain interpreters for optimization reasons like faster performance and smaller memory footprint.
4 Types of Interpreters
Bytecode interpreter
Threaded code interpreter
Abstract syntax tree interpreter
Justin-in-time compilation
10 Types of Compilers
Cross-compiler
Native compiler
Bootstrap compiler
Decompiler
Source-to-source compiler
Language rewriter
Bytecode compiler
Just-in-time compiler
AOT compilation
Assembler


Java is an OOP programming language while Java Script is an OOP scripting language. Java creates applications that run in a virtual machine or browser while JavaScript code is run on a browser only. 
Java is a statically typed language; JavaScript is dynamic.
Java is class-based; JavaScript is prototype-based.
Java constructors are special functions that can only be called at object creation; JavaScript "constructors" are just standard functions.
Java requires all non-block statements to end with a semicolon; JavaScript inserts semicolons at the ends of certain lines.
Java uses block-based scoping; JavaScript uses function-based scoping.
Java has an implicit this scope for non-static methods, and implicit class scope; JavaScript has implicit global scope.


Scripting languages are generally interpreted. Programming languages are typically compiled. This means that scripting languages are executed directly by the interpreter, while programming languages are first translated into machine code by the compiler before being executed.
Programming languages create exe file, scripting languages don't.




























----------------------------------------------------------------------

