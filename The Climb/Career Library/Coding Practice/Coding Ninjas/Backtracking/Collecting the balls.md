---
kind: "coding-problem"
title: "Collecting the balls"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/collecting balls q.txt","CODING RESOURCES/coding ninjas/2.backtrack/collecting balls s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Collecting the balls

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

There are ‘n’ number of balls in a container. Mr. Sharma and Singh want to take balls out from the container. At each step, Mr. Sharma took ‘k’ balls out of the box and Mr. Singh took one-tenth of the remaining balls. Suppose there are 29 balls at the moment and k=4. Then, Mr. Sharma will take 4 balls and Mr. Singh will take 2 balls (29-4 = 25; 25/10 = 2). If there are less than ‘k’ balls remaining at some moment, then Mr. Sharma will take all the balls which will get the container empty. The process will last until the container becomes empty. Your task is to choose minimal ‘k’ for Mr. Sharma such that Mr. Sharma will take at least half of the balls from the container.

### Input Format

The Only line of input contains a single integer ‘n’.

### Output Format

Print a single integer denoting the minimal value of ‘k’.

### Constraints

1 <= n <= 10^18
Time Limit: 1 second

### Sample Input

```text
68
```

### Sample Output

```text
3
```

### Explanation

68-3 = 65; 65/10 = 6; 65-6 = 59
59-3 = 56; 56/10 = 5; 56-5 = 51
51-3 = 48; 48/10 = 4; 48-4 = 44
44-3 = 41; 41/10 = 4; 41-4 = 37
…..
…..
…..
6-3 = 3; 3/10 = 0; 3-0 = 3
3-3 = 0; 0/10 = 0; 0-0 = 0

> [!tip] Cross-topic study
> The source stores this under Backtracking, but its reference uses an answer-space binary search (`bsearch`) with a feasibility simulation (`find`). Also study [[The Climb/Career Library/Coding Practice/Coding Ninjas/Search and Sort/Search and Sort Study Guide|Search and Sort]].


## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · collecting balls s.txt
> ```java
> import java.io.IOException;
> import java.util.*;
>
> public class Main {
> 	static FasterScanner in = new FasterScanner();
> 	static boolean find(long cur, long k){
> 		long sum=0, n = cur;
> 		while(n>0){
> 			long add = Math.min(k, n);
> 			sum+=add;
> 			n-=add;
> 			n-=(n/10);
> 		}
> 		return 2*sum>=cur;
> 	}
> 	static long bsearch(long n){
> 		long ret=n/2, lo=1, hi=n;
> 		while(lo<=hi){
> 			long mid = (lo+hi)/2;
> 			if(find(n, mid)){
> 				ret=mid;
> 				hi=mid-1;
> 			}else{
> 				lo=mid+1;
> 			}
> 		}
> 		return ret;
> 	}
> 	public static void main(String[] args)throws Exception {
> 		long n = in.nextLong();
> 		System.out.println(bsearch(n));
> 	}
>
> 	static class FasterScanner {
> 		private byte[] buf = new byte[1024];
> 		private int curChar;
> 		private int snumChars;
>
> 		public int read() {
> 			if (snumChars == -1)
> 				throw new InputMismatchException();
> 			if (curChar >= snumChars) {
> 				curChar = 0;
> 				try {
> 					snumChars = System.in.read(buf);
> 				} catch (IOException e) {
> 					throw new InputMismatchException();
> 				}
> 				if (snumChars <= 0)
> 					return -1;
> 			}
> 			return buf[curChar++];
> 		}
>
> 		public String nextLine() {
> 			int c = read();
> 			while (isSpaceChar(c))
> 				c = read();
> 			StringBuilder res = new StringBuilder();
> 			do {
> 				res.appendCodePoint(c);
> 				c = read();
> 			} while (!isEndOfLine(c));
> 			return res.toString();
> 		}
>
> 		public String nextString() {
> 			int c = read();
> 			while (isSpaceChar(c))
> 				c = read();
> 			StringBuilder res = new StringBuilder();
> 			do {
> 				res.appendCodePoint(c);
> 				c = read();
> 			} while (!isSpaceChar(c));
> 			return res.toString();
> 		}
>
> 		public long nextLong() {
> 			int c = read();
> 			while (isSpaceChar(c))
> 				c = read();
> 			int sgn = 1;
> 			if (c == '-') {
> 				sgn = -1;
> 				c = read();
> 			}
> 			long res = 0;
> 			do {
> 				if (c < '0' || c > '9')
> 					throw new InputMismatchException();
> 				res *= 10;
> 				res += c - '0';
> 				c = read();
> 			} while (!isSpaceChar(c));
> 			return res * sgn;
> 		}
>
> 		public int nextInt() {
> 			int c = read();
> 			while (isSpaceChar(c))
> 				c = read();
> 			int sgn = 1;
> 			if (c == '-') {
> 				sgn = -1;
> 				c = read();
> 			}
> 			int res = 0;
> 			do {
> 				if (c < '0' || c > '9')
> 					throw new InputMismatchException();
> 				res *= 10;
> 				res += c - '0';
> 				c = read();
> 			} while (!isSpaceChar(c));
> 			return res * sgn;
> 		}
>
> 		public int[] nextIntArray(int n) {
> 			int[] arr = new int[n];
> 			for (int i = 0; i < n; i++) {
> 				arr[i] = nextInt();
> 			}
> 			return arr;
> 		}
>
> 		public long[] nextLongArray(int n) {
> 			long[] arr = new long[n];
> 			for (int i = 0; i < n; i++) {
> 				arr[i] = nextLong();
> 			}
> 			return arr;
> 		}
>
> 		private boolean isSpaceChar(int c) {
> 			return c == ' ' || c == '\n' || c == '\r' || c == '\t' || c == -1;
> 		}
>
> 		private boolean isEndOfLine(int c) {
> 			return c == '\n' || c == '\r' || c == -1;
> 		}
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/collecting%20balls%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/collecting balls q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/collecting%20balls%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/collecting balls s.txt
