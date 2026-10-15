---
kind: "coding-problem"
title: "Valid BST (Day 37)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/ValidBST.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Valid BST (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
 

Example 1:

    2
   / \
  1   3

Input:2 1 3
Output: true
Example 2:

    5
   / \
  1   4
     / \
    3   6

Input:5 1 4 -1 -1 3 6
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ValidBST.txt
> ```java
> /*
>  * 
>  Given a binary tree, determine if it is a valid binary search tree (BST).
>
> Assume a BST is defined as follows:
>
> The left subtree of a node contains only nodes with keys less than the node's key.
> The right subtree of a node contains only nodes with keys greater than the node's key.
> Both the left and right subtrees must also be binary search trees.
>  
>
> Example 1:
>
>     2
>    / \
>   1   3
>
> Input:2 1 3
> Output: true
> Example 2:
>
>     5
>    / \
>   1   4
>      / \
>     3   6
>
> Input:5 1 4 -1 -1 3 6
> Output: false
> Explanation: The root node's value is 5 but its right child's value is 4.
>
>
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.List;
> import java.util.Scanner;
>
> class TreeNode {
>
> 	public int data;
> 	public TreeNode left;
> 	public TreeNode right;
>
> 	public TreeNode(int data) {
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
> 	public TreeNode getLeft() {
> 		return left;
> 	}
>
> 	public void setLeft(TreeNode left) {
> 		this.left = left;
> 	}
>
> 	public TreeNode getRight() {
> 		return right;
> 	}
>
> 	public void setRight(TreeNode right) {
> 		this.right = right;
> 	}
>
> }
> class BinaryTree9 {
>
> 	// Root of BinaryTree
> 	TreeNode root;
>
> 	// Function to insert nodes in level order
> 	public TreeNode insertLevelOrder(int[] arr, TreeNode root, int i) {
> 		// Base case for recursion
> 		if (i < arr.length) {
> 			TreeNode temp = new TreeNode(arr[i]);
> 			root = temp;
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
> 	 public boolean isLeaf(TreeNode t) {
> 	        return t.left == null && t.right == null;
> 	    }
>
> 	    public void addLeaves(List<Integer> res, TreeNode root) {
> 	        if (isLeaf(root)) {
> 	            res.add(root.data);
> 	        } else {
> 	            if (root.left != null) {
> 	                addLeaves(res, root.left);
> 	            }
> 	            if (root.right != null) {
> 	                addLeaves(res, root.right);
> 	            }
> 	        }
> 	    }
> 	    // valid bst code
> 	    
> 	    public  boolean helper(TreeNode node, Integer lower, Integer upper) {
> 		    if (node == null) return true;
>
> 		    int val = node.data;
> 		    if (lower != null && val <= lower) return false;
> 		    if (upper != null && val >= upper) return false;
>
> 		    if (! helper(node.right, val, upper)) return false;
> 		    if (! helper(node.left, lower, val)) return false;
> 		    return true;
> 		  }
>
> 		  public  boolean isValidBST(TreeNode root) {
> 		    return helper(root, null, null);
> 		  }
> }
>
> public class ValidBST {
>
> 	
> 	  
> 	  public static void main(String args[]) throws IOException
> 	    { 
> 	    	 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 	 		String str = br.readLine();
> 	 		
> 	 		String[] numline = str.split(" ");
> 	 		int[] arr = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 	     
> 			BinaryTree9 bt = new BinaryTree9();
> 			bt.root = new TreeNode(arr[0]);
> 			bt.root = bt.insertLevelOrder(arr, bt.root, 0);
>
> 			System.out.println(bt.isValidBST(bt.root));
>
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/ValidBST.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/ValidBST.txt
