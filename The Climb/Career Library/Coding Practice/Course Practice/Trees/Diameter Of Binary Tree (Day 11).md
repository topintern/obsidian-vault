---
kind: "coding-problem"
title: "Diameter Of Binary Tree (Day 11)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/DiameterOfBinaryTree.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Diameter Of Binary Tree (Day 11)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The diameter of a tree is the number of nodes on the longest path between two leaves in the tree.
write a program to find Diameter of a given Binary Tree .
Note:Construction of a complete binary tree is based on level order fashion.
 


### Sample Input :     

6
1 2 3 4 5 6


### Sample Output : 

5

Explanation: 4-2-1-3-6 or 5-2-1-3-6
			  1
			/   \
		  2     3
      	 / \   / 
      4     5  6

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DiameterOfBinaryTree.java
> ```java
> /*
> The diameter of a tree is the number of nodes on the longest path between two leaves in the tree.
> write a program to find Diameter of a given Binary Tree .
> Note:Construction of a complete binary tree is based on level order fashion.
>  
>
> Sample Input :     
> 6
> 1 2 3 4 5 6
>
> Sample Output : 
> 5
>
> Explanation: 4-2-1-3-6 or 5-2-1-3-6
> 			  1
> 			/   \
> 		  2     3
>       	 / \   / 
>       4     5  6
>
>  * 
>  */
>
> import java.util.Scanner;
>
> //MyBinaryTreeNode Class containing left and right child of current node and data value
> class MyBinaryTreeNode {
>
> 	public int data;
> 	public MyBinaryTreeNode left;
> 	public MyBinaryTreeNode right;
>
> 	public MyBinaryTreeNode(int data) {
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
> 	public MyBinaryTreeNode getLeft() {
> 		return left;
> 	}
>
> 	public void setLeft(MyBinaryTreeNode left) {
> 		this.left = left;
> 	}
>
> 	public MyBinaryTreeNode getRight() {
> 		return right;
> 	}
>
> 	public void setRight(MyBinaryTreeNode right) {
> 		this.right = right;
> 	}
>
> }
>
> class BinaryTree {
>
> 	// Root of BinaryTree
> 	MyBinaryTreeNode root;
>
> 	// Function to insert nodes in level order
> 	public MyBinaryTreeNode insertLevelOrder(int[] arr, MyBinaryTreeNode root, int i) {
> 		// Base case for recursion
> 		if (i < arr.length) {
> 			MyBinaryTreeNode temp = new MyBinaryTreeNode(arr[i]);
> 			root = temp;
>
> 			// insert left child
> 			root.left = insertLevelOrder(arr, root.left, 2 * i + 1);
>
> 			// insert right child
> 			root.right = insertLevelOrder(arr, root.right, 2 * i + 2);
> 		}
> 		return root;
> 	}
>
> 	static class A {
> 		int ans = Integer.MIN_VALUE;
> 	}
>
> 	/* Function to find height of a tree */
> 	int height(MyBinaryTreeNode root, A a) {
> 		if (root == null)
> 			return 0;
>
> 		int left_height = height(root.left, a);
>
> 		int right_height = height(root.right, a);
>
> 		// update the answer, because diameter of a
> 		// tree is nothing but maximum value of
> 		// (left_height + right_height + 1) for each node
> 		a.ans = Math.max(a.ans, 1 + left_height + right_height);
>
> 		return 1 + Math.max(left_height, right_height);
> 	}
>
> 	/*
> 	 * Computes the diameter of binary tree with given root.
> 	 */
> 	int diameter(MyBinaryTreeNode root) {
> 		if (root == null)
> 			return 0;
>
> 		// This will store the final answer
> 		A a = new A();
> 		int height_of_tree = height(root, a);
> 		return a.ans;
> 	}
>
> }
>
> public class DiameterOfBinaryTree {
>
> 	public static void main(String args[]) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		int numOfNodes = sc.nextInt();
> 		BinaryTree bt = new BinaryTree();
> 		int arr[] = new int[numOfNodes];
> 		for (int i = 0; i < numOfNodes; i++)
> 			arr[i] = sc.nextInt();
> 		bt.root = new MyBinaryTreeNode(arr[0]);
> 		bt.root = bt.insertLevelOrder(arr, bt.root, 0);
> 		int diameter = bt.diameter(bt.root);
> 		System.out.println(diameter);
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2011%20Solutions/DiameterOfBinaryTree.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/DiameterOfBinaryTree.java
