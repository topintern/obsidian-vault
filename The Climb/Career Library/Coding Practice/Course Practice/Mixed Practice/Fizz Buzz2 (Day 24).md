---
kind: "coding-problem"
title: "Fizz Buzz2 (Day 24)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 24 Solutions/FizzBuzz2.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Fizz Buzz2 (Day 24)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FizzBuzz2.java
> ```java
> import java.util.function.IntConsumer; 
> import java.io.*;
> import java.util.Scanner;
>
>
>
> class One implements Runnable{
>      FizzBuzz2 common;
>      public One(FizzBuzz2 fb){
>          common=fb;
>      }
>      public void run() {
>          try{
>          common.fizz();
>          }
>          catch(Exception e){
>              
>          }
>      }
>  }
>  
>  class Two implements Runnable{
>      FizzBuzz2 common;
>      public Two(FizzBuzz2 fb){
>          common=fb;
>      }
>      public void run(){
>          try{
>          common.buzz();
>           }
>          catch(Exception e){
>              
>          }
>      }
>  }
>  
>  
>  class Three implements Runnable{
>      FizzBuzz2 common;
>      public Three(FizzBuzz2 fb){
>          common=fb;
>      }
>      public void run(){
>          try{
>          common.fizzbuzz();
>      }
>          catch(Exception e){
>              
>          }
>      }
>  }
>  
>  class Four implements Runnable{
>      FizzBuzz2 common;
>      public Four(FizzBuzz2 fb){
>          common=fb;
>      }
>      public void run(){
>          try{
>          common.number();
>          }
>          catch(Exception e){
>              
>          }
>      }
>  }
>
>
>
> class FizzBuzz2 {
>     int count,n=1;
>   public FizzBuzz2(int n) { 
>       count=n;
>   }               // constructor
>   public synchronized void fizz() throws InterruptedException{
>       
>       while(n<=count){
>           if(n%3==0 && n%5!=0){
>               System.out.println("fizz");
>                n=n+1;
>               notifyAll();
>           }
>           else{
>               
>               wait();
>           }
>       }
>       
>   }    
>   
>    public synchronized void buzz() throws InterruptedException{
>       
>       while(n<=count){
>           if(n%5==0 && n%3!=0){
>               System.out.println("buzz");
>                n=n+1;
>               notifyAll();
>           }
>           else{
>               wait();
>           }
>       }
>       
>   }   
>   
>   
>    public synchronized void fizzbuzz() throws InterruptedException {
>       
>       while(n<=count){
>           if(n%5==0 && n%3==0){
>               System.out.println("fizzbuzz");
>                n=n+1;
>               notifyAll();
>           }
>           else{
>               wait();
>           }
>       }
>       
>   }  
>   
>    public synchronized void number() throws InterruptedException {
>       
>       while(n<=count){
>           if(n%5!=0 && n%3!=0){
>               System.out.println(n);
>                n=n+1;
>               notifyAll();
>           }
>           else{
>               wait();
>           }
>       }
>       
>   } 
>   
>  
>   
>   	public static void main(String[] args) throws IOException {
>     	Scanner sc=new Scanner(System.in);
>     	int n=sc.nextInt();
>     	FizzBuzz2 f= new FizzBuzz2(n);
>     	One o=new One(f);
>     	Two t=new Two(f);
>     	Three th=new Three(f);
>     	Four fo=new Four(f);
>     	Thread t1=new Thread(o);
>     	Thread t2=new Thread(t);
>     	Thread t3=new Thread(th);
>     	Thread t4=new Thread(fo);
>     	t1.start();
>     	t2.start();
>     	t3.start();
>     	t4.start();
>     	
>     	
>     }
>     
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2024%20Solutions/FizzBuzz2.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 24 Solutions/FizzBuzz2.java
