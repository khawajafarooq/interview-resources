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

Software based execution engines:

- Simple execution engine: That just inteprets the bytecode one at a time.
- Just in Time (JIT): In this scheme, the bytecodes of a method are compiled to native machine code the first time the method is invoked. The native machine code for the method is then cached, so it can be re-used the next time that same method is invoked.
- Adaptive optimizer: In this approach, the virtual machine starts by interpreting bytecodes, but monitors the activity of the running program and identifies the most heavily used areas of code. As the program runs, the virtual machine compiles to native and optimizes just these heavily used areas. The rest of the of code, which is not heavily used, remain as bytecodes which the virtual machine continues to interpret. This adaptive optimization approach enables a Java virtual machine to spend typically 80 to 90% of its time executing highly optimized native code, while requiring it to compile and optimize only the 10 to 20% of the code that really matters to performance.

Hardware based execution engine: 
On a Java virtual machine built on top of a chip that executes Java bytecodes natively, the execution engine is actually embedded in the chip. 

