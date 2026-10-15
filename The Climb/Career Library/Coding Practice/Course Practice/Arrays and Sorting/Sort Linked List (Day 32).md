---
kind: "coding-problem"
title: "Sort Linked List (Day 32)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/SortLinkedList.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sort Linked List (Day 32)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a linked list of 0s, 1s and 2s, sort it.


### Sample Input : 

0 1 2 2 0 0 1 0 2 2 1 1 -1


### Sample Output : 

0 0 0 0 1 1 1 1 2 2 2 2

-------------TestCases----------------- 
case=1
input=0 1 2 2 0 0 1 0 2 1 1 -1
output=0 0 0 0 1 1 1 1 2 2 2


case=2
input=0 0 0 1 1 1 2 0 1 1 1 -1
output=0 0 0 0 1 1 1 1 1 1 2


case=3
input=0 2 1 0 1 0 1 2 2 -1
output=0 0 0 1 1 1 2 2 2

case=4
input=0 0 0 -1
output=0 0 0

case=5
input=2 2 0 1 0 1 1 -1
output=0 0 1 1 1 2 2


case=6
input=2 2 2 1 1 1 0 0 0 -1
output=0 0 0 1 1 1 2 2 2

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SortLinkedList.java
> ```java
> /*
>  * 
> Given a linked list of 0s, 1s and 2s, sort it.
>
> Sample Input : 
> 0 1 2 2 0 0 1 0 2 2 1 1 -1
>
> Sample Output : 
> 0 0 0 0 1 1 1 1 2 2 2 2
>
> -------------TestCases----------------- 
> case=1
> input=0 1 2 2 0 0 1 0 2 1 1 -1
> output=0 0 0 0 1 1 1 1 2 2 2
>
>
> case=2
> input=0 0 0 1 1 1 2 0 1 1 1 -1
> output=0 0 0 0 1 1 1 1 1 1 2
>
>
> case=3
> input=0 2 1 0 1 0 1 2 2 -1
> output=0 0 0 1 1 1 2 2 2
>
> case=4
> input=0 0 0 -1
> output=0 0 0
>
> case=5
> input=2 2 0 1 0 1 1 -1
> output=0 0 1 1 1 2 2
>
>
> case=6
> input=2 2 2 1 1 1 0 0 0 -1
> output=0 0 0 1 1 1 2 2 2
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
> 	public void setData(int elem) {
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
> public class SortLinkedList {
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
> 		// create a linked list
> 		MyLinkedList sortedList = new MyLinkedList();
>
> 		sortedList.head = sortLinkedList(list.head);
>
> 		System.out.println(sortedList.toString());
>
> 	}
>
> 	static MyListNode sortLinkedList(MyListNode head) {
> 		// initialise count of 0 1 and 2 as 0
> 		int count[] = { 0, 0, 0 };
>
> 		MyListNode current = head;
>
> 		/* count total number of '0', '1' and '2' */
> 		while (current != null) {
> 			count[current.getData()]++;
> 			current = current.getNext();
> 		}
>
> 		int i = 0;
> 		current = head;
>
> 		/*
> 		 * Let say count[0] = n1, count[1] = n2 and count[2] = n3 now start traversing
> 		 * list from head node, 1) fill the list with 0, till n1 > 0 2) fill the list
> 		 * with 1, till n2 > 0 3) fill the list with 2, till n3 > 0
> 		 */
> 		while (current != null) {
> 			if (count[i] == 0)
> 				i++;
> 			else {
> 				current.setData(i);
> 				--count[i];
> 				current = current.getNext();
> 			}
> 		}
> 		return head;
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2032%20Solutions/SortLinkedList.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/SortLinkedList.java
