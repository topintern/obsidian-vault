---
kind: "coding-problem"
title: "Greedy Florist (Day 70)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 70 Solutions/GreedyFlorist.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Greedy Florist (Day 70)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A group of friends want to buy a bouquet of flowers. 
The florist wants to maximize his number of new customers and the money he makes. 
To do this, he decides he'll multiply the price of each flower 
by the number of that customer's previously purchased flowers plus 1. 
The first flower will be original price, (0+1)* original price, 
the next will be (0+1)* original price and so on.

Given the size of the group of friends, 
the number of flowers they want to purchase and the original prices of the flowers, 
determine the minimum cost to purchase all of the flowers.

For example, if there are k=3 friends that want to buy n=4 flowers that cost c=[1,2,3,4]
each will buy one of the flowers priced [2,3,4] at the original price. 
Having each purchased x=1 flower, the first flower in the list,c[0] , will now cost 
(previous purchases+1)*c[0]. The total cost will be 4+3+2+2=11.


### Input Format

	- The first line contains two space-separated integers n and k, 
	  the number of flowers and the number of friends.
	- The second line contains n space-separated positive integers c[i], 
	  the original price of each flower.


### Output Format

	- Print the minimum cost to buy all  flowers.

Sample Input1:
3 3
2 5 6
Sample Output1:
13

Explanation1:
There are n=3 flowers with costs c=[2,5,6] and k=3 people in the group. 
If each person buys one flower, the total cost of prices paid is  2+5+6=13 dollars. 

Sample Input2:
3 2
2 5 6
Sample Output2:
15
Explanation2:
There are n=3 flowers with costs c=[2,5,6] and k=2 people in the group. 
We can minimize the total purchase cost like so:
	- The first person purchases 2 flowers in order of decreasing price; 
	  this means they buy the more expensive flower (c1=5) first at price 5 dollars 
	  and the less expensive flower (c0=2) second at price (1+1)*2=4 dollars.
	- The second person buys the most expensive flower at price 6 dollars.
We then print the sum of these purchases, which is 5+4+6=15, as our answer.

Sample Input3:
5 3
1 3 5 7 9
Sample Output3:
29
Explanation3:
The friends buy flowers for 9, 7 and 3, 5 and 1 for a cost of 9+ 7+3*(1+1) + 5+1*(1+1).


========= Testcases Program-1 =========
case =1
input =5 3
1 3 5 7 9
output =29

case =2
input =3 2
2 5 6
output =15

case =3
input =3 3
2 5 6
output =13

case =4
input =6 4
8 3 9 2 5 6
output =38

case =5
input =9 3
15 14 18 19 7 9 3 8 2
output =150

case =6
input =9 6
15 14 18 19 7 9 3 8 2
output =107

case =7
input =12 5
3 4 5 6 9 8 2 7 11 10 12 1 
output =109

case =8
input =12 2
3 4 5 6 9 8 2 7 11 10 12 1
output =203

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GreedyFlorist.java
> ```java
> /*
> A group of friends want to buy a bouquet of flowers. 
> The florist wants to maximize his number of new customers and the money he makes. 
> To do this, he decides he'll multiply the price of each flower 
> by the number of that customer's previously purchased flowers plus 1. 
> The first flower will be original price, (0+1)* original price, 
> the next will be (0+1)* original price and so on.
>
> Given the size of the group of friends, 
> the number of flowers they want to purchase and the original prices of the flowers, 
> determine the minimum cost to purchase all of the flowers.
>
> For example, if there are k=3 friends that want to buy n=4 flowers that cost c=[1,2,3,4]
> each will buy one of the flowers priced [2,3,4] at the original price. 
> Having each purchased x=1 flower, the first flower in the list,c[0] , will now cost 
> (previous purchases+1)*c[0]. The total cost will be 4+3+2+2=11.
>
> Input Format
> 	- The first line contains two space-separated integers n and k, 
> 	  the number of flowers and the number of friends.
> 	- The second line contains n space-separated positive integers c[i], 
> 	  the original price of each flower.
>
> Output Format
> 	- Print the minimum cost to buy all  flowers.
>
> Sample Input1:
> 3 3
> 2 5 6
> Sample Output1:
> 13
>
> Explanation1:
> There are n=3 flowers with costs c=[2,5,6] and k=3 people in the group. 
> If each person buys one flower, the total cost of prices paid is  2+5+6=13 dollars. 
>
> Sample Input2:
> 3 2
> 2 5 6
> Sample Output2:
> 15
> Explanation2:
> There are n=3 flowers with costs c=[2,5,6] and k=2 people in the group. 
> We can minimize the total purchase cost like so:
> 	- The first person purchases 2 flowers in order of decreasing price; 
> 	  this means they buy the more expensive flower (c1=5) first at price 5 dollars 
> 	  and the less expensive flower (c0=2) second at price (1+1)*2=4 dollars.
> 	- The second person buys the most expensive flower at price 6 dollars.
> We then print the sum of these purchases, which is 5+4+6=15, as our answer.
>
> Sample Input3:
> 5 3
> 1 3 5 7 9
> Sample Output3:
> 29
> Explanation3:
> The friends buy flowers for 9, 7 and 3, 5 and 1 for a cost of 9+ 7+3*(1+1) + 5+1*(1+1).
>
>
> ========= Testcases Program-1 =========
> case =1
> input =5 3
> 1 3 5 7 9
> output =29
>
> case =2
> input =3 2
> 2 5 6
> output =15
>
> case =3
> input =3 3
> 2 5 6
> output =13
>
> case =4
> input =6 4
> 8 3 9 2 5 6
> output =38
>
> case =5
> input =9 3
> 15 14 18 19 7 9 3 8 2
> output =150
>
> case =6
> input =9 6
> 15 14 18 19 7 9 3 8 2
> output =107
>
> case =7
> input =12 5
> 3 4 5 6 9 8 2 7 11 10 12 1 
> output =109
>
> case =8
> input =12 2
> 3 4 5 6 9 8 2 7 11 10 12 1
> output =203
>
> */
>
>
> import java.io.*;
> import java.util.*;
> class GreedyFlorist {
> public static void main(String arg[])throws IOException
>     {
>         BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
>
>
>            String a=br.readLine();int l=0,sum=0,m1=1;
>            StringTokenizer s1=new StringTokenizer(a);
>            int n=Integer.parseInt(s1.nextToken());
>            int m=Integer.parseInt(s1.nextToken());
>            int a1[]=new int[n];
>
>            String x=br.readLine();
>
>            StringTokenizer x1=new StringTokenizer(x);
>
>            for(int i=0;i<n;i++)
>            {
>                a1[i]=Integer.parseInt(x1.nextToken());
>
>            }
>            Arrays.sort(a1);
>            for(int i=n-1;i>=0;i--)
>            {
>             
>             if(l==m)
>             {
>                 l=0;
>                 m1++;
>             }
>             l++;
>             sum=sum+a1[i]*m1;
>            }
> 		System.out.println(sum);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2070%20Solutions/GreedyFlorist.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 70 Solutions/GreedyFlorist.java
