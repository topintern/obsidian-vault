---
kind: "coding-problem"
title: "Max Trees (Day 117)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/MaxTrees.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Trees (Day 117)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are N celebrities participated in Go-Green Campaign,
All of them joined together and each one planted a tree on a flat land at different positions.
 
Now, your task is to find the maximum number of trees in single straight line.

Input Format:
-------------
Line-1 -> An integers N, number of trees planted.
Next N lines -> Two space separated integers, position of the tree.

Output Format:
--------------
Print an integer as result.


Sample Input-1:
---------------
6
1 1
3 2
5 3
4 1
2 3
1 4

Sample Output-1:
----------------
4


### Explanation

------------

Y
|
|	"
| 		"			"
|			"
|	"			"	
------------------- X
0  1  2  3  4  5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxTrees.txt
> ```java
> /*
> There are N celebrities participated in Go-Green Campaign,
> All of them joined together and each one planted a tree on a flat land at different positions.
>  
> Now, your task is to find the maximum number of trees in single straight line.
>
> Input Format:
> -------------
> Line-1 -> An integers N, number of trees planted.
> Next N lines -> Two space separated integers, position of the tree.
>
> Output Format:
> --------------
> Print an integer as result.
>
>
> Sample Input-1:
> ---------------
> 6
> 1 1
> 3 2
> 5 3
> 4 1
> 2 3
> 1 4
>
> Sample Output-1:
> ----------------
> 4
>
> Explanation:
> ------------
>
> Y
> |
> |	"
> | 		"			"
> |			"
> |	"			"	
> ------------------- X
> 0  1  2  3  4  5
>
> */
>
> import java.util.*;
>
> public class MaxTrees{
> 	public int maxTrees(int[][] trees) {
> 		if (trees==null) return 0;
>         if (trees.length<=2) return trees.length;
> 		
> 		Map<Integer,Map<Integer,Integer>> map = new HashMap<Integer,Map<Integer,Integer>>();
> 		int result=0;
> 		for (int i=0;i<trees.length;i++){ 
> 			map.clear();
> 			int overlap=0,max=0;
> 			for (int j=i+1;j<trees.length;j++){
> 				int x=trees[j][0]-trees[i][0];
> 				int y=trees[j][1]-trees[i][1];
> 				if (x==0&&y==0){
> 					overlap++;
> 					continue;
> 				}
> 				int gcd=generateGCD(x,y);
> 				if (gcd!=0){
> 					x/=gcd;
> 					y/=gcd;
> 				}
> 				
> 				if (map.containsKey(x)){
> 					if (map.get(x).containsKey(y)){
> 						map.get(x).put(y, map.get(x).get(y)+1);
> 					}else{
> 						map.get(x).put(y, 1);
> 					}   					
> 				}else{
> 					Map<Integer,Integer> m = new HashMap<Integer,Integer>();
> 					m.put(y, 1);
> 					map.put(x, m);
> 				}
> 				max=Math.max(max, map.get(x).get(y));
> 			}
> 			result=Math.max(result, max+overlap+1);
> 		}
> 		return result;		
> 	}
> 	private int generateGCD(int a,int b){
>
> 		if (b==0) return a;
> 		else return generateGCD(b,a%b);
> 		
> 	}
> 	public static void main(String args[] ) {
> 	    Scanner sc = new Scanner(System.in);
> 		int N= sc.nextInt();
> 		int[][] trees = new int[N][2];
> 		for(int i=0;i<N;i++)
> 			for(int j=0;j<2;j++)
> 				trees[i][j]= sc.nextInt();
> 			
> 		System.out.println(new MaxTrees().maxTrees(trees));
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20117%20Solutions/MaxTrees.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/MaxTrees.txt
