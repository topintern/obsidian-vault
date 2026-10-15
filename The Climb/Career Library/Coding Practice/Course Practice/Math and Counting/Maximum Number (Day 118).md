---
kind: "coding-problem"
title: "Maximum Number (Day 118)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/MaximumNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Maximum Number (Day 118)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Ram and Sam are friends, both of them have a number each, of length P and Q.
They are planned to create a new number, which is the biggest number of length K,
Where K is <= P+Q.

You will be given the digit arrays of those two numbers.
for example, Ram's number is 123 and Sam;s number is 3765 and K is 4
you will be given as, [1,2,3] and [3,7,6,5], -> bigggest number possible is [7,6,5,3]

Please help Ram and Sam, find out the biggest possible number of K length, 
without changing the relative order of the digits in their arrays.

Input Format:
-------------
Line-1 -> Two integers P and Q.
Line-2 -> P space separated digits, Ram's Number
Line-3 -> Q space separated digits, Sam's Number
Line-4 -> K, length of the biggest number.

Output Format:
--------------
Print the array of digits, of the biggest number.


Sample Input-1:
---------------
3 4
5 7 6
0 0 1 0
5

Sample Output-1:
----------------
[7, 6, 0, 1, 0]


Sample Input-2:
---------------
2 2
2 5
4 5
3

Sample Output-2:
----------------
[5, 4, 5]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaximumNumber.java
> ```java
> /*
> Ram and Sam are friends, both of them have a number each, of length P and Q.
> They are planned to create a new number, which is the biggest number of length K,
> Where K is <= P+Q.
>
> You will be given the digit arrays of those two numbers.
> for example, Ram's number is 123 and Sam;s number is 3765 and K is 4
> you will be given as, [1,2,3] and [3,7,6,5], -> bigggest number possible is [7,6,5,3]
>
> Please help Ram and Sam, find out the biggest possible number of K length, 
> without changing the relative order of the digits in their arrays.
>
> Input Format:
> -------------
> Line-1 -> Two integers P and Q.
> Line-2 -> P space separated digits, Ram's Number
> Line-3 -> Q space separated digits, Sam's Number
> Line-4 -> K, length of the biggest number.
>
> Output Format:
> --------------
> Print the array of digits, of the biggest number.
>
>
> Sample Input-1:
> ---------------
> 3 4
> 5 7 6
> 0 0 1 0
> 5
>
> Sample Output-1:
> ----------------
> [7, 6, 0, 1, 0]
>
>
> Sample Input-2:
> ---------------
> 2 2
> 2 5
> 4 5
> 3
>
> Sample Output-2:
> ----------------
> [5, 4, 5]
>
> */
> import java.util.*;
>
> class MaximumNumber {
> 	public int[] maxNumber(int[] nums1, int[] nums2, int k) {
> 		int n = nums1.length;
> 		int m = nums2.length;
> 		int[] ans = new int[k];
> 		for (int i = Math.max(0, k - m); i <= k && i <= n; ++i) {
> 			int[] candidate = merge(maxArray(nums1, i), maxArray(nums2, k - i), k);
> 			if (greater(candidate, 0, ans, 0)) ans = candidate;
> 		}
> 		return ans;
> 	}
> 	private int[] merge(int[] nums1, int[] nums2, int k) {
> 		int[] ans = new int[k];
> 		for (int i = 0, j = 0, r = 0; r < k; ++r)
> 			ans[r] = greater(nums1, i, nums2, j) ? nums1[i++] : nums2[j++];
> 		return ans;
> 	}
> 	public boolean greater(int[] nums1, int i, int[] nums2, int j) {
> 		while (i < nums1.length && j < nums2.length && nums1[i] == nums2[j]) {
> 			i++;
> 			j++;
> 		}
> 		return j == nums2.length || (i < nums1.length && nums1[i] > nums2[j]);
> 	}
> 	public int[] maxArray(int[] nums, int k) {
> 		int n = nums.length;
> 		int[] ans = new int[k];
> 		for (int i = 0, j = 0; i < n; ++i) {
> 			while (n - i + j > k && j > 0 && ans[j - 1] < nums[i]) j--;
> 			if (j < k) ans[j++] = nums[i];
> 		}
> 		return ans;
> 	}
> 	public static void main( String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int m=sc.nextInt();
> 		int n=sc.nextInt();
> 		int[] n1=new int[m];
> 		int[] n2=new int[n];
> 		for(int i=0;i<m;i++)
> 			n1[i]=sc.nextInt();
> 		for(int i=0;i<n;i++)
> 			n2[i]=sc.nextInt();
> 		int k=sc.nextInt();
> 		int[] res=new MaximumNumber().maxNumber(n1,n2,k);
> 		
> 		System.out.println(Arrays.toString(res));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20118%20Solutions/MaximumNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/MaximumNumber.java
