## Inside the Java Virtual Machine (Bill Venners)

#### Interesting points/notes:

- Chapter 1: Introduction to Javaís Architecture
  - At the heart of Java technology lies the Java Virtual Machine--the ***abstract computer on which all Java programs run***.
  - One challenge presented to developers by a networked computing environment is the wide range of devices that networks interconnect. A typical network usually has many different kinds of attached devices, with diverse hardware architectures, operating systems, and purposes. Java addresses this challenge by: 
    - Platform independence: Enabling the creation of platform-independent programs. A single Java program can run unchanged on a wide range of computers and devices. Compared with programs compiled for a specific hardware and operating system, platform-independent programs written in Java can be easier and cheaper to develop, administer, and maintain.
    - Network mobility: Another challenge the network presents to software developers is security - Java covers it. 
    - Security: One opportunity created by an omnipresent network is online software distribution. Java takes advantage of this opportunity by enabling the transmission of binary code in small pieces across networks. 
  - ***Javaís architecture*** arises out of four distinct but interrelated technologies, each of which is defined by a separate specification from Sun Microsystems:
    - the Java programming language
    - the Java class file format
    - the Java Application Programming Interface 
    - the Java Virtual Machine
  - Together, the Java Virtual Machine and Java API form a "platform" for which all Java programs are compiled. In addition to being called the Java runtime system, the combination of the Java Virtual Machine and Java API is called the Java Platform.

<> add java img <><>

  - Although ***all Java Virtual Machines must be able to execute Java bytecodes***, they may use any technique to execute them. Also, the specification is flexible enough to allow a Java Virtual Machine to be implemented either completely in software or to varying degrees in hardware.
  - A Java Virtual Machine's job is to load class files and execute the bytecodes they contain. The Java Virtual Machine contains a class loader, which loads class files from both the program and the Java API. Only those class files from the Java API that are actually needed by a running program are loaded into the virtual machine. The bytecodes are executed in an execution engine, which is one part of the virtual machine that can vary in different implementations. 
  - On a Java Virtual Machine implemented in software, the simplest kind of execution engine just interprets the bytecodes one at a time. Another kind of execution engine, one that is faster but requires more memory, is a just-in-time compiler. In this scheme, the bytecodes of a method are compiled to native machine code the first time the method is invoked. The native machine code for the method is then cached, so it can be re-used the next time that same method is invoked. On a Java Virtual Machine built on top of a chip that executes Java bytecodes natively, the execution engine is actually embedded in the chip.

<> img of the engine <>

  - Sometimes the Java Virtual Machine is called the Java interpreter; however, given the various ways in which bytecodes can be executed, this term can be misleading. 
  - A Java method is written in the Java language, compiled to bytecodes, and stored in class files. A native method is written in some other language, such as C, C++, or assembly, and compiled to the native machine code of a particular processor. Native methods are stored in a dynamically linked library whose exact form is platform specific. While Java methods are platform independent, native methods are not. When a running Java program calls a native method, the virtual machine loads the dynamic library that contains the native method and invokes it. You can use native methods to give your Java programs direct access to the resources of the underlying operating system. Their use, however, will render your program platform specific. This is because the dynamic libraries containing the native methods are platform specific. In addition, the use of native methods may render your program specific to a particular implementation of the Java Platform. One native method interface--the Java Native Interface, or JNI--enables native methods to work with any Java Platform implementation on a particular host computer. Vendors of the Java Platform, however, are not required to support JNI. They may provide their own proprietary native method interfaces in addition to (or in place of) JNI.
    - Java gives you a choice. If you want to access resources of a particular host that are unavailable through the Java API, you can write a platform-specific Java program that calls native methods. If you want to keep your program platform independent, however, you must call only Java methods and access the system resources of the underlying operating system through the Java API.
  
```
(gpt):
Java-specific code using the Java API:
import java.io.File;
public class JavaAPIExample {
    public static void main(String[] args) {
        // Get the user's home directory
        String homeDir = System.getProperty("user.home");
        System.out.println("User's home directory: " + homeDir);
        // Create a file in the user's home directory
        File file = new File(homeDir, "example.txt");
        if (file.createNewFile()) {
            System.out.println("File created: " + file.getAbsolutePath());
        } else {
            System.out.println("File already exists: " + file.getAbsolutePath());
        }
    }
}

Java program calling native methods:
public class NativeMethodExample {
    public static native int getProcessID();
    static {
        System.loadLibrary("nativelib");
    }

    public static void main(String[] args) {
        int processID = getProcessID();
        System.out.println("Process ID: " + processID);
    }
}
```

