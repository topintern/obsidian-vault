---
kind: "coding-problem"
title: "BOTTOM"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/bottom q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/bottom s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# BOTTOM

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

We will use the following (standard) definitions from graph theory. Let V be a non-empty and finite set, its elements being called vertices (or nodes). Let E be a subset of the Cartesian product V×V, its elements being called edges. Then G=(V,E) is called a directed graph.

Let n be a positive integer, and let p=(e1,…,en) be a sequence of length n of edges ei?E such that ei=(vi,vi+1)for a sequence of vertices (v1,…,vn+1). Then p is called a path from vertex v1 to vertex vn+1 in G and we say that vn+1 is reachable from v1, writing (v1?vn+1).

Here are some new definitions. A node v in a graph G=(V,E) is called a sink, if for every node w in G that is reachable from v, v is also reachable from w. The bottom of a graph is the subset of all nodes that are sinks, i.e., bottom(G)={v?V|?w?V:(v?w)?(w?v)}. You have to calculate the bottom of certain graphs.
Input Specification
The input contains several test cases, each of which corresponds to a directed graph G. Each test case starts with an integer number v, denoting the number of vertices of G=(V,E) where the vertices will be identified by the integer numbers in the set V={1,…,v}. You may assume that 1=v=5000. That is followed by a non-negative integer e and, thereafter, e pairs of vertex identifiers v1,w1,…,ve,we with the meaning that (vi,wi)?E. There are no edges other than specified by these pairs. The last test case is followed by a zero.
Output Specification
For each test case output the bottom of the specified graph on a single line. To this end, print the numbers of all nodes that are sinks in sorted order separated by a single space character. If the bottom is empty, print an empty line.

### Sample Input

```text
3 3
1 3 2 3 3 1
2 1
1 2
0
```

### Sample Output

```text
1 3
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · bottom s.txt
> ```cpp
> #include <cstdio>
> #include <vector>
> #include <queue>
>
> #define MAXN 5000
>
> using namespace std;
>
> vector< int > graph[ MAXN + 1 ], graphT[ MAXN + 1 ], sorted;
> bool visited[ MAXN + 1 ];
> int comp[ MAXN + 1 ], sol[ MAXN + 1 ];
> int N, M;
>
> void init( int N ) {
>     for ( int i = 0; i <= N; ++i ) {
>         graph[ i ].clear();
>         graphT[ i ].clear();
>         visited[ i ] = false;
>     }
> 	sorted.clear();
> }
>
> void dfs1( int S ) {
>     visited[ S ] = true;
>     int i;
>     for ( i = 0; i < graph[ S ].size(); ++i ) {
>         if ( !visited[ graph[ S ][ i ] ] ) {
>             dfs1( graph[ S ][ i ] );
>         }
>     }
>     sorted.push_back( S );
> }
>
> void dfs2( int S, int c ) {
>     visited[ S ] = false;
>     comp[ S ] = c;
>     int i;
>     for ( i = 0; i < graphT[ S ].size(); ++i ) {
>         if ( visited[ graphT[ S ][ i ] ] ) {
>             dfs2( graphT[ S ][ i ], c );
>         }
>     }
> }
>
> int main() {
>     int i, j, u, v, compon;
>     while ( 1 ) {
>         scanf( "%d", &N );
>         if ( N == 0 ) {
>             break;
>         }
>         scanf( "%d", &M );
>         init( N );
>         for ( i = 0; i < M; ++i ) {
>             scanf( "%d%d", &u, &v );
>             graph[ u ].push_back( v );
>             graphT[ v ].push_back( u );
>         }
>         for ( i = 1; i <= N; ++i ) {
>             if ( !visited[ i ] ) {
>                 dfs1( i );
>             }
>         }
>         compon = 0;
>         for ( i = sorted.size() - 1; i >= 0; --i ) {
>             if ( visited[ sorted[ i ] ] ) {
>                 dfs2( sorted[ i ], compon++ );
>                 sol[ compon - 1 ] = true;
>             }
>         }
>         for ( i = 1; i <= N; ++i ) {
>             for ( j = 0; j < graph[ i ].size(); ++j ) {
>                 if ( comp[ i ] != comp[ graph[ i ][ j ] ] ) {
>                     sol[ comp[ i ] ] = false;
>                     break;
>                 }
>             }
>         }
>         for ( i = 1; i <= N; ++i ) {
>             if ( sol[ comp[ i ] ] ) {
>                 printf( "%d ", i );
>             }
>         }
>         printf( "\n" );
>     }
>     
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/bottom%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/bottom q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/bottom%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/bottom s.txt
