<strong>.NET</strong>

Firstly a programmer will choose a programming language that targets the Common Language Runtime (CLR). The more popular .NET programming languages that can be compiled to Microsoft Intermediate Language (MSIL) are C#, Visual Basic, F# and Visual C++ (which is an Integrated Development Environment that enables C++ to be compiled using the CLR, as opposed to traditional C++ which compiles straight to CPU instructions).

When you have completed coding your program the human-readable code will be compiled to Microsoft Intermediate Language (MSIL). MSIL is a CPU-independent set of human readable instructions that can later be converted to native code. But you may ask "Why compile to this intermediate code and not straight to CPU instructions?".

There are a couple of benefits to compiling to MSIL instead of straight to machine code.

Theoretically it makes .NET cross-platform by enabling the numerous programming languages to compile to one single intermediate format. If MSIL did not exist then each compiler would have to compile straight to native code on every platform the program is being run on, however with MSIL only the virtual machine itself needs to be rewritten for each platform it is being run on.

Secondly, by having a language-agnostic intermediary language the many high-level languages have the ability to reference assemblies written in other languages, because they all get compiled to the same intermediate language, they can work seamlessly together.

Because MSIL is managed by the CLR it has the benefit of features including (memory management and <a title="Garbage Collection" href="http://chrismepham.co.uk/blog/certification/ocajp/ocajp-revision-what-is-garbage-collection/">garbage collection</a>).

When a program is run for the first time (runtime), the CLR will use a CPU architecture-specific Just-in-time (JIT) compiler which will convert only the required methods and data types necessary into CPU instructions. It knows which MSIL code to compile because the JIT loader attaches a stub to the required data types. The stub is used to mark what needs to be compiled by the JIT. This prevents unnecessary compilation of the entire MSIL which will consume unnecessary processing power and slow down program execution time. Compiled MSIL is also stored in memory so that subsequent JIT compilation requests can go straight to the native code instead of having to be recompiled every time a call is made.

An alternative to the JIT compiler is the .NET Native Image Generator (Ngen) which performs "ahead-of-time" compilation, whereby it compiles the MSIL when the program is being installed on your system. It generates an image containing all of the CPU-specific native code, which can be read each time the program is run. This will speed up the execution of programs.

<strong> Java</strong>

The Java Virtual Machine(JVM) supports multiple language compilers. Apart from it's own language compiler (Java) some other commonly used compilers are Clojure, Groovy, Scala and JRuby.

To develop a Java program a developer must first install the Java Development Kit (JDK) which contains all of the necessary tools (including the JVM) for the development and compilation of human readable (.java) files into intermediate bytecode (.class) files. The JVM (also known as the Java Interpreter) then converts the class files into CPU readable instructions, allowing for the execution of the program in the Java Runtime Environment(JRE).

The Java bytecode is managed code that runs in the JRE. This enables it similar advantages to .NET's MSIL running in the CLR in that the JRE provides garbage collection, memory management and other features to enable the program to run efficiently and provide automated maintenance, allowing the developer to focus primarily on the development of the programs features.

In much the same way as .NET's CLR. It is only the JVM that needs to be adapted to run on different platforms and compile the Java bytecode into the different CPU architectures native code. The Java bytecode will run the same on all JVM's. Meaning all Java programs will look the same no matter what platform they are running on. This is why it is known as "Write once, run anywhere".

<strong>Comparison</strong>

.NET and Java have a very similar approach to the managed execution of programs. The .NET platform however is used only on the Microsoft platforms (which includes Windows OS and Windows Enterprise Servers), whereas Java's JRE runs on most operating systems, making it truly multi-platform.

Both include an intermediate language (IL), that enables developers to choose from a range of compilers, and both provide a large API for a programmer to use standardized components, leaving the programmer to focus more on the development of business logic rather than the fundamental services a program requires to run.

C# and Java both derive from C and C++. They are both object oriented languages and are type safe, and both are compiled to an IL that runs in a Virtual Machine (VM) that provides automatic garbage collection.

&nbsp;

&nbsp;
