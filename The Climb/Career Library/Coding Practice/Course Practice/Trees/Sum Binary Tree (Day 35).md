---
kind: "coding-problem"
title: "Sum Binary Tree (Day 35)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/SumBinaryTree.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sum Binary Tree (Day 35)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a binary tree and a sum, determine if the tree has a root-to-leaf 
path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

Example:
Sample input: 5 4 8 11 13 4 7 2 -1 -1 -1 1
22

output :
true

Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1


return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

====TestCases=======
case =1
input =5 4 8 11 13 4 7 2 -1 -1 -1 1
22
output =true

case =2
input =4 8 11 4 7 2 -1 -1 -1 1
50
output =false

case =3
input =15 4 18 11 13 4 7 2 -1 -1 -1 1
42
output =false

case =4
input =4 8 4 7 2 -1 -1 -1 1
33
output =false

case =5
input =15 4 18 11 13 4 7 2 -1 -1 -1 1
32
output =true

case =6
input =4 18 11 13 4 7 2 -1 -1 -1 1
35
output =true

case =7
input =8 9 2 3 11 12 14 7 15 -1 13 -1 17 1 -1 
41
output =true

case =8
input =8 9 2 3 11 12 14 7 15 -1 13 -1 17 1 -1 
40
output =false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SumBinaryTree.java
> ```java
> /*
>  * Given a binary tree and a sum, determine if the tree has a root-to-leaf 
>  * path such that adding up all the values along the path equals the given sum.
>
> Note: A leaf is a node with no children.
>
> Example:
> Sample input: 5 4 8 11 13 4 7 2 -1 -1 -1 1
> 22
>
> output :
> true
>
> Given the below binary tree and sum = 22,
>
>       5
>      / \
>     4   8
>    /   / \
>   11  13  4
>  /  \      \
> 7    2      1
>
>
> return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
>
> ====TestCases=======
> case =1
> input =5 4 8 11 13 4 7 2 -1 -1 -1 1
> 22
> output =true
>
> case =2
> input =4 8 11 4 7 2 -1 -1 -1 1
> 50
> output =false
>
> case =3
> input =15 4 18 11 13 4 7 2 -1 -1 -1 1
> 42
> output =false
>
> case =4
> input =4 8 4 7 2 -1 -1 -1 1
> 33
> output =false
>
> case =5
> input =15 4 18 11 13 4 7 2 -1 -1 -1 1
> 32
> output =true
>
> case =6
> input =4 18 11 13 4 7 2 -1 -1 -1 1
> 35
> output =true
>
> case =7
> input =8 9 2 3 11 12 14 7 15 -1 13 -1 17 1 -1 
> 41
> output =true
>
> case =8
> input =8 9 2 3 11 12 14 7 15 -1 13 -1 17 1 -1 
> 40
> output =false
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.LinkedList;
> import java.util.Queue;
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
>
>
> class BinaryTree {
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
> 	/* Has Path Sum */
> 	public boolean hasPathSum(TreeNode root, int sum) {
> 	    if (root == null)
> 	      return false;
>
> 	    sum -= root.data;
> 	    if ((root.left == null) && (root.right == null))
> 	      return (sum == 0);
> 	    return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
> 	  }
> 	
> 	
> 		  
> }
>
> public class SumBinaryTree {
>
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 	    BinaryTree bt=new BinaryTree();
> 		
> 		String str = br.readLine();
> 		String[] numbers = str.split(" ");
> 		int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
>
> 		bt.root = new TreeNode(arr[0]);
> 		bt.root = bt.insertLevelOrder(arr, bt.root, 0);
> 		int sum=Integer.parseInt(br.readLine());
> 		System.out.println(bt.hasPathSum(bt.root,sum));
> 		}
> 	
> 	  
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2035%20Solutions/SumBinaryTree.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/SumBinaryTree.java
