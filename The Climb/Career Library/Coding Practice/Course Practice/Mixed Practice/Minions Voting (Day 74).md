---
kind: "coding-problem"
title: "Minions Voting (Day 74)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/MinionsVoting.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Minions Voting (Day 74)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are N minions who are competing in an election of the president of the ACM (Association of Cute Minions). They are standing in a line in the order from minion 1 to minion N. For each i (1 ? i ? N), the i-th minion has an influence level of Si.

A single minion may cast any number of votes. Minion j will vote for minion i (i ? j) if and only if the influence level of the j-th minion is greater than or equal to the sum of influence levels of all the minions standing between them (excluding the i-th and j-th minion).

Your task is to find the number of votes received by each minion.


### Input

The first line of the input contains a single integer T denoting the number of test cases. The description of T test cases follows.

The first line of each test case contains a single integer N denoting the number of minions.

The second line contains N space-separated integers S1, S2, ..., SN.


### Output

print a single line containing N space-separated integers. For each valid i, the i-th of these integers should denote the number of votes the i-th minion will get.



Sample Input 1:
4
4 3 2 1

Sample Output 1:
1 2 3 2


### Explanation:


    The first minion will get only a vote of the second minion.
    The second minion will get votes of the first and third minion.
    The third minion will get votes of the first, second and fourth minion.
    The fourth minion will get votes of the second and third minion.

----------Testcases Prog-2 ---------
case =1
input =4
4 3 2 1
output =1 2 3 2

case =2
input =5
1 2 2 3 1
output =2 3 2 3 1

case =3
input =6
3 2 4 1 5 2
output =2 3 4 2 3 1

case =4
input =5
1 2 3 4 5
output =2 3 3 2 1

case =5
input =7
5 3 2 5 4 4 5
output =2 3 3 5 3 3 2

case =6
input =8
3 2 3 2 3 2 2 3
output =2 2 4 2 4 3 3 2

case =7
input =10
2 3 2 5 2 4 3 2 1 2
output=2 3 2 4 2 3 2 4 3 3

case =8
input =8
1 1 1 1 1 1 1 1
output =2 3 4 4 4 4 3 2

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MinionsVoting.txt
> ```java
> /*
>  * 
> There are N minions who are competing in an election of the president of the ACM (Association of Cute Minions). They are standing in a line in the order from minion 1 to minion N. For each i (1 ? i ? N), the i-th minion has an influence level of Si.
>
> A single minion may cast any number of votes. Minion j will vote for minion i (i ? j) if and only if the influence level of the j-th minion is greater than or equal to the sum of influence levels of all the minions standing between them (excluding the i-th and j-th minion).
>
> Your task is to find the number of votes received by each minion.
>
> Input
> The first line of the input contains a single integer T denoting the number of test cases. The description of T test cases follows.
>
> The first line of each test case contains a single integer N denoting the number of minions.
>
> The second line contains N space-separated integers S1, S2, ..., SN.
>
> Output
> print a single line containing N space-separated integers. For each valid i, the i-th of these integers should denote the number of votes the i-th minion will get.
>
>
>
> Sample Input 1:
> 4
> 4 3 2 1
>
> Sample Output 1:
> 1 2 3 2
>
> Explanation:
>
>     The first minion will get only a vote of the second minion.
>     The second minion will get votes of the first and third minion.
>     The third minion will get votes of the first, second and fourth minion.
>     The fourth minion will get votes of the second and third minion.
>
> ----------Testcases Prog-2 ---------
> case =1
> input =4
> 4 3 2 1
> output =1 2 3 2
>
> case =2
> input =5
> 1 2 2 3 1
> output =2 3 2 3 1
>
> case =3
> input =6
> 3 2 4 1 5 2
> output =2 3 4 2 3 1
>
> case =4
> input =5
> 1 2 3 4 5
> output =2 3 3 2 1
>
> case =5
> input =7
> 5 3 2 5 4 4 5
> output =2 3 3 5 3 3 2
>
> case =6
> input =8
> 3 2 3 2 3 2 2 3
> output =2 2 4 2 4 3 3 2
>
> case =7
> input =10
> 2 3 2 5 2 4 3 2 1 2
> output=2 3 2 4 2 3 2 4 3 3
>
> case =8
> input =8
> 1 1 1 1 1 1 1 1
> output =2 3 4 4 4 4 3 2
>
>
>  * 
>  * 
>  */
> import java.util.*;
>  
> class MinionsVoting {
> 	
> 	
> 	public static void main(String[] args)  {
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int numOfMinions = sc.nextInt();
> 		int minionsInfluence[] = new int[numOfMinions];
> 		
> 		for(int i = 0 ; i < numOfMinions ; ++i )
> 			minionsInfluence[i] = sc.nextInt();
> 		
> 		int sumOfInfluence[] = new int[numOfMinions];
> 		int res[] = new int[numOfMinions];
> 		
> 		sumOfInfluence = Arrays.copyOfRange(minionsInfluence , 0 , numOfMinions);
> 		Arrays.fill(res , 0);
> 		//calculate for each minion, sum of all his left side minions influences
> 		for(int i = 1 ; i < numOfMinions ; ++i ) {
> 			sumOfInfluence[i] += sumOfInfluence[i-1];
> 		}
> 		
> 		for(int i = 0 ; i < numOfMinions ; ++i ) { 
> 			//check right side minions can vote current minion or not
> 			for(int j = i + 1 ; j < numOfMinions ; ++j ) { 
> 				long diff = sumOfInfluence[j] - sumOfInfluence[i] - minionsInfluence[j];
> 				if(minionsInfluence[i] >= diff) 
> 					++res[j];
> 				else if(minionsInfluence[j] < diff) 
> 					break;
> 			
> 			}
> 			//check left side minions can vote current minion or not
> 			for(int j = i - 1 ; j >= 0 ; --j ) { 
> 				long diff = sumOfInfluence[i] - sumOfInfluence[j] - minionsInfluence[i];
> 				if(minionsInfluence[i] >= diff) 
> 					++res[j];
> 				else
> 					break;
> 			
> 			}
> 		}
> 		
> 		for(int i = 0 ; i < numOfMinions ; ++i )
> 			System.out.print(res[i] + " ");
> 		
> 	}
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2074%20Solutions/MinionsVoting.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/MinionsVoting.txt
