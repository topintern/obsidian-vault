---
kind: "coding-problem"
title: "Flower Box (Day 33)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 33 Solutions/FlowerBox.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Flower Box (Day 33)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a row of trees, the i-th tree produces fruit with type tree[i].

You start at any tree of your choice, then repeatedly perform the following steps:
    - Add one piece of fruit from this tree to your baskets,  
      If you cannot, stop.
    - Move to the next tree to the right of the current tree,
      If there is no tree to the right, stop.
    - Note that you do not have any choice after the initial choice of starting tree: 
      you must perform step 1, then step 2, then back to step 1, then step 2, and so on 
      until you stop.

You have two baskets, and each basket can carry any quantity of fruit, 
but you want each basket to only carry one type of fruit each.

What is the total amount of fruit you can collect with this procedure?

 

Example 1:
    Input: 1 2 1
    Output: 3
    Explanation: We can collect [1,2,1].
    
    
Example 2:
    Input: 0 1 2 2
    Output: 3
    Explanation: We can collect [1,2,2].
        If we started at the first tree, we would only collect [0, 1].


Example 3:
    Input: 1 2 3 2 2
    Output: 4
    Explanation: We can collect [2,3,2,2].
        If we started at the first tree, we would only collect [1, 2].


Example 4:
    Input: 3 3 3 1 2 1 1 2 3 3 2 4
    Output: 5
    Explanation: We can collect [1,2,1,1,2].
        If we started at the first tree or the eighth tree, we would only collect 4 fruits.

=====TestCases=========
case =1
input =1 2 3 4 2 3 1 2 3
output =2

case =2
input =1 1 1 2 3 2 3 2 3 2 3 2 4 1 4
output =9

case =3
input =0 1 0 1 2 1 2 2 1 3 4 3 2
output =6

case =4
input =3 3 3 3 4 2 2 2 1 2 4
output =5

case =5
input =2 4 5 6 2 1 3 5 4 1 2 2 3 3 4
output =4

case =6
input =2 2 2 2 2 2 2 2 2 2 3 3 3 3
output =14

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FlowerBox.java
> ```java
> /*
> In a row of trees, the i-th tree produces fruit with type tree[i].
>
> You start at any tree of your choice, then repeatedly perform the following steps:
>     - Add one piece of fruit from this tree to your baskets,  
>       If you cannot, stop.
>     - Move to the next tree to the right of the current tree,
>       If there is no tree to the right, stop.
>     - Note that you do not have any choice after the initial choice of starting tree: 
>       you must perform step 1, then step 2, then back to step 1, then step 2, and so on 
>       until you stop.
>
> You have two baskets, and each basket can carry any quantity of fruit, 
> but you want each basket to only carry one type of fruit each.
>
> What is the total amount of fruit you can collect with this procedure?
>
>  
>
> Example 1:
>     Input: 1 2 1
>     Output: 3
>     Explanation: We can collect [1,2,1].
>     
>     
> Example 2:
>     Input: 0 1 2 2
>     Output: 3
>     Explanation: We can collect [1,2,2].
>         If we started at the first tree, we would only collect [0, 1].
>
>
> Example 3:
>     Input: 1 2 3 2 2
>     Output: 4
>     Explanation: We can collect [2,3,2,2].
>         If we started at the first tree, we would only collect [1, 2].
>
>
> Example 4:
>     Input: 3 3 3 1 2 1 1 2 3 3 2 4
>     Output: 5
>     Explanation: We can collect [1,2,1,1,2].
>         If we started at the first tree or the eighth tree, we would only collect 4 fruits.
>
> =====TestCases=========
> case =1
> input =1 2 3 4 2 3 1 2 3
> output =2
>
> case =2
> input =1 1 1 2 3 2 3 2 3 2 3 2 4 1 4
> output =9
>
> case =3
> input =0 1 0 1 2 1 2 2 1 3 4 3 2
> output =6
>
> case =4
> input =3 3 3 3 4 2 2 2 1 2 4
> output =5
>
> case =5
> input =2 4 5 6 2 1 3 5 4 1 2 2 3 3 4
> output =4
>
> case =6
> input =2 2 2 2 2 2 2 2 2 2 3 3 3 3
> output =14
>
> */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class FlowerBox {
> 	 public static int totalFlower(int[] tree) {
> 	        int res = 0, cur = 0, count_b = 0, a = 0, b = 0;
> 	        for (int c :  tree) {
> 	            cur = c == a || c == b ? cur + 1 : count_b + 1;
> 	            count_b = c == b ? count_b + 1 : 1;
> 	            if (b != c) {a = b; b = c;}
> 	            res = Math.max(res, cur);
> 	        }
> 	        return res;
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] numbers = str.split(" ");
> 		int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.println(totalFruit(arr));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2033%20Solutions/FlowerBox.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 33 Solutions/FlowerBox.java
