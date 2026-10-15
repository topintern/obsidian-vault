---
kind: "coding-problem"
title: "Minimum Count"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/min count q.txt","CODING RESOURCES/coding ninjas/Dp-1/min count s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Minimum Count

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an integer N, find and return the count of minimum numbers, sum of whose squares is equal to N.
That is, if N is 4, then we can represent it as : {1^2 + 1^2 + 1^2 + 1^2} and {2^2}. Output will be 1, as 1 is the minimum count of numbers required.
Note : x^y represents x raise to the power y.

### Input Format

Integer N

### Output Format

Required minimum count

### Constraints

1 <= N <= 1000

### Sample Input 1

```text
12
```

### Sample Output 1

```text
3
Sample Output 1 Explanation :
12 can be represented as :
1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1
1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 1^1 + 2^2
1^1 + 1^1 + 1^1 + 1^1 + 2^2 + 2^2
2^2 + 2^2 + 2^2
As we can see, the output should be 3.
```

### Sample Input 2

```text
9
```

### Sample Output 2

```text
1
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · min count s.txt
> ```cpp
> #include<algorithm>
> int minCount(int n) {
> 	// count[i] - represents minimum count of squares for integer n
> 		if(n <= 3) {
> 			return n;
> 		}
> 		int count[n+1] ;
> 		count[0] = 0;
> 		count[1] = 1;
> 		count[2] = 2;
> 		count[3] = 3;
> 		
> 		for(int i = 4; i <= n; i++) {
> 			int ans = i;	
> 			for(int j = 1; j <= i/2; j++) {
> 				int k = i - (j * j);
> 				if(k >= 0)
> 					ans = min(ans, count[k] + 1);
> 			}
> 			count[i] = ans;
> 		}
> 		return count[n];
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/min%20count%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/min count q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/min%20count%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/min count s.txt
