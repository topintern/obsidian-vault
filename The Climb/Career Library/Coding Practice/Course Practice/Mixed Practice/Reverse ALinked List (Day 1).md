---
kind: "coding-problem"
title: "Reverse ALinked List (Day 1)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/ReverseALinkedList.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reverse ALinked List (Day 1)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Problem: Reverse	a singly linked list.

Sample Input and Output:

	Sample Input : 
    15 4 85 10 -1

	Sample Output : 
	Given Linked List
	15 4 85 10
	Reversed Linked List 
	10 85 4 15

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ReverseALinkedList.java
> ```java
> /*
>  * Problem: Reverse	a singly linked list.
>  * 
>  * Sample Input and Output:
>  * 
> 	Sample Input : 
>     15 4 85 10 -1
>
> 	Sample Output : 
> 	Given Linked List
> 	15 4 85 10
> 	Reversed Linked List 
> 	10 85 4 15
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
> public class ReverseALinkedList {
>
> 	// static ListNode head;
> 	public static void main(String[] args) {
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
> 		System.out.println("Given Linked List");
> 		System.out.println(list.toString());
>
> 		// call reverse list iterative function
> 		list.head = reverseListIterative(list.head);
> 		System.out.println("Reversed Linked List ");
> 		System.out.println(list.toString());
>
> 	}
>
> 	/*
> 	 * 
> 	 * 
> 	 * Algorithm for this method 
> 	 * ------------------------- 
> 	 * Initialize three pointers
> 	 * prev as NULL, current as head and next as NULL. Iterate trough the linked
> 	 * list. In loop, do following. 
> 	 * // Before changing next of current, 
> 	 * // store next node 
> 	 * next = current.getNext();
> 	 * 
> 	 * // Now change next of current 
> 	 * // This is where actual reversing happens
> 	 * current.setNext(prev);
> 	 * 
> 	 * // Move prev and current one step forward 
> 	 * prev = current 
> 	 * current = next
> 	 * 
> 	 * 
> 	 */
> 	public static MyListNode reverseListIterative(MyListNode head) {
> 		// initially Current is head
> 		MyListNode current = head;
> 		// initially previous & next are null
> 		MyListNode prev = null;
> 		MyListNode next = null;
>
> 		while (current != null) {
> 			// Save the next node
> 			next = current.getNext();
> 			// Make current node points to the previous
> 			current.setNext(prev);
> 			// update previous
> 			prev = current;
> 			// update current
> 			current = next;
> 		}
> 		return prev;
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%201/ReverseALinkedList.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/ReverseALinkedList.java
