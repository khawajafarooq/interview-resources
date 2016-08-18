Java Core:

#The Architecture
http://www.artima.com/insidejvm/ed2/introarch2.html

Java's architecture arises out of four distinct but interrelated technologies:

    the Java programming language
    the Java class file format
    the Java Application Programming Interface
    the Java virtual machine 

When you write and run a Java program, you are tapping the power of these four technologies. You express the program in source files 
written in the Java programming language, compile the source to Java class files, and run the class files on a Java virtual machine. 
When you write your program, you access system resources (such as I/O, for example) by calling methods in the classes that implement 
the Java Application Programming Interface, or Java API. As your program runs, it fulfills your program's Java API calls by invoking 
methods in class files that implement the Java API.

![Java Programming Environment](http://www.artima.com/insidejvm/ed2/images/fig1-1.gif "Java Programming Environment")

Together, the Java virtual machine and Java API form a "platform" for which all Java programs are compiled. In addition to being called the Java runtime system, the combination of the Java virtual machine and Java API is called the Java Platform (or, starting with version 1.2, the Java 2 Platform). Java programs can run on many different kinds of computers because the Java Platform can itself be implemented in software. 

![Java Platform](http://www.artima.com/insidejvm/ed2/images/fig1-2.gif "Java Platform")

Also, the specification is flexible enough to allow a Java virtual machine to be implemented either completely in software or to varying degrees in hardware. The flexible nature of the Java virtual machine's specification enables it to be implemented on a wide variety of computers and devices. 

A Java virtual machine's main job is to load class files and execute the bytecodes they contain. As you can see in Figure below, the Java virtual machine contains a class loader, which loads class files from both the program and the Java API. Only those class files from the Java API that are actually needed by a running program are loaded into the virtual machine. The bytecodes are executed in an execution engine.
![JVM](http://www.artima.com/insidejvm/ed2/images/fig1-3.gif "JVM")

The execution engine is one part of the virtual machine that can vary in different implementations. It can be implemented in software and hardware.

###Software based execution engines:

- Simple execution engine: That just inteprets the bytecode one at a time.
- Just in Time (JIT): In this scheme, the bytecodes of a method are compiled to native machine code the first time the method is invoked. The native machine code for the method is then cached, so it can be re-used the next time that same method is invoked.
- Adaptive optimizer: In this approach, the virtual machine starts by interpreting bytecodes, but monitors the activity of the running program and identifies the most heavily used areas of code. As the program runs, the virtual machine compiles to native and optimizes just these heavily used areas. The rest of the of code, which is not heavily used, remain as bytecodes which the virtual machine continues to interpret. This adaptive optimization approach enables a Java virtual machine to spend typically 80 to 90% of its time executing highly optimized native code, while requiring it to compile and optimize only the 10 to 20% of the code that really matters to performance.

###Hardware based execution engine: 
On a Java virtual machine built on top of a chip that executes Java bytecodes natively, the execution engine is actually embedded in the chip. 

###Native Methods:
When running on a Java virtual machine that is implemented in software on top of a host operating system, a Java program interacts with the host by invoking native methods. In Java, there are two kinds of methods: Java and native. A Java method is written in the Java language, compiled to bytecodes, and stored in class files. A native method is written in some other language, such as C, C++, or assembly, and compiled to the native machine code of a particular processor. Native methods are stored in a dynamically linked library whose exact form is platform specific. While Java methods are platform independent, native methods are not. When a running Java program calls a native method, the virtual machine loads the dynamic library that contains the native method and invokes it. As you can see in Figure below, native methods are the connection between a Java program and an underlying host operating system.

![Native Method Invocation](http://www.artima.com/insidejvm/ed2/images/fig1-4.gif "Native Method Invocation")

    Java gives you a choice. If you want to access resources of a particular host that are unavailable through the Java API, you can
    write a platform-specific Java program that calls native methods. If you want to keep your program platform independent, however, you
    must access the system resources of the underlying operating system only through the Java API.

###Class Files:
    The Java class file, by contrast, is a binary file that can be run on any hardware platform and operating system that hosts the Java virtual machine. 
    
    A Java compiler, by contrast, translates the instructions of the Java source files into bytecodes, the "machine language" of the Java virtual machine. 
    
    In a Java class file, byte order is big-endian irrespective of what platform generated the file and independent of whatever platforms may eventually use it. 
    
###Java API:
The Java API is set of runtime libraries that give you a standard way to access the system resources of a host computer. When you write a Java program, you assume the class files of the Java API will be available at any Java virtual machine that may ever have the privilege of running your program. This is a relatively safe assumption because the Java virtual machine and the class files for the Java API are the required components of any implementation of the Java Platform.

The combination of all loaded class files (from your program and from the Java API) and any loaded dynamic libraries (containing native methods) constitute the full program executed by the Java virtual machine. 

The class files of the Java API are inherently specific to the host platform. The API's functionality must be implemented expressly for a particular platform before that platform can host Java programs. To access the native resources of the host, the Java API calls native methods. As you can see in Figure below, the class files of the Java API invoke native methods so your Java program doesn't have to. In this manner, the Java API's class files provide a Java program with a standard, platform-independent interface to the underlying host. To the Java program, the Java API looks the same and behaves predictably no matter what platform happens to be underneath. Precisely because the Java virtual machine and Java API are implemented specifically for each particular host platform, Java programs themselves can be platform independent. 

![Platform Independence](http://www.artima.com/insidejvm/ed2/images/fig1-6.gif "Platform Independent")

The Java API is geared towards platform independence and security. For example, Abstract Windows Toolkit (AWT) and Swing are libaries that help you acheive platform independence in UI because the UIs built in these works on all the host operating systems. The look and feel can adapt to the host system but the UI code itself works everywhere. Similary, each API method performs a security check before performing any harmful operation like writing to disk. 

###Java Programming Language:
As a whole, Java technology leans heavily in the direction of networks, but the Java programming language is quite general-purpose. The Java language allows you to write programs that take advantage of many software technologies:

    object-orientation
    multi-threading
    structured error-handling
    garbage collection
    dynamic linking
    dynamic extension 

- Platform independence of Java allows Sys admins to easily update programs across network of different host OS.

    In addition, the emerging proliferation of network-enabled embedded devices represents another environment in which Java's platform independence is useful. In the workplace, for example, various kinds of embedded devices, such as printers, scanners, and fax machines, are typically connected to the internal network. Network-connected embedded devices have also appeared in consumer domains, such as the home and car. In the embedded world, Java's platform independence can also help simplify system administration. Jini technology, which aims to bring plug and play to the network, simplifies the task of administering a dynamic environment of network-connected embedded devices for both consumers at home and systems administrators at work. Once a device is plugged into the network, it can access other devices attached to the network, and other devices can access it. To achieve this ease of connectivity, Jini-enabled devices exchange objects across the network, a technique that would be impossible without Java's support for platform independence. 
- Java can reduce the cost and time required to develop and deploy applications on multiple platforms.
- But perhaps most significantly for developers, the fact that Java code can run unchanged on multiple platforms gives the network a homogeneous execution environment that enables new kinds of distributed systems built around network-mobile objects. APIs such as object serialization, RMI (Remote Method Invocation), and Jini take advantage of this underlying capability to bring object-oriented programming out of the virtual machine and onto the network.
