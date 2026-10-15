---
kind: "coding-problem"
title: "Kingdom Of Monkeys"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/kingdom of monkey q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/kingdom of monkey s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Kingdom Of Monkeys

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

This is the story in Zimbo, the kingdom officially made for monkeys. Our Code Monk visited Zimbo and declared open a challenge in the kingdom, thus spoke to all the monkeys :

You all have to make teams and go on a hunt for Bananas. The team that returns with the highest number of Bananas will be rewarded with as many gold coins as the number of Bananas with them. May the force be with you!
Given there are N monkeys in the kingdom. Each monkey who wants to team up with another monkey has to perform a ritual. Given total M rituals are performed. Each ritual teams up two monkeys. If Monkeys A and B teamed up and Monkeys B and C teamed up, then Monkeys A and C are also in the same team.

You are given an array A where Ai is the number of bananas i'th monkey gathers.

Find out the number of gold coins that our Monk should set aside for the prize.

### Input

First line contains an integer T. T test cases follow. First line of each test case contains two space-separated N and M. M lines follow. Each of the M lines contains two integers Xi and Yi, the indexes of monkeys that perform the i'th ritual. Last line of the testcase contains N space-separated integer constituting the array A.

### Output

Print the answer to each test case in a new line.

### Constraints

1 = T = 10
1 = N = 10^5
0 = M = 10^5
0 = Ai = 10^12

### SAMPLE INPUT

```text
1
4 3
1 2
2 3
3 1
1 2 3 5
```

### SAMPLE OUTPUT

```text
6
```

### Explanation

Monkeys 1,2 ,3 are in the same team. They gather 1+2+3=6 bananas.
Monkey 4 is a team. It gathers 5 bananas.
Therefore, number of gold coins (highest number of bananas by a team) = 6.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · kingdom of monkey s.txt
> ```java
> import java.io.*;
> import java.util.*;
>  
> class solution {
>     static long dfs(int s,boolean []visited,LinkedList []adj,int []a)
>     {
>         visited[s]=true;
>         Stack<Integer> stack=new Stack<>();
>         stack.push(s);
>         long sum=0;
>         sum=a[s];
>         while(stack.empty()==false)
>         {
>             int p=stack.peek();
>             //System.out.println("p is "+p);
>             stack.pop();
>             if(visited[p]==false)
>             {
>                 visited[p]=true;
>                 sum=sum+a[p];
>             }
>             Iterator<Integer> it=adj[p].listIterator();
>             while(it.hasNext())
>             {
>                 int v=it.next();
>                 if(visited[v]==false)
>                 stack.push(v);
>             }
>         }
>         return sum;
>     }
>     public static void main(String args[]){
>        Scanner scan=new Scanner(System.in);
>        int t=scan.nextInt();
>        for(int i=0;i<t;i++)
>        {
>            int n=scan.nextInt();
>            int m=scan.nextInt();
>            LinkedList<Integer> []adj=new LinkedList[n];
>            boolean []visited=new boolean[n];
>            for(int j=0;j<n;j++)
>            {
>                adj[j]=new LinkedList();
>            }
>            for(int j=0;j<m;j++)
>            {
>                int a=scan.nextInt();
>                int b=scan.nextInt();
>                adj[a-1].add(b-1);
>                adj[b-1].add(a-1);
>            }
>            int a[]=new int[n];
>            for(int j=0;j<n;j++)
>            {
>                a[j]=scan.nextInt();
>            }
>            long max=0;
>            long h=0;
>            for(int j=0;j<n;j++)
>            {
>                if(visited[j]==false)
>                h=dfs(j,visited,adj,a);
>                
>                if(h>max)
>                max=h;
>               // System.out.println("h is "+h);
>            }
>            System.out.println(max);
>        }
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/kingdom%20of%20monkey%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/kingdom of monkey q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/kingdom%20of%20monkey%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/kingdom of monkey s.txt
