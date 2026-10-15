---
kind: "coding-problem"
title: "String Similarity (Day 80)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 80 Solutions/StringSimilarity.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# String Similarity (Day 80)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Sample Input

ababaa  

Sample Output

11  




### Explanation :


For the first case, the suffixes of the string are "ababaa", "babaa", "abaa", "baa", "aa" and "a". The similarities of these strings with the string "ababaa" are 6,0,3,0,1, & 1 respectively. 

Thus, the answer is 6 + 0 + 3 + 0 + 1 + 1 = 11.


Sample Input
aa

Sample Output
3

the answer is 2 + 1 = 3.


case =1
input =ababazx
output =11

case =2
input =ddd
output =6

case =3
input =abababzcz
output =15

case =4
input =zxcvbnm
output =7

case =5
input =zzzxcvbnm
output =12

case =6
input =aaabbbcccdddeee
output =18

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StringSimilarity.java
> ```java
> /*
>
>
>
>
> Sample Input
>
> ababaa  
>
> Sample Output
>
> 11  
>
>
>
> Explanation :
>
> For the first case, the suffixes of the string are "ababaa", "babaa", "abaa", "baa", "aa" and "a". The similarities of these strings with the string "ababaa" are 6,0,3,0,1, & 1 respectively. 
>
> Thus, the answer is 6 + 0 + 3 + 0 + 1 + 1 = 11.
>
>
> Sample Input
> aa
>
> Sample Output
> 3
>
> the answer is 2 + 1 = 3.
>
>
> case =1
> input =ababazx
> output =11
>
> case =2
> input =ddd
> output =6
>
> case =3
> input =abababzcz
> output =15
>
> case =4
> input =zxcvbnm
> output =7
>
> case =5
> input =zzzxcvbnm
> output =12
>
> case =6
> input =aaabbbcccdddeee
> output =18
>
> */
>
>
> import java.util.Scanner;
>
>  class StringSimilarity
> {
>
>         public static void main(String[] args)throws Exception
>         {
>         
>             Scanner cin=new Scanner(System.in);
>         
>           
>                 String str=cin.nextLine();
>                 char arr[]=str.toCharArray();
>     		int N=str.length();
>     		int Z[]=new int[N];
>     		char s[]=str.toCharArray();
>     		Z[0] = N;  
>     		long sum=0;
>     		sum=N;
>     		int a = 0, b = 0;
>
>     		for (int i = 1; i < N; ++i)
>     		 {
>      		     int k = i < b ? Math.min(b - i, Z[i - a]) : 0;
>      			while (i + k < N && s[i + k] == s[k]) ++k;
>      			Z[i] = k;
>      			sum+=k;
>      			if (i + k > b) { 
> 			a = i; b = i + k; 
> 			}
>     		 }
>                 System.out.println(sum);
>             
>             
>         cin.close();
>             
>         }
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2080%20Solutions/StringSimilarity.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 80 Solutions/StringSimilarity.java
