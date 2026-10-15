---
kind: "coding-problem"
title: "Storyof Tree (Day 81)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/StoryofTree.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Storyof Tree (Day 81)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
-------------
    - The first line contains an integer N, denoting the number of nodes in the tree.

    - next 'N-1' lines contain two space-separated integers, s and e , 
      defining an undirected edge between nodes s and e .

    - Next line contains two space-separated integers p and q
      describing the respective values of p (thenumber of guesses) 
      and q (the minimum score needed to win).

    - Next 'p' lines contains two space-separated integers, s and e,
    indicating guesses parent(e)=s.


Output Format :
	- Print the probability as a reduced fraction in the format m/n .

Note: Print 0/1 if the probability is 0 and print 1/1 if the probability is 1.



### Sample Input 

4
1 2
1 3
3 4
2 2
1 2
3 4


### Sample Output 

1/2




### Sample Input 

3
1 2
1 3
2 2
1 2
1 3


### Sample Output 

1/3
**********Testcases***********
case =1
input =4
1 2
1 3
3 4
2 2
1 2
3 4
output =1/2

case =2
input =3
1 2
1 3
2 2
1 2
1 3
output =1/3

case =3
input =5
1 2
2 3
3 4
4 5
1 3
1 4
output =0/1



case =4
input =4
1 2
1 3
1 4
3 3
1 2
1 3
1 4
output =1/4


case =5
input =5
1 2
1 3
1 4
1 5
2 2
1 2
1 3
output =3/5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StoryofTree.txt
> ```java
> /*
> Input Format:
> -------------
>     - The first line contains an integer N, denoting the number of nodes in the tree.
>
>     - next 'N-1' lines contain two space-separated integers, s and e , 
>       defining an undirected edge between nodes s and e .
>
>     - Next line contains two space-separated integers p and q
>       describing the respective values of p (thenumber of guesses) 
>       and q (the minimum score needed to win).
>
>     - Next 'p' lines contains two space-separated integers, s and e,
>     indicating guesses parent(e)=s.
>
>
> Output Format :
> 	- Print the probability as a reduced fraction in the format m/n .
>
> Note: Print 0/1 if the probability is 0 and print 1/1 if the probability is 1.
>
>
> Sample Input :
> 4
> 1 2
> 1 3
> 3 4
> 2 2
> 1 2
> 3 4
>
> Sample Output :
> 1/2
>
>
>
> Sample Input :
> 3
> 1 2
> 1 3
> 2 2
> 1 2
> 1 3
>
> Sample Output :
> 1/3
>
>
> ***********Testcases***********
> case =1
> input =4
> 1 2
> 1 3
> 3 4
> 2 2
> 1 2
> 3 4
> output =1/2
>
> case =2
> input =3
> 1 2
> 1 3
> 2 2
> 1 2
> 1 3
> output =1/3
>
> case =3
> input =5
> 1 2
> 2 3
> 3 4
> 4 5
> 1 3
> 1 4
> output =0/1
>
>
>
> case =4
> input =4
> 1 2
> 1 3
> 1 4
> 3 3
> 1 2
> 1 3
> 1 4
> output =1/4
>
>
> case =5
> input =5
> 1 2
> 1 3
> 1 4
> 1 5
> 2 2
> 1 2
> 1 3
> output =3/5
>
> */
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class TreeStory {
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         
>             int n = in.nextInt();
>             ArrayList<ArrayList<Integer>> neigh = new ArrayList<ArrayList<Integer>>();
>             ArrayList<HashSet<Integer>> down = new ArrayList<HashSet<Integer>>();
>             for (int i = 0; i < n; i++) {
>                 neigh.add(new ArrayList<Integer>());
>                 down.add(new HashSet<Integer>());
>             }
>             for(int a1 = 0; a1 < n-1; a1++){
>                 int u = in.nextInt()-1;
>                 int v = in.nextInt()-1;
>                 neigh.get(u).add(v);
>                 neigh.get(v).add(u);
>             }
>             int g = in.nextInt();
>             int k = in.nextInt();
>             for(int a1 = 0; a1 < g; a1++){
>                 int u = in.nextInt()-1;
>                 int v = in.nextInt()-1;
>                 down.get(u).add(v);
>             }
>             int[] correct = new int[n];
>             ArrayDeque<Integer> qu = new ArrayDeque<Integer>();
>             qu.add(0);
>             boolean[] vis = new boolean[n];
>             vis[0] = true;
>             while (!qu.isEmpty()) {
>                 int u = qu.removeFirst();
>                 for (int v : neigh.get(u)) {
>                     if(!vis[v]) {
>                         vis[v] = true;
>                         if (down.get(u).contains(v))
>                             correct[0]++;
>                         qu.add(v);
>                     }
>                 }
>             }
>             qu.add(0);
>             vis = new boolean[n];
>             vis[0] = true;
>             while (!qu.isEmpty()) {
>                 int u = qu.removeFirst();
>                 for (int v : neigh.get(u)) {
>                     if(!vis[v]) {
>                         vis[v] = true;
>                         correct[v] = correct[u];
>                         if (down.get(u).contains(v))
>                             correct[v]--;
>                         if (down.get(v).contains(u))
>                             correct[v]++;
>                         qu.add(v);
>                     }
>                 }
>             }
>             int ansNum = 0;
>             for (int i = 0; i < n; i++) {
>                 if (correct[i] >= k)
>                     ansNum++;
>             }
>             int gcd = gcd(ansNum, n);
>             System.out.println(ansNum/gcd+"/"+n/gcd);
>     
>     }
>     
>     public static int gcd(int a, int b) {
>         if (a==0)
>             return b;
>         if (a > b)
>             return gcd(b,a);
>         return gcd(b%a, a);
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2081%20Solution/StoryofTree.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/StoryofTree.txt
