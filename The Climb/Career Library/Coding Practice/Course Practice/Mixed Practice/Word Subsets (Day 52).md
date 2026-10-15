---
kind: "coding-problem"
title: "Word Subsets (Day 52)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/WordSubsets.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Word Subsets (Day 52)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

We are given two arrays A and B of words.  Each word is a string of lowercase letters.

Now, say that word b is a subset of word a if every letter in b occurs in a, including multiplicity.  
For example, "wrr" is a subset of "warrior", but is not a subset of "world".

Now say a word 'a' from A is universal if for every 'b' in B, 'b' is a subset of 'a'. 

Return a list of all universal words in A.  You can return the words in alphabetical order.

 
Sample Input 1:
leoc amazon apple facebook google 
lo eo

Sample Output 1: 
google leoc


Sample Input 2: 
amazon apple facebook google leoc
ec oc ceo

Sample Output 2: 
facebook leoc
 

Note:
1 <= A.length, B.length <= 10000
1 <= A[i].length, B[i].length <= 10
A[i] and B[i] consist only of lowercase letters.
All words in A[i] are unique: there isn't i != j with A[i] == A[j].

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · WordSubsets.txt
> ```java
> /*
>  * 
> We are given two arrays A and B of words.  Each word is a string of lowercase letters.
>
> Now, say that word b is a subset of word a if every letter in b occurs in a, including multiplicity.  
> For example, "wrr" is a subset of "warrior", but is not a subset of "world".
>
> Now say a word 'a' from A is universal if for every 'b' in B, 'b' is a subset of 'a'. 
>
> Return a list of all universal words in A.  You can return the words in alphabetical order.
>
>  
> Sample Input 1:
> leoc amazon apple facebook google 
> lo eo
>
> Sample Output 1: 
> google leoc
>
>
> Sample Input 2: 
> amazon apple facebook google leoc
> ec oc ceo
>
> Sample Output 2: 
> facebook leoc
>  
>
> Note:
> 1 <= A.length, B.length <= 10000
> 1 <= A[i].length, B[i].length <= 10
> A[i] and B[i] consist only of lowercase letters.
> All words in A[i] are unique: there isn't i != j with A[i] == A[j].
>
>  * 
>  */
>  import java.io.*;
> import java.util.*;
> public class WordSubsets {
>
> 	public static List<String> wordSubsets(String[] A, String[] B) {
>         int[] bmax = count("");
>         for (String b: B) {
>             int[] bCount = count(b);
>             for (int i = 0; i < 26; ++i)
>                 bmax[i] = Math.max(bmax[i], bCount[i]);
>         }
>
>         List<String> ans = new ArrayList();
>         search: for (String a: A) {
>             int[] aCount = count(a);
>             for (int i = 0; i < 26; ++i)
>                 if (aCount[i] < bmax[i])
>                     continue search;
>             ans.add(a);
>         }
>
>         return ans;
>     }
>
>     public static int[] count(String S) {
>         int[] ans = new int[26];
>         for (char c: S.toCharArray())
>             ans[c - 'a']++;
>         return ans;
>     }
> 	public static void main(String args[]) throws IOException {
> 		
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String strA = br.readLine();
> 		String[] wordsA = strA.split(" ");
> 		
> 		String strB = br.readLine();
> 		String[] wordsB = strB.split(" ");
>
> 		List<String> wordSubsets = wordSubsets(wordsA, wordsB);
> 		Collections.sort(wordSubsets);
> 		wordSubsets.stream().forEach(s -> System.out.print(s+" "));
>
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2052%20Solutions/WordSubsets.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/WordSubsets.txt
