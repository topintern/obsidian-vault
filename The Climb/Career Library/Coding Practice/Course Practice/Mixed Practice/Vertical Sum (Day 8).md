---
kind: "coding-problem"
title: "Vertical Sum (Day 8)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/VerticalSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Vertical Sum (Day 8)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Problem:(Problem No.35 from Trees) Write a program to create a binary tree as shown below with 7 nodes and 
to find the vertical sum of the binary tree.


### Sample Input

1 2 3 4 5 6 7


### Sample Output

4 2 12 3 7 


### Explanation

       1
     /   \
   2      3
  / \    / \
 4   5  6   7

The tree has 5 vertical lines
Vertical-Line-1 has only one node 4 => vertical sum is 4
Vertical-Line-2: has only one node 2=> vertical sum is 2
Vertical-Line-3: has three nodes: 1,5,6 => vertical sum is 1+5+6 = 12
Vertical-Line-4: has only one node 3 => vertical sum is 3
Vertical-Line-5: has only one node 7 => vertical sum is 7

So expected output is 4, 2, 12, 3 and 7

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · VerticalSum.java
> ```java
> /*
>  * 
> Problem:(Problem No.35 from Trees) Write a program to create a binary tree as shown below with 7 nodes and 
> to find the vertical sum of the binary tree.
>
> Sample Input:
> 1 2 3 4 5 6 7
>
> Sample Output:
> 4 2 12 3 7 
>
> Explanation:
>        1
>      /   \
>    2      3
>   / \    / \
>  4   5  6   7
>
> The tree has 5 vertical lines
> Vertical-Line-1 has only one node 4 => vertical sum is 4
> Vertical-Line-2: has only one node 2=> vertical sum is 2
> Vertical-Line-3: has three nodes: 1,5,6 => vertical sum is 1+5+6 = 12
> Vertical-Line-4: has only one node 3 => vertical sum is 3
> Vertical-Line-5: has only one node 7 => vertical sum is 7
>
> So expected output is 4, 2, 12, 3 and 7
>
>
>
>
>
>  * 
>  */
>
> import java.util.HashMap;
> import java.util.Scanner;
> import java.util.*; 
>
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
> 	public static void vSum(HashMap <Integer, Integer> hash,MyBinaryTreeNode root, int c){
>
>         //System.out.println(root.data);
>         if(root.left!=null)
>         	vSum(hash, root.left, c-1);
>
>         if(root.right!=null)
>         	vSum(hash,root.right, c+1);
>
>         int data=0;
>         if(hash.containsKey(c)){
>             data=hash.get(c);
>         }
>
>
>         hash.put(c, root.data+data);
>     }
>
>     public static void verticalSum(MyBinaryTreeNode root){
>         HashMap <Integer, Integer> hash = new HashMap<Integer, Integer>();
>         vSum(hash, root, 0);
>          //System.out.print(hash);
>                  // TreeMap to store values of HashMap 
>         TreeMap<Integer, Integer> sorted = new TreeMap<>(); 
>         // Copy all data from hashMap into TreeMap 
>         sorted.putAll(hash); 
>         System.out.print(sorted);
>   
>         // Display the TreeMap which is naturally sorted 
>         for (Map.Entry<Integer, Integer> entry : sorted.entrySet())  
>             System.out.print(entry.getValue()+" ");         
>
>
>       
>     }
> 	
> }
>
> public class VerticalSum {
> 	/* main program */
> 	public static void main(String args[]) {
> 		BinaryTree tree = new BinaryTree();
>
> 		Scanner sc = new Scanner(System.in);
>
> 		MyBinaryTreeNode root = new MyBinaryTreeNode(sc.nextInt()); 
> 		tree.root = root;
> 		tree.root.setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.setRight(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getLeft().setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getLeft().setRight(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getRight().setLeft(new MyBinaryTreeNode(sc.nextInt())); 
> 		tree.root.getRight().setRight(new MyBinaryTreeNode(sc.nextInt())); 
> 	        
> 		tree.verticalSum(tree.root);
>
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%208%20Solutions/VerticalSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/VerticalSum.java