- 
A Java application can use two types of class loaders: a "primordial" class loader and class loader objects. 

Because of class loader objects, you donít have to know at compile-time all the classes that may ultimately take part in a running Java application. They enable you to dynamically extend a Java application at run-time. As it runs, your application can determine what extra classes it needs and load them through one or more class loader objects. Because you write the class loader in Java, you can load classes in any manner.

The Java class file helps make Java suitable for networks mainly in the areas of platform-independence and network-mobility. Its role in platform independence is serving as a binary form for Java programs that is expected by the Java Virtual Machine but independent of underlying host platforms. This approach breaks with the tradition followed by languages such as C or C++. Programs written in these languages are most often compiled and linked into a single binary executable file specific to a particular hardware platform and operating system. In general, a binary executable file for one platform wonít
work on another. The Java class file, by contrast, is a binary file that can be run on any hardware platform and operating system that hosts the Java Virtual Machine.
When you compile and link a C++ program, the executable binary file you get is specific to a particular target hardware platform and operating system because it contains machine language specific to the target processor. A Java compiler, by contrast, translates the instructions of the Java source files into bytecodes, the "machine language" of the Java Virtual Machine.
In addition to processor-specific machine language, another platform-dependent attribute of a traditional binary executable file is the byte order of integers. In executable binary files for the Intel X86 family of processors, for example, the byte order is little-endian, or lower order byte first. In executable files for the PowerPC chip, however, the byte order is big-endian, or higher order byte first. In a Java class file, byte order is big-endian irrespective of what platform generated the file and independent of whatever platforms may eventually use it.

<add image 9 > <> <>

The graphical user interface library of the Java API, called the Abstract Windows Toolkit (or AWT), is designed to facilitate the creation of user interfaces that work on all platforms. 

Another way Java prevents you from inadvertently corrupting memory is through automatic garbage collection. Java has a new operator, just like C++, that you use to allocate memory on the heap for a new object. But unlike C++, Java has no corresponding delete operator, which C++ programmers use to free the memory for an object that is no longer needed by the program. In Java, you merely stop referencing an object, and at some later time, the garbage collector will reclaim the memory occupied by the object.
You can be more productive in Java in part because you donít have to chase down memory corruption bugs.

When the Java program runs, a virtual machine loads the class files and executes the
bytecodes they contain. When running on a virtual machine that interprets bytecodes, a Java program may be 10 to 30 times slower than an equivalent C++ program compiled to native machine code.
This performance degradation is primarily a tradeoff in exchange for platform independence. Instead of compiling a Java program to platform-specific native machine code, you compile it to platform independent Java bytecodes. Native machine code can run fast, but only on the native platform. Java bytecodes (when interpreted) run slowly, but can be executed on any platform that hosts the Java Virtual Machine.
Fortunately, other techniques can improve the performance of bytecode execution. For example, just-in- time compiling can speed up program execution 7 to 10 times over interpreting. 




Java programs can run slower than an equivalent C++ program for many reasons:
l Interpreting bytecodes is 10 to 30 times slower than native execution.
l Just-in-time compiling bytecodes can be 7 to 10 times faster than interpreting, but still not quite as
fast as native execution.
l Java programs are dynamically linked.
l The Java Virtual Machine may have to wait for class files to download across a network.
l Array bounds are checked on each array access.
l All objects are created on the heap (no objects are created on the stack).
l All uses of object references are checked at run-time for null .
l All reference casts are checked at run-time for type safety.
l The garbage collector is likely less efficient (though often more effective) at managing the heap
than you could be if you managed it directly as in C++.
l Primitive types in Java are the same on every platform, rather than adjusting to the most efficient
size on each platform as in C++.
l Strings in Java are always UNICODE. When you really need to manipulate just an ASCII string, a
Java program will be slightly less efficient than an equivalent C++ program.

One area in which you can expect improvement over time is in the execution speed of Java programs. Sun, for example, is currently working on a technology they call "hot-spot compiling," which is a hybrid of interpreting and just-in- time compiling. 

Programs often spend 80 or 90 percent of their time in 10 to 20 percent of the code. To be most effective, you should focus your optimization efforts on just the 10 to 20 percent of the code that really matters to execution speed.


chapter 2

































--------------------------------

