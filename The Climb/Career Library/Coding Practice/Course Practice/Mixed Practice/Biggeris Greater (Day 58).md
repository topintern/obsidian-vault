---
kind: "coding-problem"
title: "Biggeris Greater (Day 58)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 58 Solutions/BiggerisGreater.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Biggeris Greater (Day 58)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Lexicographical order is often known as alphabetical order when dealing with strings. 
A string is greater than another string if it comes later in a lexicographically sorted list.

Given a word, create a new word by swapping some or all of its characters. 
This new word must meet two criteria:
	- It must be greater than the original word
	- It must be the smallest word that meets the first condition
For example, given the word "abcd", the next largest word is "abdc".

Input Format:
The first line of input contains a string (without spaces and contains lowercase alphabets).
Output Format:
For each test case, output the string meeting the criteria. 
If no answer exists, print "no answer".


### Sample Input 

	dhck

### Sample Output 

	dhkc

### Explanation 

	dhkc is the next string greater than dhck.


### Sample Input

	fedcbabcd
Sample Output 1
	fedcbabdc

========= Testcases Program-1 =========
case =1
input =dhck
output ="dhkc"

case =2
input =fedcbabcd
output ="fedcbabdc"

case =3
input =zyyyvvvvvuttsrqqokjjheedccb
output ="no answer"

case =4
input =chntqzcpvrhvzvpywuhxombxcsjlpsergz
output ="chntqzcpvrhvzvpywuhxombxcsjlpserzg"

case =5
input =bvulomthrfugqfbaknxginokekuemgb
output ="bvulomthrfugqfbaknxginokekugbem"

case =6
input =phoatpygffol
output ="phoatpygflfo"

case =7
input =dkuwfemegcc
output ="dkuwfemgcce"

case =8
input =bdmkhyleclldykvysxkfttkipzdmkexxhmdtdabxjzuxgyvlzyhebe
output ="bdmkhyleclldykvysxkfttkipzdmkexxhmdtdabxjzuxgyvlzyheeb"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BiggerisGreater.txt
> ```java
> /*
> Lexicographical order is often known as alphabetical order when dealing with strings. 
> A string is greater than another string if it comes later in a lexicographically sorted list.
>
> Given a word, create a new word by swapping some or all of its characters. 
> This new word must meet two criteria:
> 	- It must be greater than the original word
> 	- It must be the smallest word that meets the first condition
> For example, given the word "abcd", the next largest word is "abdc".
>
> Input Format:
> The first line of input contains a string (without spaces and contains lowercase alphabets).
> Output Format:
> For each test case, output the string meeting the criteria. 
> If no answer exists, print "no answer".
>
> Sample Input :
> 	dhck
> Sample Output :
> 	dhkc
> Explanation :
> 	dhkc is the next string greater than dhck.
>
> Sample Input:
> 	fedcbabcd
> Sample Output 1
> 	fedcbabdc
>
> ========= Testcases Program-1 =========
> case =1
> input =dhck
> output ="dhkc"
>
> case =2
> input =fedcbabcd
> output ="fedcbabdc"
>
> case =3
> input =zyyyvvvvvuttsrqqokjjheedccb
> output ="no answer"
>
> case =4
> input =chntqzcpvrhvzvpywuhxombxcsjlpsergz
> output ="chntqzcpvrhvzvpywuhxombxcsjlpserzg"
>
> case =5
> input =bvulomthrfugqfbaknxginokekuemgb
> output ="bvulomthrfugqfbaknxginokekugbem"
>
> case =6
> input =phoatpygffol
> output ="phoatpygflfo"
>
> case =7
> input =dkuwfemegcc
> output ="dkuwfemgcce"
>
> case =8
> input =bdmkhyleclldykvysxkfttkipzdmkexxhmdtdabxjzuxgyvlzyhebe
> output ="bdmkhyleclldykvysxkfttkipzdmkexxhmdtdabxjzuxgyvlzyheeb"
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class BiggerisGreater {
>
>     public static void main(String args[])
>     {
>     	Scanner s=new Scanner(System.in);
>     	int testCAses=s.nextInt();
>     	lable:
>     	{
>     		char c[]=s.nextLine().toCharArray();
>     		for(int j=c.length-2;j>=0;j--)
>     		{
>     			for(int k=c.length-1;k>j;k--)
>     			{
>     				if(c[j]<c[k])
>     				{
>     					char t=c[j];
>     					c[j]=c[k];
>     					c[k]=t;
>     					Arrays.sort(c, j+1, c.length);
>     					System.out.println(new S
> 						tring(c));
>     					break lable;
>     					
>     				}
>     			}
>     		}
>     		System.out.println("no answer");
>     	}
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2058%20Solutions/BiggerisGreater.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 58 Solutions/BiggerisGreater.txt
