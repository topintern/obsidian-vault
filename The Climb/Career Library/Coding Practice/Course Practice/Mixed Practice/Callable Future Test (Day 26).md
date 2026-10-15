---
kind: "coding-problem"
title: "Callable Future Test (Day 26)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 26 Solutions/CallableFutureTest.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Callable Future Test (Day 26)

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

> [!example]- Reference 1 · CallableFutureTest.java
> ```java
>
> import java.io.BufferedReader;
> import java.io.File;
> import java.io.FileReader;
> import java.io.IOException;
> import java.util.ArrayList;
> import java.util.Collections;
> import java.util.Comparator;
> import java.util.List;
>
> import java.util.concurrent.Callable;
> import java.util.concurrent.ExecutorService;
> import java.util.concurrent.Executors;
> import java.util.concurrent.FutureTask;
>
>
> class Studentt 
> { 
>     int marks; 
>     String rollno; 
>   
>     // Constructor 
>     public Studentt(String rollno,int marks) 
>     { 
>         this.marks = marks; 
>         this.rollno = rollno; 
>         
>     } 
>   
>     // Used to print student details in main() 
>     public String toString() 
>     { 
>         return this.rollno+" "+this.marks;
>     } 
>  
> } 
>   
> class Sortbymarks implements Comparator<Studentt> 
> { 
>     // Used for sorting in ascending order of 
>     // marks 
>     public int compare(Studentt a, Studentt b) 
>     { 
>         return b.marks-a.marks; 
>     } 
> } 
>
>
> class ReadFile implements Callable {
>
> 	private String filename;
>
> 	public ReadFile(String filename) {
> 		this.filename = filename;
> 	}
>
> 	@Override
> 	public List call() throws Exception {
> 		return readUsingFileReader(filename);
> 	}
>
> 	private List readUsingFileReader(String fileName) throws IOException {
> 		File file = new File(fileName);
> 		FileReader fr = new FileReader(file);
> 		BufferedReader br = new BufferedReader(fr);
> 		String line;
> 		String[] stuinfo;
> 		List<Studentt> studentlist = new ArrayList<>();
> 		List<String> toplist = new ArrayList<>();
> 		while ((line = br.readLine()) != null) {
> 			 //System.out.println(line);
> 			 stuinfo = line.split(" ");
> 			 Studentt s = new Studentt(stuinfo[0],Integer.parseInt(stuinfo[1]));
> 			 studentlist.add(s);
> 		}
>         Collections.sort(studentlist, new Sortbymarks()); 
>         
>         for(int i = 0; i < 5; i++) {
>         	toplist.add(studentlist.get(i).rollno);
>         }
>
> 		br.close();
> 		fr.close();
> 		return toplist;
>
> 	}
>
> }
>
> public class CallableFutureTest {
> 	@SuppressWarnings("unchecked")
> 	public static void main(String[] args) throws Exception {
>
> 		// FutureTask is a concrete class that
> 		// implements both Runnable and Future
> 		FutureTask[] randomNumberTasks = new FutureTask[3];
>
> 		Callable callable1 = new ReadFile("maths.txt");
> 		Callable callable2 = new ReadFile("physics.txt");
> 		Callable callable3 = new ReadFile("chemistry.txt");
>
> 		// Create the FutureTask with Callable
> 		randomNumberTasks[0] = new FutureTask(callable1);
> 		randomNumberTasks[1] = new FutureTask(callable2);
> 		randomNumberTasks[2] = new FutureTask(callable3);
>
> 		// As it implements Runnable, create Thread
> 		// with FutureTask
> 		/*Thread t1 = new Thread(randomNumberTasks[0]);
> 		t1.start();
> 		Thread t2 = new Thread(randomNumberTasks[1]);
> 		t2.start();
> 		Thread t3 = new Thread(randomNumberTasks[2]);
> 		t3.start();*/
> 		
>         ExecutorService pool = Executors.newFixedThreadPool(3);   
>         
>         // passes the Task objects to the pool to execute (Step 3) 
>         pool.execute(randomNumberTasks[0]); 
>         pool.execute(randomNumberTasks[1]); 
>         pool.execute(randomNumberTasks[2]); 
>           
>         // pool shutdown ( Step 4) 
>         pool.shutdown();     
>
> 		// As it implements Future, we can call get()
>         List<String> l1 = (List<String>) randomNumberTasks[0].get();
>         List<String> l2 =  (List<String>) randomNumberTasks[1].get();
>         List<String> l3 = (List<String>) randomNumberTasks[2].get();
> 		//System.out.println(l1.toString());
> 		//System.out.println(l2.toString());
> 		//System.out.println(l3.toString());
> 		 l2.retainAll(l1);
> 		 l3.retainAll(l2);
> 		 System.out.println(l3);
> 		
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2026%20Solutions/CallableFutureTest.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 26 Solutions/CallableFutureTest.java
