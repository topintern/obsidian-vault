---
kind: "coding-problem"
title: "Failing Phobia (Day 52)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/FailingPhobia.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Failing Phobia (Day 52)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Tyrion has recently qualified for Google's CodeJAM, 
and he can't keep his excitement with himself and share this news with 'K' of his friends.

One day Scrolling on Instagram Tyrion find a quote written :
 "The more the people knows, the more is the chances of FAILURE.", 
Now reading this he is scared and fears what if it will become true. 
However, he is well prepared for Google's CodeJAM even though he wants to 
find the number of peoples who had by now known the news.

Tyrion knows his friends and his friends friend (and so on) very well, 
he knows that his friends will share this news to every friend who has friendship strength ≤ 'S'.

You are given the graph representing the friendship and the friendship strength, 
find the number of peoples who knows this news. 

The graph can also be disconnected.

Input Format:
------------
    1st line:
    N M (N = No of total friends, M = total no of friendship bonds)
    Next M Lines contains 3 integers: a,b,c representing a and b are both friends with friendship strength of c.
    K S (K = no of friends with whom Tyrion shared the news, S = mentioned above)
    Next K space separated integers representing the friends whom Tyrion shared the news.
    k1,k2.....kk.
    
    
Output Format:
--------------
    Single Integer representing the number of friends who by now knows a news.



### Constraints

-----------
1≤N≤ 100,000 M≤min(123456, N(N-1)/2), K≤ N, S≤ 1000000000
1≤a,b≤N, 1≤c≤1000000000
Ki ≤ N


### Sample Input

5 5
1 2 6
1 3 3
2 3 2
3 4 6
3 5 5
2 5
1 5


### Sample Output

4

QUICK EXPLANATION:
-----------------
Run a DFS from each reachable node. 
If any neighbour has edge weight ≤S, 
it is reachable and run a DFS from it. 
Maintain a visited array so that you visit each node utmost once. 
Print the number of nodes that were visited.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FailingPhobia.txt
> ```java
> /*
>  * 
> Tyrion has recently qualified for Google's CodeJAM, 
> and he can't keep his excitement with himself and share this news with 'K' of his friends.
>
> One day Scrolling on Instagram Tyrion find a quote written :
>  "The more the people knows, the more is the chances of FAILURE.", 
> Now reading this he is scared and fears what if it will become true. 
> However, he is well prepared for Google's CodeJAM even though he wants to 
> find the number of peoples who had by now known the news.
>
> Tyrion knows his friends and his friends friend (and so on) very well, 
> he knows that his friends will share this news to every friend who has friendship strength ≤ 'S'.
>
> You are given the graph representing the friendship and the friendship strength, 
> find the number of peoples who knows this news. 
>
> The graph can also be disconnected.
>
> Input Format:
> ------------
>     1st line:
>     N M (N = No of total friends, M = total no of friendship bonds)
>     Next M Lines contains 3 integers: a,b,c representing a and b are both friends with friendship strength of c.
>     K S (K = no of friends with whom Tyrion shared the news, S = mentioned above)
>     Next K space separated integers representing the friends whom Tyrion shared the news.
>     k1,k2.....kk.
>     
>     
> Output Format:
> --------------
>     Single Integer representing the number of friends who by now knows a news.
>
>
> Constraints
> -----------
> 1≤N≤ 100,000 M≤min(123456, N(N-1)/2), K≤ N, S≤ 1000000000
> 1≤a,b≤N, 1≤c≤1000000000
> Ki ≤ N
>
> Sample Input:
> 5 5
> 1 2 6
> 1 3 3
> 2 3 2
> 3 4 6
> 3 5 5
> 2 5
> 1 5
>
> Sample Output:
> 4
>
> QUICK EXPLANATION:
> -----------------
> Run a DFS from each reachable node. 
> If any neighbour has edge weight ≤S, 
> it is reachable and run a DFS from it. 
> Maintain a visited array so that you visit each node utmost once. 
> Print the number of nodes that were visited.
>
>  * 
>  * 
>  */
> import java.io.IOException;
> import java.util.ArrayList;
> import java.util.List;
> import java.util.Scanner;
>
> public class FailingPhobia {
>     List<int[]>[] graph;
>     int N;
>     int M;
>     boolean[] visited;
>     int total_number;
>     int S;
>
>     public FailingPhobia(int N, int M){
>         this.N = N;
>         this.M = M;
>         this.graph = new ArrayList[N];
>         for(int i = 0; i< N; i++){
>             this.graph[i] = new ArrayList<int[]>();
>         }
>         this.visited = new boolean[N];
>         this.total_number = 0;
>     }
>
>     public void create_entry(int friend1, int friend2, int strength){
>         int index_friend1 = friend1-1;
>         int index_friend2 = friend2-1;
>         int[] pair12 = {strength, index_friend2};
>         int[] pair21 = {strength, index_friend1};
>         this.graph[index_friend1].add(pair12);
>         this.graph[index_friend2].add(pair21);
>     }
>
>     public void traversal_modified(int friend){
>         if(this.visited[friend]){
>             return;
>         }
>       
>         this.visited[friend] = true;
>         this.total_number = this.total_number + 1;
>         for(int[] path_friend: this.graph[friend]){
>             
>             if(path_friend[0] <= this.S){
>                // System.out.print(path_friend[1]+" ");
>                 traversal_modified(path_friend[1]);
>             }
>         }
>     }
>
>     public static void main(String[] args) throws IOException {
>         
>         Scanner sc = new Scanner(System.in);
>         int N = sc.nextInt();
>         int M = sc.nextInt();
>         FailingPhobia fp = new FailingPhobia(N, M);
>         for(int relation=0; relation<M; relation++){
>           
>             int friend1 = sc.nextInt();
>             int friend2 = sc.nextInt();
>             int strength = sc.nextInt();
>             fp.create_entry(friend1, friend2, strength);
>         }
>         
>         int K = sc.nextInt();
>         int S = sc.nextInt();
>         fp.S = S;
>         
>         for(int i =0; i<K; i++){
>         	fp.traversal_modified(sc.nextInt() - 1);
>         }
>         System.out.println(fp.total_number);
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2052%20Solutions/FailingPhobia.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/FailingPhobia.txt
