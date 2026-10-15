---
kind: "coding-problem"
title: "Jaidu Abby (Day 49)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/JaiduAbby.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Jaidu Abby (Day 49)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Mr. Abby loves his new friend jadu.Jadu has come from different planet.
As Jadu is not fit for our planet Earth,he is destined to go. 
But jadu agrees to be on planet Earth if Mr.Abby solves one of this mysterious problem 
which he has been pondering over from a long time. So jadu seeks your help!! 

You are given N and M, where N is the size of the array. S is a set of elements from 1 to M. 
You need to assign/match each number of an array to any one of its distinct prime divisors 
and the corresponding prime divisor must be present in the set S. 

Once assigned/matched, the corresponding prime divisor gets deleted from the set automatically. 
You have to find the optimal assignment/matching such as to maximize 
the count of numbers assigned/matched.

Input Format:
-------------
First line contains N and M.
Next line follows N integers which implies elements of an array.

Output Format:
--------------
Print the maximum matching possible as explained.



### Sample Input

4 10
10 60 40 55


### Sample Output

	3


### Explanation

Here N=4,M=10.
S = {1,2,3,4,5,6,7,8,9,10}
Lets find prime divisors first.
For 10 = {2,5},		
60 = {2,3,5},			
40 = {2,5},				
55 = {5,11}.
One of the optimal matching is 2 for 10,3 for 60 and 5 for 40. 


### Sample Input

5 15
65 72 343 56 712

### Sample Output

4

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · JaiduAbby.java
> ```java
> /*
>  * 
> Mr. Abby loves his new friend jadu.Jadu has come from different planet.
> As Jadu is not fit for our planet Earth,he is destined to go. 
> But jadu agrees to be on planet Earth if Mr.Abby solves one of this mysterious problem 
> which he has been pondering over from a long time. So jadu seeks your help!! 
>
> You are given N and M, where N is the size of the array. S is a set of elements from 1 to M. 
> You need to assign/match each number of an array to any one of its distinct prime divisors 
> and the corresponding prime divisor must be present in the set S. 
>
> Once assigned/matched, the corresponding prime divisor gets deleted from the set automatically. 
> You have to find the optimal assignment/matching such as to maximize 
> the count of numbers assigned/matched.
>
> Input Format:
> -------------
> First line contains N and M.
> Next line follows N integers which implies elements of an array.
>
> Output Format:
> --------------
> Print the maximum matching possible as explained.
>
>
> Sample Input:
> 4 10
> 10 60 40 55
>
> Sample Output:
> 	3
>
> Explanation:
> Here N=4,M=10.
> S = {1,2,3,4,5,6,7,8,9,10}
> Lets find prime divisors first.
> For 10 = {2,5},		
> 60 = {2,3,5},			
> 40 = {2,5},				
> 55 = {5,11}.
> One of the optimal matching is 2 for 10,3 for 60 and 5 for 40. 
>
> Sample Input:
> 5 15
> 65 72 343 56 712
> Sample Output:
> 4
>  */
>
> import java.util.*;
>
> public class JaiduAbby {
>
> 	// Global Variables
> 	static private int n, m;
> 	static private List<Integer> edge[];
>
> 	private JaiduAbby(int n) {
>
> 		edge = new List[n];
> 		for (int i = 0; i < n; i++) {
> 			edge[i] = new ArrayList<Integer>();
> 		}
>
> 	}
>
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		n = sc.nextInt();
> 		m = sc.nextInt();
> 		JaiduAbby ja = new JaiduAbby(n);
> 		int maxMatched = 0;
> 		for (int i = 0; i < n; i++) {
> 			int num = sc.nextInt();
> 			List<Integer> pList =primeFactors(num);
> 			for(int p : pList){
> 				if(num%p==0 && p<=m)edge[i].add(p);
> 			}
> 			//System.out.println(edge[i]);
> 		}
> 		int[] match = new int[m+1];
> 		Arrays.fill(match, -1);
>
> 		for (int i = 0; i < n; i++) {
> 			if (findMatch(i, new boolean[m+1], match))
> 				maxMatched++;
> 		}
>
> 		System.out.println(maxMatched);
>
> 	}
>
> 	// A function to get all unique prime factors
> 	// of a given number n
> 	static private List<Integer> primeFactors(int num) {
> 		List<Integer> primeFactor = new ArrayList<Integer>();
> 		// add the number of 2s that divide n
> 		while (num % 2 == 0) {
> 			primeFactor.add(2);
> 			num /= 2;
> 		}
> 		
> 		// n must be odd at this point. So we can 
> 		// skip one element (Note i = i +2) 
> 		for (int i = 3; i <= Math.sqrt(num); i+= 2) {
> 			// While i divides n, add i and divide n
> 			while (num % i == 0) {
> 				primeFactor.add(i);
> 				num /= i;
> 			}
> 		}
> 		// This condition is to handle the case where
> 		// n is a prime number greater than 2
> 		if (num > 2) {
> 			primeFactor.add(num);
> 		}
>
> 		/* we need unique primefactors in list */
> 		HashSet hs = new HashSet();
> 		hs.addAll(primeFactor);
> 		primeFactor.clear();
> 		primeFactor.addAll(hs);
>
> 		return primeFactor;
> 	}
>
> 	static private boolean findMatch(int u, boolean[] seen, int[] match) {
> 		for (int i = 0; i < edge[u].size(); i++) {
> 			int v = edge[u].get(i);			
> 			if (!seen[v]) {
> 				seen[v] = true;
> 				if (match[v] < 0 || findMatch(match[v], seen, match)) {
> 					match[v] = u;
> 					return true;
> 				}
> 			}
> 		}
> 		return false;
> 	}
> }
>
> /*
> ====== Testcases Program-4 ======
> case =1
> input =4 20
> 55 40 10 60
> output =4
>
> case =2
> input =3 5
> 210 78 504
> output =3
>
> case =3
> input =5 15
> 504 210 78 60 40
> output =5
>
> case =4
> input =5 15
> 79 504 67 47 210
> output =2
>
> case =5
> input =4 10
> 10 60 40 55
> output =3
>
> case =6
> input =5 15
> 65 72 343 56 712
> output =4
>
> case =7
> input =6 12
> 34 45 63 121 143 75
> output =5
>
> case =8
> input =8 17
> 34 45 63 121 143 75 65 117
> output =6
>
> case =9
> input =15 30
> 6 15 18 34 45 63 121 143 75 65 117 125 289 333 115
> output =8
>
> case =10
> input =13 30
> 6 15 18 34 45 63 121 143 75 65 117 125 289
> output =7
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2049%20Solutions/JaiduAbby.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/JaiduAbby.java
