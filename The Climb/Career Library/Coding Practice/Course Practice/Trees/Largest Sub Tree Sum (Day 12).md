---
kind: "coding-problem"
title: "Largest Sub Tree Sum (Day 12)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/LargestSubTreeSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Largest Sub Tree Sum (Day 12)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Problem: Given a binary tree, find subtree with maximum sum in tree.


	      1
            /   \
           2      3
          / \    / \
         4   5  6   7
         
Sample Input 1:       
1 2 3 4 5 6 7

Sample Output 1: 
28

Explanation 1:
As all the tree elements are positive,
the largest subtree sum is equal to
sum of all tree elements.


              1
            /    \
          -2      3
          / \    /  \
         4   5  -6   2
 
Sample Input 2:
1 -2 3 4 5 -6 2


Sample Output 2:
7

Explanation 2:
Subtree with largest sum is : -2
                             /  \ 
                            4    5
Also, entire tree sum is also 7.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LargestSubTreeSum.java
> ```java
> /*
> Problem: Given a binary tree, find subtree with maximum sum in tree.
>
>
> 	      1
>             /   \
>            2      3
>           / \    / \
>          4   5  6   7
>          
> Sample Input 1:       
> 1 2 3 4 5 6 7
>
> Sample Output 1: 
> 28
>
> Explanation 1:
> As all the tree elements are positive,
> the largest subtree sum is equal to
> sum of all tree elements.
>
>
>               1
>             /    \
>           -2      3
>           / \    /  \
>          4   5  -6   2
>  
> Sample Input 2:
> 1 -2 3 4 5 -6 2
>
>
> Sample Output 2:
> 7
>
> Explanation 2:
> Subtree with largest sum is : -2
>                              /  \ 
>                             4    5
> Also, entire tree sum is also 7.
>
> */
>
> import java.util.Scanner;
>
> class MyBinaryTreeNode { 
>
> 	public int data;	
> 	public MyBinaryTreeNode left;
> 	public MyBinaryTreeNode right;
> 	
> 	public MyBinaryTreeNode(int data){
> 		this.data = data;
> 		left = null;
> 		right = null;
> 	}
> 	public int getData() {
> 		return data;
> 	}
> 	public void setData(int data) {
> 		this.data = data;
> 	}
> 	public MyBinaryTreeNode getLeft() {
> 		return left;
> 	}
> 	public void setLeft(MyBinaryTreeNode left) {
> 		this.left = left;
> 	}
> 	public MyBinaryTreeNode getRight() {
> 		return right;
> 	}
> 	public void setRight(MyBinaryTreeNode right) {
> 		this.right = right;
> 	}
>
> 	
> } 
>
> class BinaryTree{
>     
> 	// Root of BinaryTree 
> 	MyBinaryTreeNode root;
> 	
> 	static class INT 
> 	{ 
> 		int v; 
> 		INT(int a) 
> 		{ 
> 			v = a; 
> 		} 
> 	} 
> 	
> 	// Helper function to find largest 
> 	// subtree sum recursively. 
> 	int findLargestSubtreeSumUtil(MyBinaryTreeNode root, INT ans) 
> 	{ 
> 		// If current node is null then 
> 		// return 0 to parent node. 
> 		if (root == null)	 
> 			return 0; 
> 		
> 		// Subtree sum rooted 
> 		// at current node. 
> 		int currSum = root.getData() + 
> 		findLargestSubtreeSumUtil(root.left, ans) + 
> 		findLargestSubtreeSumUtil(root.right, ans); 
>
> 		// Update answer if current subtree 
> 		// sum is greater than answer so far. 
> 		ans.v = Math.max(ans.v, currSum); 
>
> 		// Return current subtree 
> 		// sum to its parent node. 
> 		return currSum; 
> 	} 
> 	
> 	public int findLargestSubtreeSum(MyBinaryTreeNode root){
> 		// If tree does not exist, 
> 		// then answer is 0. 
> 		if (root == null)	 
> 			return 0; 
> 		
> 		// Variable to store 
> 		// maximum subtree sum. 
> 		INT ans = new INT(-9999999); 
>
> 		// Call to recursive function 
> 		// to find maximum subtree sum. 
> 		findLargestSubtreeSumUtil(root, ans); 
>
> 		return ans.v; 
> 	}
> 	
> 	
> }
> public class LargestSubTreeSum {
>
> 	
> 	public static void main(String args[]) 
> 	{ 
> 		BinaryTree tree = new BinaryTree(); 
> 		
> 		Scanner sc = new Scanner(System.in);
> 		
> 		
> 		//creating a binary tree
> 		tree.root = new MyBinaryTreeNode(sc.nextInt()); 
> 		tree.root.setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.setRight(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getLeft().setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getLeft().setRight(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getRight().setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getRight().setRight(new MyBinaryTreeNode(sc.nextInt())); 
>
> 		System.out.println(tree.findLargestSubtreeSum(tree.root)); 
>
> 	}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2012%20Solutions/LargestSubTreeSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/LargestSubTreeSum.java
