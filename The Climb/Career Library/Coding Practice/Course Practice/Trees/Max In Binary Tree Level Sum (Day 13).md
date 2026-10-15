---
kind: "coding-problem"
title: "Max In Binary Tree Level Sum (Day 13)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/MaxInBinaryTreeLevelSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max In Binary Tree Level Sum (Day 13)

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

> [!example]- Reference 1 · MaxInBinaryTreeLevelSum.java
> ```java
>
> import java.util.LinkedList;
> import java.util.Queue;
> import java.util.Scanner;
> /*
> Problem: Given a Binary Tree having positive and negative nodes, 
> the task is to find maximum sum level in it.
>
> 		      4
>                     /   \
>                    2    -5
>                   / \    /\
>                 -1   3 -2  6
>
> Sample Input :
> 7
> 4 2 -5 -1 3 -2 6
>
> Output: 
> 6
>
> Explanation :
> Sum of all nodes of 0'th level is 4
> Sum of all nodes of 1'th level is -3
> Sum of all nodes of 2'th level is 6
> Hence maximum sum is 6
>
> */
>
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
> 			if (arr[i] == -1)
> 				return null;
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
> 	public int maxSumInBinaryTreeLevel(MyBinaryTreeNode root) {
>
> 		if (root == null)
> 			return 0;
>
> 		// Initialize maxSum
> 		int maxSum = root.getData();
>
> 		// Do Level order traversal keeping track of number
> 		// of nodes at every level.
> 		Queue<MyBinaryTreeNode> q = new LinkedList<MyBinaryTreeNode>();
> 		q.offer(root);
> 		while (!q.isEmpty()) {
> 			// Get the size of queue for each level
> 			int count = q.size();
>
> 			// Iterate through all the nodes in the queue currently
> 			int sum = 0;
> 			while (count > 0) {
>
> 				MyBinaryTreeNode tmp = q.poll();
>
> 				// Add this node's value to current sum.
> 				sum = sum + tmp.getData();
>
> 				if (tmp != null) {
> 					if (tmp.getLeft() != null)
> 						q.offer(tmp.getLeft());
> 					if (tmp.right != null)
> 						q.offer(tmp.right);
> 				}
> 				count--;
> 			}
>
> 			// Update the maximum sum
> 			maxSum = Math.max(sum, maxSum);
> 		}
>
> 		return maxSum;
> 	}
>
> }
>
> public class MaxInBinaryTreeLevelOrder {
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
>
> 		System.out.println(bt.maxSumInBinaryTreeLevel(bt.root));
>
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day13%20Solutions/MaxInBinaryTreeLevelSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/MaxInBinaryTreeLevelSum.java
