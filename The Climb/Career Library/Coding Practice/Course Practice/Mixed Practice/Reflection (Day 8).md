---
kind: "coding-problem"
title: "Reflection (Day 8)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/Reflection.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reflection (Day 8)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Reflection in Java

Reflection is an API which is used to examine or modify the behavior of methods, classes, interfaces at runtime.

    The required classes for reflection are provided under java.lang.reflect package.
    Reflection gives us information about the class to which an object belongs and also the methods of that class which can be executed by using the object.
    Through reflection we can invoke methods at runtime irrespective of the access specifier used with them.

Reflection can be used to get information about –

    Class The getClass() method is used to get the name of the class to which an object belongs.
    Constructors The getConstructors() method is used to get the public constructors of the class to which an object belongs.
    Methods The getMethods() method is used to get the public methods of the class to which an objects belongs.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Reflection.java
> ```java
> /*
>
> Reflection in Java
>
> Reflection is an API which is used to examine or modify the behavior of methods, classes, interfaces at runtime.
>
>     The required classes for reflection are provided under java.lang.reflect package.
>     Reflection gives us information about the class to which an object belongs and also the methods of that class which can be executed by using the object.
>     Through reflection we can invoke methods at runtime irrespective of the access specifier used with them.
>
> Reflection can be used to get information about –
>
>     Class The getClass() method is used to get the name of the class to which an object belongs.
>     Constructors The getConstructors() method is used to get the public constructors of the class to which an object belongs.
>     Methods The getMethods() method is used to get the public methods of the class to which an objects belongs.
>
> */
>
>
>
> // A simple Java program to demonstrate the use of reflection 
> import java.lang.reflect.Method; 
> import java.lang.reflect.Field; 
> import java.lang.reflect.Constructor; 
>   
> // class whose object is to be created 
> class Test 
> { 
>     // creating a private field 
>     private String s; 
>   
>     // creating a public constructor 
>     public Test()  {  s = "constructor"; } 
>   
>     // Creating a public method with no arguments 
>     public void method1()  { 
>         System.out.println("The string is " + s); 
>     } 
>   
>     // Creating a public method with int as argument 
>     public void method2(int n)  { 
>         System.out.println("The number is " + n); 
>     } 
>   
>     // creating a private method 
>     private void method3() { 
>         System.out.println("Private method invoked"); 
>     } 
> } 
>   
> class Reflection 
> { 
>     public static void main(String args[]) throws Exception 
>     { 
>         // Creating object whose property is to be checked 
>         Test obj = new Test(); 
>   
>         // Creating class object from the object using 
>         // getclass method 
>         Class cls = obj.getClass(); 
>         System.out.println("The name of class is " + 
>                             cls.getName()); 
>   
>         // Getting the constructor of the class through the 
>         // object of the class 
>         Constructor constructor = cls.getConstructor(); 
>         System.out.println("The name of constructor is " + constructor.getName()); 
>   
>         System.out.println("The public methods of class are : "); 
>   
>         // Getting methods of the class through the object 
>         // of the class by using getMethods 
>         Method[] methods = cls.getMethods(); 
>   
>         // Printing method names 
>         for (Method method:methods) 
>             System.out.println(method.getName()); 
>   
>         // creates object of desired method by providing the 
>         // method name and parameter class as arguments to 
>         // the getDeclaredMethod 
>         Method methodcall1 = cls.getDeclaredMethod("method2", int.class); 
>   
>         // invokes the method at runtime 
>         methodcall1.invoke(obj, 19); 
>   
>         // creates object of the desired field by providing 
>         // the name of field as argument to the  
>         // getDeclaredField method 
>         Field field = cls.getDeclaredField("s"); 
>   
>         // allows the object to access the field irrespective 
>         // of the access specifier used with the field 
>         field.setAccessible(true); 
>   
>         // takes object and the new value to be assigned 
>         // to the field as arguments 
>         field.set(obj, "JAVA"); 
>   
>         // Creates object of desired method by providing the 
>         // method name as argument to the getDeclaredMethod 
>         Method methodcall2 = cls.getDeclaredMethod("method1"); 
>   
>         // invokes the method at runtime 
>         methodcall2.invoke(obj); 
>   
>         // Creates object of the desired method by providing 
>         // the name of method as argument to the  
>         // getDeclaredMethod method 
>         Method methodcall3 = cls.getDeclaredMethod("method3"); 
>   
>         // allows the object to access the method irrespective  
>         // of the access specifier used with the method 
>         methodcall3.setAccessible(true); 
>   
>         // invokes the method at runtime 
>         methodcall3.invoke(obj); 
>     } 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%208%20Solutions/Reflection.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/Reflection.java
