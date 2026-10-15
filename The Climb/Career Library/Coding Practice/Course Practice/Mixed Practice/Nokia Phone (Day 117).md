---
kind: "coding-problem"
title: "Nokia Phone (Day 117)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/NokiaPhone.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Nokia Phone (Day 117)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a nokia phone,with the following dialpad.
		1 2 3
		4 5 6
		7 8 9
0 #
And You are given an L band to dial the number,  
Using the L band you can dial the number as follows, 
You can start with any digit,
	if you are at digit 1, next digit you can choose {6,8}
	if you are at digit 2, next digit you can choose {7,9}
	if you are at digit 3, next digit you can choose {4,8}
	and so on..

Now your task is to find how many distinct numbers of length N you can dial.

Note: Numbers should contain only digits, no {* , #}.
Answer is modulo 1000000007.

Input Format:
-----------------
An integer N, length of numbers
 
Output Format:
------------------
Print an integer, number of distinct numbers you can dial.


Sample Input-1:
---------------
1

Sample Output-1:
----------------
10


### Explanation

-------------
To dial a number of length 1, you can dial all digits.


Sample Input-2:
---------------
2

Sample Output-2:
----------------
20


### Explanation

------------
To dial a number of length 2, the possible numbers are
{04, 06, 16, 18, 27, 29, 34, 38, 40, 43, 49, 60, 61, 67, 72, 76, 81, 83, 92, 94}

Sample Input-3:
---------------
5

Sample Output-3:
----------------
240

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NokiaPhone.txt
> ```java
> /*
> Given a nokia phone,with the following dialpad.
> 		1 2 3
> 		4 5 6
> 		7 8 9
> 		* 0 #
> And You are given an L band to dial the number,  
> Using the L band you can dial the number as follows, 
> You can start with any digit,
> 	if you are at digit 1, next digit you can choose {6,8}
> 	if you are at digit 2, next digit you can choose {7,9}
> 	if you are at digit 3, next digit you can choose {4,8}
> 	and so on..
>
> Now your task is to find how many distinct numbers of length N you can dial.
>
> Note: Numbers should contain only digits, no {* , #}.
> Answer is modulo 1000000007.
>
> Input Format:
> -----------------
> An integer N, length of numbers
>  
> Output Format:
> ------------------
> Print an integer, number of distinct numbers you can dial.
>
>
> Sample Input-1:
> ---------------
> 1
>
> Sample Output-1:
> ----------------
> 10
>
> Explanation:
> -------------
> To dial a number of length 1, you can dial all digits.
>
>
> Sample Input-2:
> ---------------
> 2
>
> Sample Output-2:
> ----------------
> 20
>
> Explanation:
> ------------
> To dial a number of length 2, the possible numbers are
> {04, 06, 16, 18, 27, 29, 34, 38, 40, 43, 49, 60, 61, 67, 72, 76, 81, 83, 92, 94}
>
> Sample Input-3:
> ---------------
> 5
>
> Sample Output-3:
> ----------------
> 240
>
> */
> import java.util.*;
> class NokiaPhone {
>     public int lbandDialer(int N) {
>         if(N==1) return 10;
>         long mod = 1000000007;
>         long[] pre = new long[10];  // to record previous result. It is needed because if we only use cur, the cur array itself is changed during calculation. 
>         long[] cur = new long[10];  // to record current result. 
>         Arrays.fill(pre,1);
>         while(--N>0){
>             cur[0]=(pre[4]+pre[6])%mod;
>             cur[1]=(pre[6]+pre[8])%mod;
>             cur[2]=(pre[7]+pre[9])%mod;
>             cur[3]=(pre[4]+pre[8])%mod;
>             cur[4]=(pre[3]+pre[9]+pre[0])%mod;
>             cur[6]=(pre[1]+pre[7]+pre[0])%mod;
>             cur[7]=(pre[2]+pre[6])%mod;
>             cur[8]=(pre[1]+pre[3])%mod;
>             cur[9]=(pre[2]+pre[4])%mod;
>
>             for(int i=0; i<10; i++) pre[i]=cur[i];  //Right for it's value copy(deep copy).
>         }
>         long sum = 0;
>         for(int i=0; i<10; i++){
>             sum = (sum+cur[i])%mod;
>         }
>         return (int)sum;
>     }
> 	
> 	public static void main(String args[] ) {
> 	    Scanner sc = new Scanner(System.in);
> 		int N= sc.nextInt();			
> 		System.out.println(new NokiaPhone().lbandDialer(n));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20117%20Solutions/NokiaPhone.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/NokiaPhone.txt
