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


--------------------------------

