---
kind: "coding-problem"
title: "Ramanujan Number (Day 48)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/RamanujanNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Ramanujan Number (Day 48)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have 4 cards each containing a number from 1 to 99. 
You need to judge whether they could operated through *, /, +, -, (, ) to get the value of 1729.

Example 1:
Input: 85 19 10 20
Output: True
Explanation: (85*20) + (19+10) = 1729

Example 2:
Input: 17 99 21 2
Output: False


Note:
You cannot concatenate numbers together. For example, if the input is [17, 10, 1, 9], we cannot write this as 1710+19.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RamanujanNumber.java
> ```java
> /*
>  * 
> You have 4 cards each containing a number from 1 to 99. 
> You need to judge whether they could operated through *, /, +, -, (, ) to get the value of 1729.
>
> Example 1:
> Input: 85 19 10 20
> Output: True
> Explanation: (85*20) + (19+10) = 1729
>
> Example 2:
> Input: 17 99 21 2
> Output: False
>
>
> Note:
> You cannot concatenate numbers together. For example, if the input is [17, 10, 1, 9], we cannot write this as 1710+19.
>
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class RamanujanNumber {
>
> 	 public static boolean judgePoint1729(int[] nums) {
> 	        ArrayList A = new ArrayList<Double>();
> 	        for (int v: nums) A.add((double) v);
> 	        return solve(A);
> 	    }
> 	    private static boolean solve(ArrayList<Double> nums) {
> 	        if (nums.size() == 0) return false;
> 	        if (nums.size() == 1) return Math.abs(nums.get(0) - 1729) < 1e-6;
>
> 	        for (int i = 0; i < nums.size(); i++) {
> 	            for (int j = 0; j < nums.size(); j++) {
> 	                if (i != j) {
> 	                    ArrayList<Double> nums2 = new ArrayList<Double>();
> 	                    for (int k = 0; k < nums.size(); k++) if (k != i && k != j) {
> 	                        nums2.add(nums.get(k));
> 	                    }
> 	                    for (int k = 0; k < 4; k++) {
> 	                        if (k < 2 && j > i) continue;
> 	                        if (k == 0) nums2.add(nums.get(i) + nums.get(j));
> 	                        if (k == 1) nums2.add(nums.get(i) * nums.get(j));
> 	                        if (k == 2) nums2.add(nums.get(i) - nums.get(j));
> 	                        if (k == 3) {
> 	                            if (nums.get(j) != 0) {
> 	                                nums2.add(nums.get(i) / nums.get(j));
> 	                            } else {
> 	                                continue;
> 	                            }
> 	                        }
> 	                        if (solve(nums2)) return true;
> 	                        nums2.remove(nums2.size() - 1);
> 	                    }
> 	                }
> 	            }
> 	        }
> 	        return false;
> 	    }
> 	    
> 	    public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numberline = str.split(" ");
> 			int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(judgePoint1729(nums));   
> 			
> 			}
> }
>
> /*
> =======Testcases=======
> case =1
> input =34 5 10 29
> output =true
>
> case =2
> input =40 4 43 5
> output =true
>
> case =3
> input =68 24 5 25
> output =true
>
> case =4
> input =40 65 64 40
> output =true
>
> case =5
> input =66 64 39 41
> output =true
>
> case =6
> input =34 5 10 19
> output =false
>
> case =7
> input =40 6 43 5
> output =false
>
> case =8
> input =68 24 5 30
> output =false
>
> case =9
> input =40 65 64 41
> output =false
>
> case =10
> input =66 64 39 40
> output =false
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2048%20Solutions/RamanujanNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/RamanujanNumber.java
