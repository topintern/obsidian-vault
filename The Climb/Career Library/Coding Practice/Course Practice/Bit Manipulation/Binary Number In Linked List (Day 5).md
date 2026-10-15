---
kind: "coding-problem"
title: "Binary Number In Linked List (Day 5)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/BinaryNumberInLinkedList.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Binary Number In Linked List (Day 5)

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

> [!example]- Reference 1 · BinaryNumberInLinkedList.java
> ```java
> package others;
>
> /*
>  * Problem: Binary number in linked list
>  * Given a singly linked list of 0s and 1s find its decimal equivalent. 
>  * 
>  * 
> 	Sample Input :
> 	3 
>     1 0 0
>
> 	Sample Output : 
> 	4
> 	
> 	Explanation:
> 	(100) base 2 = (4) base 10
> 	
>  * 
>  * 
>  */
> import java.util.Scanner;
>
> class MyListNode {
> 	public MyListNode next;
> 	public int data;
>
> 	// Creates an empty node.
> 	public MyListNode() {
> 		next = null;
> 		data = 0;
> 	}
>
> 	// Creates a node storing the specified data.
> 	public MyListNode(int data) {
> 		next = null;
> 		this.data = data;
> 	}
>
> 	// Returns the node that follows this one.
> 	public MyListNode getNext() {
> 		return next;
> 	}
>
> 	// Sets the node that follows this one.
> 	public void setNext(MyListNode node) {
> 		next = node;
> 	}
>
> 	// Returns the data stored in this node.
> 	public int getData() {
> 		return data;
> 	}
>
> 	// Sets the data stored in this node.
> 	public void setdata(int elem) {
> 		data = elem;
> 	}
>
> 	// Sets the data stored in this node.
> 	public String toString() {
> 		return Integer.toString(data);
> 	}
> }
>
> class MyLinkedList {
> 	// This class has a default constructor:
> 	public MyLinkedList() {
> 		length = 0;
> 	}
>
> 	// Length of the linked list
> 	private int length = 0;
> 	// This is the only field of the class. It holds the head of the list
> 	MyListNode head;
>
> 	// Insert a node at the end of the list
> 	public synchronized void insertAtEnd(MyListNode node) {
> 		if (head == null)
> 			head = node;
> 		else {
> 			MyListNode p, q;
> 			for (p = head; (q = p.getNext()) != null; p = q)
> 				;
> 			p.setNext(node);
> 		}
> 		length++;
> 	}
>
> 	// Return a string representation of this collection, in the form
> 	// "str1" "str2" ....
> 	public String toString() {
> 		String result = "";
> 		if (head == null) {
> 			return result + "";
> 		}
> 		result = result + head.getData();
> 		MyListNode temp = head.getNext();
> 		while (temp != null) {
> 			result = result + " " + temp.getData();
> 			temp = temp.getNext();
> 		}
> 		return result + "";
> 	}
>
> 	// Return the current length of the list.
> 	public int length() {
> 		return length;
> 	}
>
> }
>
> public class BinaryNumberInLinkedList {
>
> 	// static ListNode head;
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		int noOfElements = sc.nextInt();
>
> 		// create a linked list
> 		MyLinkedList list = new MyLinkedList();
> 		
> 		for(int i=0;i<noOfElements;i++)
> 			list.insertAtEnd(new MyListNode(sc.nextInt()));
>
> 		//System.out.println(list.toString());
>
> 		// call get decimal function
> 		System.out.println(getDecimalEquivalent(list.head));
>
> 	}
>
> 	
> 	public static int getDecimalEquivalent(MyListNode head) {
> 		int res=0;
> 		// initially Current is head
> 		MyListNode current = head;
> 		
> 		// Traverse linked list 
> 	    while (current != null) 
> 	    { 
> 	        // Multiply result by 2 and add current's data 
> 	        res = (res  << 1) + current.getData(); 
> 	  
> 	        // Move next 
> 	        current = current.getNext(); 
> 	    } 
> 		return res;
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%205%20Solutions/BinaryNumberInLinkedList.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/BinaryNumberInLinkedList.java
