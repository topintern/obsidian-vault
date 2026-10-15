---
kind: "coding-problem"
title: "Delete Lesser Nodes (Day 40)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/DeleteLesserNodes.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Delete Lesser Nodes (Day 40)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a singly linked list, remove all the nodes which have a greater value on 
 right side.

Examples:
a) The list 12->15->10->11->5->6->2->3->NULL should be changed 
to 15->11->6->3->NULL. 
Note that 12, 10, 5 and 2 have been deleted because there is a greater 
value on the right side.

When we examine 12, we see that after 12 there is one node with value greater 
than 12 (i.e. 15), so we delete 12.
When we examine 15, we find no node after 15 that has value greater than 15 
so we keep this node.
When we go like this, we get 15->11->6->3

	Sample Input : 
    12 15 10 11 5 6 2 3 -1

	Sample Output : 
	15 11 6 3



========================================================================

case=1
input=12 15 10 11 5 6 2 3 1 -1
output=15 11 6 3 1

case=2
input=10 11 12 13 14 15 -1
output=15

case=3
input=15 14 13 12 11 -1
output=15 14 13 12 11

case=4
input=11 12 10 15 14 18 17 20 -1
output=20


case=5
input=10 9 17 12 15 14 13 12 11 -1
output=17 15 14 13 12 11

case=6
input=11 12 10 15 18 14 24 18 29 17 16 20 -1
output=29 20

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DeleteLesserNodes.java
> ```java
>
>
> /*
>  * Given a singly linked list, remove all the nodes which have a greater value on 
>  right side.
>
> Examples:
> a) The list 12->15->10->11->5->6->2->3->NULL should be changed 
> to 15->11->6->3->NULL. 
> Note that 12, 10, 5 and 2 have been deleted because there is a greater 
> value on the right side.
>
> When we examine 12, we see that after 12 there is one node with value greater 
> than 12 (i.e. 15), so we delete 12.
> When we examine 15, we find no node after 15 that has value greater than 15 
> so we keep this node.
> When we go like this, we get 15->11->6->3
>
> 	Sample Input : 
>     12 15 10 11 5 6 2 3 -1
>
> 	Sample Output : 
> 	15 11 6 3
>
>
>
> ========================================================================
>
> case=1
> input=12 15 10 11 5 6 2 3 1 -1
> output=15 11 6 3 1
>
> case=2
> input=10 11 12 13 14 15 -1
> output=15
>
> case=3
> input=15 14 13 12 11 -1
> output=15 14 13 12 11
>
> case=4
> input=11 12 10 15 14 18 17 20 -1
> output=20
>
>
> case=5
> input=10 9 17 12 15 14 13 12 11 -1
> output=17 15 14 13 12 11
>
> case=6
> input=11 12 10 15 18 14 24 18 29 17 16 20 -1
> output=29 20
>
>
>  * 
>  * 
>  */
>
> package Elite2020;
> import java.util.Scanner;
>
> class MyListNode20 {
> 	public MyListNode20 next;
> 	public int data;
>
> 	// Creates an empty node.
> 	public MyListNode20() {
> 		next = null;
> 		data = Integer.MIN_VALUE;
> 	}
>
> 	// Creates a node storing the specified data.
> 	public MyListNode20(int data) {
> 		next = null;
> 		this.data = data;
> 	}
>
> 	// Returns the node that follows this one.
> 	public MyListNode20 getNext() {
> 		return next;
> 	}
>
> 	// Sets the node that follows this one.
> 	public void setNext(MyListNode20 node) {
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
> class MyLinkedList20 {
> 	// This class has a default constructor:
> 	public MyLinkedList20() {
> 		length = 0;
> 	}
>
> 	// Length of the linked list
> 	private int length = 0;
> 	// This is the only field of the class. It holds the head of the list
> 	MyListNode20 head;
>
> 	// Insert a node at the end of the list
> 	public synchronized void insertAtEnd(MyListNode20 node) {
> 		if (head == null)
> 			head = node;
> 		else {
> 			MyListNode20 p, q;
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
> 		MyListNode20 temp = head.getNext();
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
> public class DeleteLesserNodes {
>
> 	// static ListNode head;
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		int tempData = -1;
>
> 		// create a linked list
> 		MyLinkedList20 list = new MyLinkedList20();
>
> 		// add nodes one by one till you find end of the character
> 		while ((tempData = sc.nextInt()) != -1) {
> 			// add nodes to the linked list
> 			list.insertAtEnd(new MyListNode20(tempData));
> 		}
>
> 		// create a linked list
> 		MyLinkedList20 lesserNodes = new MyLinkedList20();
>
> 		lesserNodes.head = delLesserNodes(list.head);
>
> 		System.out.println(lesserNodes.toString());
>
> 	}
>
> 	/*
> 	 * Deletes nodes which have a node with greater value node on left side
> 	 */
> 	static MyListNode20 delLesserNodes(MyListNode20 head) {
> 		/* 1.Reverse the linked list */
> 		MyListNode20 reversedHead = reverse(head);
>
> 		/*
> 		 * 2) In the reversed list, delete nodes which have a node with greater value
> 		 * node on left side. Note that head node is never deleted because it is the
> 		 * leftmost node.
> 		 */
> 		reversedHead = _delLesserNodes(reversedHead);
>
> 		/*
> 		 * 3) Reverse the linked list again to retain the original order
> 		 */
> 		return reverse(reversedHead);
> 	}
>
> 	/*
> 	 * Deletes nodes which have greater value node(s) on left side
> 	 */
> 	static MyListNode20 _delLesserNodes(MyListNode20 head) {
> 		MyListNode20 current = head;
>
> 		/* Initialise max */
> 		MyListNode20 maxnode = head;
> 		MyListNode20 temp;
>
> 		while (current != null && current.getNext() != null) {
> 			/*
> 			 * If current is smaller than max, then delete current
> 			 */
> 			if (current.getNext().getData() < maxnode.getData()) {
> 				temp = current.getNext();
> 				current.setNext(temp.getNext());
> 				temp = null;
> 			}
>
> 			/*
> 			 * If current is greater than max, then update max and move current
> 			 */
> 			else {
> 				current = current.getNext();
> 				maxnode = current;
> 			}
> 		}
> 		return head;
> 	}
>
> 	static MyListNode20 reverse(MyListNode20 head) {
> 		// initially Current is head
> 		MyListNode20 current = head;
> 		// initially previous & next are null
> 		MyListNode20 prev = null;
> 		MyListNode20 next = null;
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
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2040%20Solutions/DeleteLesserNodes.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/DeleteLesserNodes.java
