---
kind: "coding-problem"
title: "Reverse KNodes (Day 9)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/ReverseKNodes.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reverse KNodes (Day 9)

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

> [!example]- Reference 1 · ReverseKNodes.java
> ```java
> import java.util.Scanner;
>
> /*
>  * For a given K value (K > 0), Reverse a Linked List in groups of size K.
>  * 
>  
> Sample Input : 
> 10 20 30 40 50 60 -1
> 3
>
> Sample Output : 
> 30 20 10 60 50 40
>     
>  * 
>  * 
>  */
>  
> class MyListNode {
> 	public MyListNode next;
> 	public int data;
>
> 	// Creates an empty node.
> 	public MyListNode() {
> 		next = null;
> 		data = Integer.MIN_VALUE;
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
> 			return "NULL";
> 		}
> 		result = result + head.getData();
> 		MyListNode temp = head.getNext();
> 		while (temp != null) {
> 			result = result + " " + temp.getData();
> 			temp = temp.getNext();
> 		}
> 		
> 		return result;
> 	}
>
> 	// Return the current length of the list.
> 	public int length() {
> 		return length;
> 	}
>
> }
>
> public class ReverseKNodes{
>
>     public static MyListNode reverseKNodes(MyListNode head, int k){
>     	MyListNode current = head;
>     	MyListNode next = null;
>     	MyListNode prev = null;
>         int count = k;
>
>         //Reverse K nodes
>         while (current != null && count > 0) {
>             next = current.getNext();
>             current.setNext(prev);
>             prev = current;
>             current = next;
>             count--;
>         }
>
>         //Now next points to K+1 th node, returns the pointer to the head node
>         if (next != null) {
>             head.setNext(reverseKNodes(next, k));
>         }
>         //return head node
>         return prev;
>     }
>
>
>     
>     
>     public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		int tempData = -1;
>
> 		// create a linked list
> 		MyLinkedList list = new MyLinkedList();
>
> 		// add nodes one by one till you find end of the character
> 		while ((tempData = sc.nextInt()) != -1) {
> 			// add nodes to the linked list
> 			list.insertAtEnd(new MyListNode(tempData));
> 		}
> 		
> 		int k=sc.nextInt();
>
> 		
> 		list.head = reverseKNodes(list.head,k);
> 		System.out.println(list.toString());
>
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%209%20Solutions/ReverseKNodes.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/ReverseKNodes.java
