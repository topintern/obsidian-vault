---
kind: "coding-problem"
title: "Min Stack Test (Day 11)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/MinStackTest.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Min Stack Test (Day 11)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
 

Example:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.


### Sample Input

push 20
push 15
pop
push 44
push 80
getmin


### Sample Output 

20



### Sample Input

push 40
push 30
push 85
push 64
pop
pop
top


### Sample Output 

30

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MinStackTest.java
> ```java
> /*
>  * 
> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
>
> push(x) -- Push element x onto stack.
> pop() -- Removes the element on top of the stack.
> top() -- Get the top element.
> getMin() -- Retrieve the minimum element in the stack.
>  
>
> Example:
>
> MinStack minStack = new MinStack();
> minStack.push(-2);
> minStack.push(0);
> minStack.push(-3);
> minStack.getMin();   --> Returns -3.
> minStack.pop();
> minStack.top();      --> Returns 0.
> minStack.getMin();   --> Returns -2.
>
> Sample Input:
> push 20
> push 15
> pop
> push 44
> push 80
> getmin
>
> Sample Output :
> 20
>
>
> Sample Input:
> push 40
> push 30
> push 85
> push 64
> pop
> pop
> top
>
> Sample Output :
> 30
>
>
>  */
>
> package Elite2020;
>
> import java.io.IOException;
> import java.util.*;
>
> class MinStack{
> private Node head;
>     
>     public void push(int x) {
>         if(head == null) 
>             head = new Node(x, x);
>         else 
>             head = new Node(x, Math.min(x, head.min), head);
>     }
>
>     public void pop() {
>         head = head.next;
>     }
>
>     public int top() {
>         return head.val;
>     }
>
>     public int getMin() {
>         return head.min;
>     }
>     
>     private class Node {
>         int val;
>         int min;
>         Node next;
>         
>         private Node(int val, int min) {
>             this(val, min, null);
>         }
>         
>         private Node(int val, int min, Node next) {
>             this.val = val;
>             this.min = min;
>             this.next = next;
>         }
>     }
> }
>
> /* class MinStack {
> 	
> 	    int min = Integer.MAX_VALUE;
> 	    Stack<Integer> stack = new Stack<Integer>();
> 	    public void push(int x) {
> 	        // only push the old minimum value when the current 
> 	        // minimum value changes after pushing the new value x
> 	        if(x <= min){          
> 	            stack.push(min);
> 	            min=x;
> 	        }
> 	        stack.push(x);
> 	    }
>
> 	    public void pop() {
> 	        // if pop operation could result in the changing of the current minimum value, 
> 	        // pop twice and change the current minimum value to the last minimum value.
> 	        if(stack.pop() == min) min=stack.pop();
> 	    }
>
> 	    public int top() {
> 	        return stack.peek();
> 	    }
>
> 	    public int getMin() {
> 	        return min;
> 	    }
> 	
>
> }*/
>
> class MinStackTest{
> 	 public static void main(String args[] ) throws IOException {
>
> 	Scanner sc = new Scanner(System.in);
> 	MinStack minStack = new MinStack();
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
> 		case "getmin":
> 			System.out.println(minStack.getMin());
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

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2011%20Solutions/MinStackTest.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/MinStackTest.java
