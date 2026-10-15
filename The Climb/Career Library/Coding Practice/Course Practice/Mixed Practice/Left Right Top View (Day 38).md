---
kind: "coding-problem"
title: "Left Right Top View (Day 38)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/LeftRightTopView.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Left Right Top View (Day 38)

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

> [!example]- Reference 1 · LeftRightTopView.txt
> ```java
>
>
> import java.util.LinkedList;
> import java.util.Map.Entry;
>
> /*
> Given a Binary Tree, print Right view of it. 
> Right view of a Binary Tree is set of nodes visible when 
> tree is visited from Right side. 
>
> Note: -1 represents "no node"
>
> Sample Input :     
> 11
> 1 2 3 4 5 -1 6 -1 8 9 10
>
> Sample Output : 
> 1 2 4 8 
> 1 3 6 10 
> 4 2 1 3 6
>
> Explanation: 
>                  1
>                /   \
>               2     3
>              / \     \
>             4   5     6
>              \ / \
>              8 9 10
>              
> Left View :1 2 4 8
> Right View: 1 3 6 10
> Top View: 4 2 1 3 6
>           
>  * 
>  */
>
> import java.util.*;
>
> //MyBinaryTreeNode Class containing left and right child of current node and data value
> class MyBinaryTreeNode111 {
>
> 	public int data;
> 	public MyBinaryTreeNode111 left;
> 	public MyBinaryTreeNode111 right;
>
> 	public MyBinaryTreeNode111(int data) {
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
> 	public MyBinaryTreeNode111 getLeft() {
> 		return left;
> 	}
>
> 	public void setLeft(MyBinaryTreeNode111 left) {
> 		this.left = left;
> 	}
>
> 	public MyBinaryTreeNode111 getRight() {
> 		return right;
> 	}
>
> 	public void setRight(MyBinaryTreeNode111 right) {
> 		this.right = right;
> 	}
>
> }
>
> class BinaryTree1111 {
>
> 	// Root of BinaryTree
> 	MyBinaryTreeNode111 root;
>
> 	// Function to insert nodes in level order
> 	public MyBinaryTreeNode111 insertLevelOrder(int[] arr, MyBinaryTreeNode111 root, int i) {
>
> 		// Base case for recursion
> 		if (i < arr.length) {
>
> 			if (arr[i] == -1)
> 				return null;
>
> 			MyBinaryTreeNode111 temp = new MyBinaryTreeNode111(arr[i]);
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
> 	
> 	static int max_level = 0;
>
> 	
> 	// recursive function to print left view
> 			void leftViewUtil(MyBinaryTreeNode111 node, int level) {
> 				// Base Case
> 				if (node == null)
> 					return;
>
> 				// If this is the first node of its level
> 				if (max_level < level) {
> 					System.out.print(node.getData()+" ");
> 					max_level = level;
> 				}
>
> 				// Recur for left and right subtrees
> 				leftViewUtil(node.getLeft(), level + 1);
> 				leftViewUtil(node.getRight(), level + 1);
> 			}
>
> 			// A wrapper over leftViewUtil()
> 			void leftView(MyBinaryTreeNode111 root) {
> 				leftViewUtil(root, 1);
> 			}
> 			
> 			static int m_level = 0;
> 	
> 	// recursive function to print right view
> 		void rightViewUtil(MyBinaryTreeNode111 node, int level) {
> 			// Base Case
> 			if (node == null)
> 				return;
>
> 			// If this is the last Node of its level
> 			if (m_level < level) {
> 				System.out.print(node.data + " ");
> 				m_level = level;
> 			}
>
> 			// Recur for right subtree first, then left subtree
> 			rightViewUtil(node.right, level + 1);
> 			rightViewUtil(node.left, level + 1);
>
> 		}
>
> 		// A wrapper over rightViewUtil()
> 		void rightView(MyBinaryTreeNode111 root) {
> 			rightViewUtil(root, 1);
> 		}
> 		
> 		
> 		
> 		 // function should print the topView of 
> 	    // the binary tree 
> 	    public void TopView(MyBinaryTreeNode111 root) { 
> 	        class QueueObj { 
> 	        	MyBinaryTreeNode111 node; 
> 	            int hd; 
> 	  
> 	            QueueObj(MyBinaryTreeNode111 node, int hd) { 
> 	                this.node = node; 
> 	                this.hd = hd; 
> 	            } 
> 	        } 
> 	        Queue<QueueObj> q = new LinkedList<QueueObj>(); 
> 	        Map<Integer, MyBinaryTreeNode111> topViewMap = new TreeMap<Integer, MyBinaryTreeNode111>(); 
> 	  
> 	        if (root == null) { 
> 	            return; 
> 	        } else { 
> 	            q.add(new QueueObj(root, 0)); 
> 	        } 
> 	        // count function returns 1 if the container  
> 	        // contains an element whose key is equivalent  
> 	        // to hd, or returns zero otherwise. 
> 	        while (!q.isEmpty()) { 
> 	            QueueObj tmpNode = q.poll(); 
> 	            if (!topViewMap.containsKey(tmpNode.hd)) { 
> 	                topViewMap.put(tmpNode.hd, tmpNode.node); 
> 	            } 
> 	  
> 	            if (tmpNode.node.left != null) { 
> 	                q.add(new QueueObj(tmpNode.node.left, tmpNode.hd - 1)); 
> 	            } 
> 	            if (tmpNode.node.right != null) { 
> 	                q.add(new QueueObj(tmpNode.node.right, tmpNode.hd + 1)); 
> 	            } 
> 	  
> 	        } 
> 	        for (Entry<Integer, MyBinaryTreeNode111> entry : topViewMap.entrySet()) { 
> 	            System.out.print(entry.getValue().data+" "); 
> 	        } 
> }
> }
>  class LeftRightTopView {
>
> 	public static void main(String args[]) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		int numOfNodes = sc.nextInt();
> 		BinaryTree1111 bt = new BinaryTree1111();
> 		int arr[] = new int[numOfNodes];
> 		for (int i = 0; i < numOfNodes; i++)
> 			arr[i] = sc.nextInt();
> 		bt.root = new MyBinaryTreeNode111(arr[0]);
> 		bt.root = bt.insertLevelOrder(arr, bt.root, 0);
> 		bt.leftView(bt.root);
> 		System.out.println();
> 		bt.rightView(bt.root);
> 		System.out.println();
> 		bt.TopView(bt.root);
>
>
>
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/LeftRightTopView.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/LeftRightTopView.txt
