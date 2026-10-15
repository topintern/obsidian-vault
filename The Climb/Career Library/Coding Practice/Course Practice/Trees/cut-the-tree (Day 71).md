---
kind: "coding-problem"
title: "cut-the-tree (Day 71)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/cut-the-tree-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/CutTheTree.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# cut-the-tree (Day 71)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

========= Testcases Program-1 =========
case =1
input =6
100 200 100 500 100 600
1 2
2 3
2 5
4 5
5 6
output =400

case =2
input =8
10 20 30 40 50 60 70 80
1 2
2 3
2 4
3 5
3 6
4 7
4 8
output =20

case =3
input =10
15 25 35 40 50 65 80 75 90 35
1 4
4 2
4 3
2 7 
2 6
3 8
3 9
6 5
8 10
output =40

case =4
input =8
15 25 35 40 50 65 80 75
1 2
2 4
4 3
2 7 
3 6
3 8
6 5
output =65

case =5
input =6
100 250 400 500 750 900
1 3
3 4
3 2
4 5
4 6
output =1100

case =6
input =6
100 200 300 500 400 600
1 6
6 5
6 4
4 2
4 3
output =100

case =7
input =10
10 20 10 30 10 40 10 50 10 60
1 2
2 3
2 4
3 5
3 6
4 7
4 8
5 9
5 10
output =10

case =8
input =6
300 250 100 450 750 600
2 5
2 3
3 1
3 4
1 6
output =450

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CutTheTree.java
> ```java
> /*
> ========= Testcases Program-1 =========
> case =1
> input =6
> 100 200 100 500 100 600
> 1 2
> 2 3
> 2 5
> 4 5
> 5 6
> output =400
>
> case =2
> input =8
> 10 20 30 40 50 60 70 80
> 1 2
> 2 3
> 2 4
> 3 5
> 3 6
> 4 7
> 4 8
> output =20
>
> case =3
> input =10
> 15 25 35 40 50 65 80 75 90 35
> 1 4
> 4 2
> 4 3
> 2 7 
> 2 6
> 3 8
> 3 9
> 6 5
> 8 10
> output =40
>
> case =4
> input =8
> 15 25 35 40 50 65 80 75
> 1 2
> 2 4
> 4 3
> 2 7 
> 3 6
> 3 8
> 6 5
> output =65
>
> case =5
> input =6
> 100 250 400 500 750 900
> 1 3
> 3 4
> 3 2
> 4 5
> 4 6
> output =1100
>
> case =6
> input =6
> 100 200 300 500 400 600
> 1 6
> 6 5
> 6 4
> 4 2
> 4 3
> output =100
>
> case =7
> input =10
> 10 20 10 30 10 40 10 50 10 60
> 1 2
> 2 3
> 2 4
> 3 5
> 3 6
> 4 7
> 4 8
> 5 9
> 5 10
> output =10
>
> case =8
> input =6
> 300 250 100 450 750 600
> 2 5
> 2 3
> 3 1
> 3 4
> 1 6
> output =450
>
> */
>
>
> import java.util.*;
>
> public class CutTheTree {
>     static class TreeNode{
>         int value;
>         int number;
>         ArrayList<TreeNode> children;
>         public TreeNode(int value,int number){
>             this.value = value;
>             this.number = number;
>             children = new ArrayList<TreeNode>();
>         }
>     }
>     
>     private static int dfs(TreeNode root,boolean[] visited){
>         visited[root.number]=true;
>         for(TreeNode child:root.children){
>             if(!visited[child.number]){
>                 root.value += dfs(child, visited);
>             }
>         }
>         return root.value;
>     }
>     
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         TreeNode[] treeNodes = new TreeNode[n];
>         int W  = 0;
>         
>         for(int i = 0;i < n;i++)
>         {
>             int value = in.nextInt();
>             treeNodes[i]=new TreeNode(value,i);
>             W += value;
>         }
>         
>         for(int i = 0;i < n-1;i++){
>             int a = in.nextInt();
>             int b = in.nextInt();
>             treeNodes[a-1].children.add(treeNodes[b-1]);
>             treeNodes[b-1].children.add(treeNodes[a-1]);
>         }
>         
>         boolean[] visited = new boolean[n];
>         
>         dfs(treeNodes[0], visited);
>         int miniDif = Integer.MAX_VALUE;
>         
>         for(TreeNode t:treeNodes){
>             miniDif = Math.min(miniDif, Math.abs(W-2*t.value));
>         }
>         System.out.println(miniDif);      
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/cut-the-tree-English-867d898d.pdf|cut-the-tree-English-867d898d.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/cut-the-tree-English-867d898d.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2071%20Solutions/cut-the-tree-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/cut-the-tree-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2071%20Solutions/CutTheTree.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/CutTheTree.java
