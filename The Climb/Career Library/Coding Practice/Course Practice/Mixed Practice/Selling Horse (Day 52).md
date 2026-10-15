---
kind: "coding-problem"
title: "Selling Horse (Day 52)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/SellingHorse.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Selling Horse (Day 52)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Ameeta Mehra owns S horses. He wants to keep only horses that can run very fast. 
He decides which horses are fast by making them race against each other. 
If a horse comes in last, then Ameeta Mehra will sell it.

The race course consists of N checkpoints and E roads. Ameeta Mehra positions his horses at 
the first S checkpoints i.e., checkpoints 1 to S. The checkpoint N is chosen as the finish line. 
The horses need 1 unit of time to cross one road. 
If the horses have two or more paths to choose, then they choose the one which is shortest. 
The horses start the race at the same instant. When a horse reaches checkpoint N, it finishes 
the race.

Find the total number of horses that Ameeta Mehra will sell i.e., the number of horses that come 
in last.

NOTE : The roads are bidirectional.

Input Format:
-------------
The first line of the input consists of S (the number of horses), N (the number of checkpoints) 
and E (the number of roads) Each of the next E lines contains a and b, indicating that there is 
a road between checkpoints a and b.

Output Format:
--------------
Print a single integer, the number horses that come in last.


### Constraints

-----------
1 ≤ S < N ≤ 300000
1 ≤ E ≤ 300000
1 ≤ a , b ≤ N


### Sample Input

3 5 4
1 5
2 4
3 4
5 4


### Sample Output

2

Explanation

There are 3 horses, each starting at checkpoint 1, 2 and 3 respectively. 
Checkpoint 5 is the finish line. The horse starting at checkpoint 1 finishes the race first, 
in 1 unit of time. The horses at 2 and 3 come in last and finish the race at the same instant. 
Hence, Ameeta Mehra will sell 2 horses.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SellingHorse.txt
> ```java
> /*
>  * 
> Ameeta Mehra owns S horses. He wants to keep only horses that can run very fast. 
> He decides which horses are fast by making them race against each other. 
> If a horse comes in last, then Ameeta Mehra will sell it.
>
> The race course consists of N checkpoints and E roads. Ameeta Mehra positions his horses at 
> the first S checkpoints i.e., checkpoints 1 to S. The checkpoint N is chosen as the finish line. 
> The horses need 1 unit of time to cross one road. 
> If the horses have two or more paths to choose, then they choose the one which is shortest. 
> The horses start the race at the same instant. When a horse reaches checkpoint N, it finishes 
> the race.
>
> Find the total number of horses that Ameeta Mehra will sell i.e., the number of horses that come 
> in last.
>
> NOTE : The roads are bidirectional.
>
> Input Format:
> -------------
> The first line of the input consists of S (the number of horses), N (the number of checkpoints) 
> and E (the number of roads) Each of the next E lines contains a and b, indicating that there is 
> a road between checkpoints a and b.
>
> Output Format:
> --------------
> Print a single integer, the number horses that come in last.
>
> Constraints
> -----------
> 1 ≤ S < N ≤ 300000
> 1 ≤ E ≤ 300000
> 1 ≤ a , b ≤ N
>
> Sample Input:
> 3 5 4
> 1 5
> 2 4
> 3 4
> 5 4
>
> Sample Output:
> 2
>
> Explanation
>
> There are 3 horses, each starting at checkpoint 1, 2 and 3 respectively. 
> Checkpoint 5 is the finish line. The horse starting at checkpoint 1 finishes the race first, 
> in 1 unit of time. The horses at 2 and 3 come in last and finish the race at the same instant. 
> Hence, Ameeta Mehra will sell 2 horses.
>
>  * 
>  */
>
> import java.io.*;
> import java.util.*;
> public class SellingHorse 
> {
>     
>     static ArrayList<Integer> adj[];
>
>     public static void main(String args[]) throws IOException {
>         Scanner sc=new Scanner(System.in);
>         int S = sc.nextInt();
>         int N = sc.nextInt();
>         int E = sc.nextInt();
>         adj = new ArrayList[N+1];
>         visited = new boolean[N+1];
>         dis = new int[N+1];
>         for (int i = 0 ; i< N+1; i++){
>             adj[i] = new ArrayList<>();
>         }
>         for (int i = 0 ;i < E; i++){
>             int x = sc.nextInt();
>             int y = sc.nextInt();
>             adj[x].add(y);
>             adj[y].add(x);
>         }
>         bfs(N);
>         int max = Integer.MIN_VALUE;
>         for (int i = 1; i <= S; i++){
>             if (dis[i] > max)
>                 max = dis[i];
>         }
>         
>         int c = 0;
>         for (int i = 1; i <= S; i++){
>             if (dis[i] == max)
>                 c++;
>         }
>         System.out.println(c);
>     }
>     static boolean visited[];
>     static int dis[];
>     public static void bfs(int n){
>         LinkedList<Integer> queue = new LinkedList<>();
>         queue.add(n);
>         visited[n] = true;
>         while (!queue.isEmpty()){
>             int f = queue.poll();
>             for (int i = 0; i < adj[f].size(); i++){
>                 int x = adj[f].get(i);
>                 if (!visited[x]){
>                     visited[x] = true;
>                     queue.add(x);
>                     dis[x] = dis[f] + 1;
>                 }
>             }
>         }
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2052%20Solutions/SellingHorse.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/SellingHorse.txt
