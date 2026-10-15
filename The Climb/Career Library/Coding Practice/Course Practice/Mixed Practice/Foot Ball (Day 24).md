---
kind: "coding-problem"
title: "Foot Ball (Day 24)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 24 Solutions/FootBall.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Foot Ball (Day 24)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Suppose you are given the following code:

class FootBall {
  public void foot() {
    for (int i = 0; i < n; i++) {
      print("foot");
    }
  }

  public void ball() {
    for (int i = 0; i < n; i++) {
      print("ball");
    }
  }
}
The same instance of FootBall will be passed to two different threads. 
Thread A will call foot() while thread B will call ball(). 
Modify the given program to output "football" n times.

 

Example 1:

Input: n = 1
Output: "football"
Explanation: There are two threads being fired asynchronously. One of them calls foo(), while the other calls bar(). "foobar" is being output 1 time.
Example 2:

Input: n = 2
Output: "footballfootball"
Explanation: "football" is being output 2 times.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FootBall.java
> ```java
> /*
>  * 
>  Suppose you are given the following code:
>
> class FootBall {
>   public void foot() {
>     for (int i = 0; i < n; i++) {
>       print("foot");
>     }
>   }
>
>   public void ball() {
>     for (int i = 0; i < n; i++) {
>       print("ball");
>     }
>   }
> }
> The same instance of FootBall will be passed to two different threads. 
> Thread A will call foot() while thread B will call ball(). 
> Modify the given program to output "football" n times.
>
>  
>
> Example 1:
>
> Input: n = 1
> Output: "football"
> Explanation: There are two threads being fired asynchronously. One of them calls foo(), while the other calls bar(). "foobar" is being output 1 time.
> Example 2:
>
> Input: n = 2
> Output: "footballfootball"
> Explanation: "football" is being output 2 times.
>
>
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.Scanner;
> import java.util.concurrent.Semaphore;
> class FootBall implements Runnable{
>     private int n;
>     Semaphore s1 = new Semaphore(0);
>     Semaphore s2 = new Semaphore(1);
>
>     public FootBall(int n) {
>         this.n = n;
>     }
>     @Override
> 	public void run() {
>     	if("A".equals(Thread.currentThread().getName())) {
>     		try {
>     			foot(printFoot);
> 			} catch (InterruptedException e) {
> 				e.printStackTrace();
> 			}
>     	}
>     	if("B".equals(Thread.currentThread().getName())) {
>     		try {
>     			ball(printBall);
> 			} catch (InterruptedException e) {
> 				e.printStackTrace();
> 			}
>     	}
> 		
> 	}
>     
>     Runnable printFoot = new Runnable() {
>         public void run() {
>         	 System.out.print("foot");
>         	 s1.release();
>         }
>     };
>     
>     Runnable printBall = new Runnable() {
>         public void run() {
>         	 System.out.print("ball");
>         	 s2.release();
>         }
>     };
>     
>     public void foot(Runnable printFoot) throws InterruptedException {
>         for (int i = 0; i < n; i++) {
>             s2.acquire();
>             printFoot.run();
>         }
>     }
>     public void ball(Runnable printBall) throws InterruptedException {
>         for (int i = 0; i < n; i++) {
>         	s1.acquire();
>             printBall.run();
>         }
>     }
>     public static void main(String[] args) throws IOException {
>     	Scanner sc=new Scanner(System.in);
>     	int n=sc.nextInt();
>         FootBall fb = new FooBar(n);
>         Thread one = new Thread(fb,"A");
>         Thread two = new Thread(fb,"B");
>         one.start();
>         two.start();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2024%20Solutions/FootBall.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 24 Solutions/FootBall.java
