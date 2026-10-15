---
kind: "coding-problem"
title: "PARTY"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/party q.txt","CODING RESOURCES/coding ninjas/Dp-2/party s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# PARTY

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You just received another bill which you cannot pay because you lack the money.
Unfortunately, this is not the first time to happen, and now you decide to investigate the cause of your constant monetary shortness. The reason is quite obvious: the lion's share of your money routinely disappears at the entrance of party localities.
You make up your mind to solve the problem where it arises, namely at the parties themselves. You introduce a limit for your party budget and try to have the most possible fun with regard to this limit.
You inquire beforehand about the entrance fee to each party and estimate how much fun you might have there. The list is readily compiled, but how do you actually pick the parties that give you the most fun and do not exceed your budget?
Write a program which finds this optimal set of parties that offer the most fun. Keep in mind that your budget need not necessarily be reached exactly. Achieve the highest possible fun level, and do not spend more money than is absolutely necessary.

### Input

The first line of the input specifies your party budget and the number n of parties.

The following n lines contain two numbers each. The first number indicates the entrance fee of each party. Parties cost between 5 and 25 francs. The second number indicates the amount of fun of each party, given as an integer number ranging from 0 to 10.

The budget will not exceed 500 and there will be at most 100 parties. All numbers are separated by a single space.

There are many test cases. Input ends with 0 0.

### Output

For each test case your program must output the sum of the entrance fees and the sum of all fun values of an optimal solution. Both numbers must be separated by a single space. 

### Sample Input

```text
50 10
12 3
15 8
16 9
16 6
10 2
21 9
18 4
12 4
17 8
18 9 

50 10
13 8
19 10
16 8
12 9
10 2
12 8
13 5
15 5
11 7
16 2

0 0
```

### Sample Output

```text
49 26
48 32
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · party s.txt
> ```cpp
> #include <iostream>
> #include <cstdio>
> #include <algorithm>
>
> using namespace std;
> int w[101], val[101], dp[101][501];
> int main()
> {
>     int i, j, W, n, ans;
>     while(1)
>     {
>     	cin>>W>>n;
>     	if(W==0&&n==0)
>     	break;
> 	    w[0]=0;
> 	    val[0]=0;
> 	    for(i=0;i<n;i++)
> 	        scanf("%d %d", &w[i+1], &val[i+1]);
> 	    for(i=0;i<=n;i++)
> 	        dp[i][0]=0;
> 	    for(j=0;j<=W;j++)
> 	        dp[0][j]=0;
> 	    for(i=1;i<=n;i++)
> 	    for(j=1;j<=W;j++)
> 	    {//Every time i am checking if max weight is j
> 	        if(w[i]>j)
> 	        {
> 	            dp[i][j]=dp[i-1][j];//if weight of the element is more than the required weight ..just give value of previous item
> 	        }
> 	        else
> 	        dp[i][j]=max(dp[i-1][j], dp[i-1][j-w[i]]+val[i]);
> 	    }
> 	    ans=W;
> 	    for(i=0;i<W;i++)
> 	    {
> 	        if(dp[n][i]==dp[n][W])
> 	        {
> 	            ans=i;
> 	            break;
> 	        }
> 	    }
> 	    printf("%d %d\n", ans, dp[n][W]);
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/party%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/party q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/party%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/party s.txt
