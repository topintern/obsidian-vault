---
kind: "coding-problem"
title: "Left View Of Binary Tree (Day 15)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/LeftViewOfBinaryTree.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Left View Of Binary Tree (Day 15)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a Binary Tree, print left view of it. 
Left view of a Binary Tree is set of nodes visible 
when tree is visited from left side.

Note: -1 represents "no node"


### Sample Input :     

6
1 2 3 4 5 -1 6 -1 8 9 10


### Sample Output : 

1 2 4 8


### Explanation: 

	    1
	  /   \
	 2     3
	/ \     \
	4  5    6
	\ / \
	8 9 10

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LeftViewOfBinaryTree.java
> ```java
>
> /*
> Given a Binary Tree, print left view of it. 
> Left view of a Binary Tree is set of nodes visible 
> when tree is visited from left side.
>
> Note: -1 represents "no node"
>
> Sample Input :     
> 6
> 1 2 3 4 5 -1 6 -1 8 9 10
>
> Sample Output : 
> 1 2 4 8
>
> Explanation: 
> 	    1
> 	  /   \
> 	 2     3
> 	/ \     \
> 	4  5    6
> 	\ / \
> 	8 9 10
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
>
> 		// Base case for recursion
> 		if (i < arr.length) {
>
> 			if (arr[i] == -1)
> 				return null;
>
> 			MyBinaryTreeNode temp = new MyBinaryTreeNode(arr[i]);
> 			root = temp;
>
> 			// insert left child
> 			root.left = insertLevelOrder(arr, root.left, 2 * i + 1);
>
> 			// insert right child
> 			root.right = insertLevelOrder(arr, root.right, 2 * i + 2);
>
> 		}
> 		return root;
> 	}
>
> 	static int max_level = 0;
>
> 	// recursive function to print left view
> 	void leftViewUtil(MyBinaryTreeNode node, int level) {
> 		// Base Case
> 		if (node == null)
> 			return;
>
> 		// If this is the first node of its level
> 		if (max_level < level) {
> 			System.out.print(" " + node.getData());
> 			max_level = level;
> 		}
>
> 		// Recur for left and right subtrees
> 		leftViewUtil(node.getLeft(), level + 1);
> 		leftViewUtil(node.getRight(), level + 1);
> 	}
>
> 	// A wrapper over leftViewUtil()
> 	void leftView(MyBinaryTreeNode root) {
> 		leftViewUtil(root, 1);
> 	}
>
> }
>
> public class LeftViewOfBinaryTree {
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
> 		bt.leftView(bt.root);
>
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2015%20Solutions/LeftViewOfBinaryTree.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/LeftViewOfBinaryTree.java
