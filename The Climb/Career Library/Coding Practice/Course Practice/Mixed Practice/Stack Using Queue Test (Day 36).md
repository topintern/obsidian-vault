---
kind: "coding-problem"
title: "Stack Using Queue Test (Day 36)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/StackUsingQueueTest.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Stack Using Queue Test (Day 36)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

mplement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.
Example:

MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
Notes:

You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

Note : can you do using one queue

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StackUsingQueueTest.java
> ```java
> /*
>  * 
>  mplement the following operations of a stack using queues.
>
> push(x) -- Push element x onto stack.
> pop() -- Removes the element on top of the stack.
> top() -- Get the top element.
> empty() -- Return whether the stack is empty.
> Example:
>
> MyStack stack = new MyStack();
>
> stack.push(1);
> stack.push(2);  
> stack.top();   // returns 2
> stack.pop();   // returns 2
> stack.empty(); // returns false
> Notes:
>
> You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
> Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
> You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).
>
> Note : can you do using one queue
>  */
>
> package Elite2020;
>
> import java.io.IOException;
> import java.util.LinkedList;
> import java.util.Queue;
> import java.util.Scanner;
>
>  class StackUsingQueue{
> 	
> Queue<Integer> queue;
>     
>     public StackUsingQueue()
>     {
>         this.queue=new LinkedList<Integer>();
>     }
>     
>     // Push element x onto stack.
>     public void push(int x) 
>     {
>        queue.add(x);
>        for(int i=0;i<queue.size()-1;i++)
>        {
>            queue.add(queue.poll());
>        }
>     }
>
>     // Removes the element on top of the stack.
>     public void pop() 
>     {
>         queue.poll();
>     }
>
>     // Get the top element.
>     public int top() 
>     {
>         return queue.peek();
>     }
>
>     // Return whether the stack is empty.
>     public boolean empty() 
>     {
>         return queue.isEmpty();
>     }
>     
>     
>
> }
>
>
> class StackUsingQueueTest{
> 	 public static void main(String args[] ) throws IOException {
>
> 	Scanner sc = new Scanner(System.in);
> 	StackUsingQueue minStack = new StackUsingQueue();
>
> 	while(true){
> 		
> 		String line = sc.nextLine();
> 		String[] choice=line.split(" ");
>
> 		switch(choice[0]){
> 		case "push": 
> 			minStack.push(Integer.parseInt(choice[1]));
> 		break;
> 		case "pop": 
> 			minStack.pop();
> 		break;
> 		case "top":
> 			System.out.println(minStack.top());
> 		break;
> 		case "empty":
> 			System.out.println(minStack.empty());
> 		break;
> 		case "exit":
> 			minStack.top();
> 		break;
> 		default:
> 			System.exit(0);
> 		}
> 	}
> 	 
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2036%20Solutions/StackUsingQueueTest.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/StackUsingQueueTest.java
