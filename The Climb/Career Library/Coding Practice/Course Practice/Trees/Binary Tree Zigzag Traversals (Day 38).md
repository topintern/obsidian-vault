---
kind: "coding-problem"
title: "Binary Tree Zigzag Traversals (Day 38)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/BinaryTreeZigzagTraversals.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Binary Tree Zigzag Traversals (Day 38)

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

> [!example]- Reference 1 · BinaryTreeZigzagTraversals.txt
> ```java
> import java.util.*;
>
> /*
> Problem: Write a program to display Zigzag order traversal of a given n nodes tree.
>
> 		       	  1
> 		       /	 \  
> 		      /        \
> 		     /   	      \
> 		    2      	      3
> 		  /   \    	 		 /    \
> 		 4     5  	     6       7
> 	    / \   	/ \  		  / \     / \
>        8  9  10 11  12 13 14 15
>  
> Sample Input:15
> 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
>
> Sample Output:
> 1 3 2 4 5 6 7 15 14 13 12 11 10 9 8
>
> */
> // MyBinaryTreeNode Class containing left and right child of current node and data value
> class MyBinaryTreeNode5 {
>
> 	public int data;
> 	public MyBinaryTreeNode5 left;
> 	public MyBinaryTreeNode5 right;
>
> 	public MyBinaryTreeNode5(int data) {
> 		this.data = data;
> 		left = null;
> 		right = null;
> 	}
>
> 	public int getData() {
> 		return data;
> 	}
>
> 	public void setData(int data) {
> 		this.data = data;
> 	}
>
> 	public MyBinaryTreeNode5 getLeft() {
> 		return left;
> 	}
>
> 	public void setLeft(MyBinaryTreeNode5 left) {
> 		this.left = left;
> 	}
>
> 	public MyBinaryTreeNode5 getRight() {
> 		return right;
> 	}
>
> 	public void setRight(MyBinaryTreeNode5 right) {
> 		this.right = right;
> 	}
>
> }
>
> class BinaryTree66 {
>
> 	// Root of BinaryTree
> 	MyBinaryTreeNode5 root;
>
> 	
> 		// Function to insert nodes in level order
> 		public MyBinaryTreeNode5 insertLevelOrder(int[] arr, MyBinaryTreeNode5 root, int i) {
>
> 			// Base case for recursion
> 			if (i < arr.length) {
>
> 				if (arr[i] == -1)
> 					return null;
>
> 				MyBinaryTreeNode5 temp = new MyBinaryTreeNode5(arr[i]);
> 				root = temp;
>
> 				// insert left child
> 				root.left = insertLevelOrder(arr, root.left, 2 * i + 1);
>
> 				// insert right child
> 				root.right = insertLevelOrder(arr, root.right, 2 * i + 2);
>
> 			}
> 			return root;
> 		}
>
> 		
> 		
> 	public void zigzagTreeOrder(MyBinaryTreeNode5 root) {
>
>
>
> 		// if null then return
> 		if (root == null) {
> 			return;
> 		}
>
> 		// declare two stacks
> 		Stack<MyBinaryTreeNode5> currentLevel = new Stack<>();
> 		Stack<MyBinaryTreeNode5> nextLevel = new Stack<>();
>
> 		// push the root
> 		currentLevel.push(root);
> 		boolean leftToRight = true;
>
> 		// check if stack is empty
> 		while (!currentLevel.isEmpty()) {
>
> 			// pop out of stack
> 			MyBinaryTreeNode5 node = currentLevel.pop();
>
> 			// print the data in it
> 			System.out.print(node.data + " ");
>
> 			// store data according to current
> 			// order.
> 			if (leftToRight) {
> 				if (node.getLeft() != null) {
> 					nextLevel.push(node.getLeft());
> 				}
>
> 				if (node.getRight() != null) {
> 					nextLevel.push(node.getRight());
> 				}
> 			} else {
> 				if (node.getRight() != null) {
> 					nextLevel.push(node.getRight());
> 				}
>
> 				if (node.getLeft() != null) {
> 					nextLevel.push(node.getLeft());
> 				}
> 			}
>
> 			if (currentLevel.isEmpty()) {
> 				leftToRight = !leftToRight;
> 				Stack<MyBinaryTreeNode5> temp = currentLevel;
> 				currentLevel = nextLevel;
> 				nextLevel = temp;
> 			}
> 		}
> 	}
>
> }// end of BinaryTree
>
> public class BinaryTreeZigzagTraversals {
>
> 	public static void main(String args[]) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		int numOfNodes = sc.nextInt();
> 		BinaryTree66 bt = new BinaryTree66();
> 		int arr[] = new int[numOfNodes];
> 		for (int i = 0; i < numOfNodes; i++)
> 			arr[i] = sc.nextInt();
> 		bt.root = new MyBinaryTreeNode5(arr[0]);
> 		bt.root = bt.insertLevelOrder(arr, bt.root, 0);
> 		bt.zigzagTreeOrder(bt.root);
>
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/BinaryTreeZigzagTraversals.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/BinaryTreeZigzagTraversals.txt
