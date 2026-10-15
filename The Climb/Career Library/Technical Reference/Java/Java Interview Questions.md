---
kind: "study-reference"
title: "Java Interview Questions"
collection: "Java"
topic: "Java"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/Angular/Java Interview Questions.docx"]
tags: ["career/library"]
source_status: "source-reference"
---

# Java Interview Questions

[[The Climb/Career Library/Career Library]]

**Java Interview Questions**

  **Is**** Java Platform ****Independent if**** then how?**

- Yes, Java is platform-independent due to its "Write Once, Run Anywhere" capability. Java code is compiled into bytecode by the Java compiler, and this bytecode can run on any machine that has a Java Virtual Machine (JVM), making Java platform-independent.

  **How**** is Java different from C++?**

- Java is platform-independent, while C++ is not.

- Java doesn't support multiple inheritance directly (uses interfaces), whereas C++ does.

- Java has built-in garbage collection; in C++, memory management is manual (using delete).

- Java doesn't use pointers, while C++ heavily relies on pointers.

  **What**** is Java 8?**

- Java 8 is a major release of the Java language that introduced several new features like Lambda expressions, the Stream API, default methods in interfaces, and the java.time package for better date and time manipulation.

  **What**** are the top Java Features?**

- Platform Independence

- Object-Oriented

- Multithreaded

- High Performance (using JIT)

- Robust and Secure

- Automatic Garbage Collection

- Dynamic and Portable

  **Tell**** us something about JIT compiler.**

- The Just-In-Time (JIT) compiler is a part of the JVM that improves performance by compiling bytecode into machine code at runtime, optimizing frequently used parts of the code.

  **How**** is an infinite loop declared in Java?**

- while(true) { } or for(;;) { }

  **What**** do you understand by an instance variable and a local variable?**

- Instance variables are declared inside a class but outside any method and are accessible to all non-static methods.

- Local variables are declared within a method and are only accessible within that method.

  **What**** is a ****ClassLoader****?**

- A ClassLoader in Java is part of the JVM responsible for loading class files into memory at runtime. It loads classes when they are needed for execution.

  **Can**** you tell the difference between ****equals()**** method and equality operator (****==****) in Java?**

- == compares references (memory addresses), while equals() compares the contents (logical equality) of two objects.

  **What**** are the default values assigned to variables and instances in Java?**

- Numeric types (byte, short, int, long, float, double) are assigned 0 or 0.0.

- char is assigned \u0000.

- Boolean is assigned false.

- Object references (including arrays) are assigned null.

  **Explain**** the use of the ****final**** keyword in variable, method, and class.**

- final variable: its value cannot be changed once initialized.

- final method: cannot be overridden by subclasses.

- final class: cannot be subclassed.

  **What**** are the differences between class and object?**

- A class is a blueprint or template that defines the structure and behavior (data and methods) of objects.

- An object is an instance of a class created at runtime, holding actual values.

  **What**** are the rules for creating a constructor?**

- The constructor must have the same name as the class.

- It must not have a return type, not even void.

- A constructor can be overloaded but cannot be inherited.

  **What**** is method overriding, and how does it work?**

- Method overriding occurs when a subclass provides its implementation for a method that is already defined in its superclass. The overridden method must have the same signature and return type.

  **What**** does it mean when an operator is overloaded?**

- Operator overloading allows operators to be used in user-defined types. However, Java does not support operator overloading like C++.

  **What**** is the use of ****finalize()****?**

- The finalize() method is called by the garbage collector before an object is reclaimed, allowing the object to clean up resources. It's rarely used now due to unpredictable behavior.

  **What**** is Garbage Collection (GC)?**

- Garbage Collection is the process of automatically reclaiming memory by identifying and disposing of objects that are no longer in use, helping prevent memory leaks.

  **What**** is an interface?**

- An interface in Java is a blueprint of a class that contains abstract methods (methods without a body). Classes implementing the interface must provide concrete implementations for these methods.

  **What**** are pure virtual functions?**

- In Java, pure virtual functions are equivalent to abstract methods in an interface or abstract class. They have no implementation and must be implemented by subclasses.

  **What**** are virtual functions?**

- In C++, virtual functions are methods that can be overridden in derived classes. In Java, all non-static methods are considered "virtual" by default, meaning they can be overridden.

  **What**** is exception handling?**

- Exception handling in Java involves using try, catch, and finally blocks to manage runtime errors and prevent application crashes by handling exceptional conditions.

  **How**** is an abstract class different from an interface?**

- An abstract class can have both abstract and concrete methods, while an interface can only have abstract methods (prior to Java 8). A class can extend only one abstract class but implement multiple interfaces.

  **What**** is a singleton design pattern, and how does it ensure the creation of only one instance?**

- The singleton pattern ensures only one instance of a class is created. This is achieved by making the constructor private and providing a static method that returns the instance.

  **What**** is the difference between ****throw**** and ****throws**** keywords in Java?**

- throw is used to explicitly throw an exception in a method.

- throws is used in the method signature to declare that a method might throw exceptions.

  **What**** do you understand by the term Vector in Java?**

- A Vector is a dynamic array that grows as needed. It's synchronized, meaning it's thread-safe, but this synchronization can make it slower than alternatives like ArrayList.

  **What**** is the difference between a program and a process?**

- A program is a set of instructions stored on disk (static). A process is an instance of a program being executed in memory (dynamic).

  **Write**** a Java program to create and throw custom exceptions.**

java

Copy code

class CustomException extends Exception {

    public CustomException(String message) {

        super(message);

    }

}

public class Main {

    public static void main(String[] args) {

        try {

            throw new CustomException("This is a custom exception");

        } catch (CustomException e) {

            System.out.println(e.getMessage());

        }

    }

}

  **What**** happens if there are multiple ****main**** methods inside one class in Java?**

- Only the main method with the correct signature (public static void main(String[] args)) will be executed. If other methods named main exist, they are treated like any other methods.

  **Are** **int array[]**** and ****int[] array**** different or the same?**

- Both declarations are the same and valid in Java. The difference is in the placement of square brackets.

  **Can** **this**** keyword be used to refer to static members?**

- No, this refers to the current instance of a class and cannot be used with static members because static members belong to the class, not instances.

  **What**** do you understand by the jagged array?**

- A jagged array is an array of arrays where each sub-array can have different lengths. It's a multidimensional array where the rows can have varying column sizes.

  **Will**** the ****finally**** block be executed if the code ****System.exit****(0)**** is written at the end of the ****try**** block?**

- No, the finally block will not be executed if System.exit(0) is called because it terminates the JVM.

  **What**** are the differences between ****StringBuffer**** and ****StringBuilder****?**

- Both are used to create mutable strings, but StringBuffer is synchronized (thread-safe), while StringBuilder is not, making StringBuilder faster in most single-threaded scenarios.

## Source provenance

- [Original DOCX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/Angular/Java%20Interview%20Questions.docx) · CODING RESOURCES/Lectures/Angular/Java Interview Questions.docx

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
