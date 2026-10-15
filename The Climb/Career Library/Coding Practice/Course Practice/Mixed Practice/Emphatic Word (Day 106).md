---
kind: "coding-problem"
title: "Emphatic Word (Day 106)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 106 Solutions/Emphatic Word.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Emphatic Word (Day 106)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

"Emphatic Pronunciation" of a given word is where we take the word and
replicate some of the letter to emphasize their impact.

Instead of saying 'oh my god', someone may say "ohhh myyy goddd", 
We define emphatic pronunciation of a word, which is derived by replicating 
a group (or single) of letters in the original word. 

So that the replicated group is atleast 3 characters or more and 
greater than or equal to size of original group. 
For example Good -> Goood is an emphatic pronunciation,
but Goodd is not because in Goodd the 'd' are only occuring twice consecutively.
 
In the question you are given the "Emphatic pronunciation" word, 
you have to findout how many words can legal result in the "emphatic pronunciation" word.

Input Format:
-------------
Line-1 -> A String contains a single word, Emphatic Pronunciation word
Line-2 -> Space seperated word/s

Output Format:
--------------
Print an integer as your result


Sample Input-1:
---------------
Goood
Good

Sample Output-1:
----------------
1


Sample Input-2:
---------------
heeelllooo
hello hi helo

Sample Output-2:
----------------
2


------------testcases------------
case =1
input =Goood
Good
output =1

case =2
input =Heeelllooo
Helo Hello Hi
output =2

case =3
input =aaabbcccddddddeeeff
abcdef abbcdeff aabbcdeeff aabbcdddeff abbcdeff
output =4

case =4
input =apppllleee
aple apple aplle aplee aaplee aappllee aaplle aaple apppllee
output =5

case =5
input =dddiiiinnssssssoooo
dinnssoo ddinso ddiinnso ddiinnssoo ddiinso dinsoo ddiinsso dinssoo dinso
output =3

case =6
input =aaaaaaaa
a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa
output =8

case =7
input =aaaaabbbbbbb
ab aab aabb aaabbb aaabb aabbb aaabbbb aaaabbbb aaaaabbbbab aaabbbbbaa aaaaabbbbbbb aaaaabbbbbbbb
output =9

case =8
input =abbbcccdddeeefffgghhhiiijjjkkklllllmmmnnnooo
abcdefghijklmno abcdefgghhijklmno abbccdddeeefffgghhiijjkkkllmno abcccddeffgghhhiijjkklmno abbccddeeffghiijjkllmno abccdeefffggihhjkkllmmnooo abcdefghijklmno abcdefghijklmno abbccddeeffgghiiijjkllmno abccdefgghhiiiiijkkllmnoo
output =4

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Emphatic Word.txt
> ```java
> /*
> "Emphatic Pronunciation" of a given word is where we take the word and
> replicate some of the letter to emphasize their impact.
>
> Instead of saying 'oh my god', someone may say "ohhh myyy goddd", 
> We define emphatic pronunciation of a word, which is derived by replicating 
> a group (or single) of letters in the original word. 
>
> So that the replicated group is atleast 3 characters or more and 
> greater than or equal to size of original group. 
> For example Good -> Goood is an emphatic pronunciation,
> but Goodd is not because in Goodd the 'd' are only occuring twice consecutively.
>  
> In the question you are given the "Emphatic pronunciation" word, 
> you have to findout how many words can legal result in the "emphatic pronunciation" word.
>
> Input Format:
> -------------
> Line-1 -> A String contains a single word, Emphatic Pronunciation word
> Line-2 -> Space seperated word/s
>
> Output Format:
> --------------
> Print an integer as your result
>
>
> Sample Input-1:
> ---------------
> Goood
> Good
>
> Sample Output-1:
> ----------------
> 1
>
>
> Sample Input-2:
> ---------------
> heeelllooo
> hello hi helo
>
> Sample Output-2:
> ----------------
> 2
>
>
> ------------testcases------------
> case =1
> input =Goood
> Good
> output =1
>
> case =2
> input =Heeelllooo
> Helo Hello Hi
> output =2
>
> case =3
> input =aaabbcccddddddeeeff
> abcdef abbcdeff aabbcdeeff aabbcdddeff abbcdeff
> output =4
>
> case =4
> input =apppllleee
> aple apple aplle aplee aaplee aappllee aaplle aaple apppllee
> output =5
>
> case =5
> input =dddiiiinnssssssoooo
> dinnssoo ddinso ddiinnso ddiinnssoo ddiinso dinsoo ddiinsso dinssoo dinso
> output =3
>
> case =6
> input =aaaaaaaa
> a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa
> output =8
>
> case =7
> input =aaaaabbbbbbb
> ab aab aabb aaabbb aaabb aabbb aaabbbb aaaabbbb aaaaabbbbab aaabbbbbaa aaaaabbbbbbb aaaaabbbbbbbb
> output =9
>
> case =8
> input =abbbcccdddeeefffgghhhiiijjjkkklllllmmmnnnooo
> abcdefghijklmno abcdefgghhijklmno abbccdddeeefffgghhiijjkkkllmno abcccddeffgghhhiijjkklmno abbccddeeffghiijjkllmno abccdeefffggihhjkkllmmnooo abcdefghijklmno abcdefghijklmno abbccddeeffgghiiijjkllmno abccdefgghhiiiiijkkllmnoo
> output =4
>
> */
>
> import java.util.Scanner;
>
> class EmphaticWord {
> public static int emphaticWord(String S, String[] words) {
>         int res = 0;
>         for (String W : words) if (check(S, W)) res++;
>         return res;
>     }
>    public static boolean check(String S, String W) {
>         int n = S.length(), m = W.length(), i = 0, j = 0;
>         for (int i2 = 0, j2 = 0; i < n && j < m; i = i2, j = j2) {
>             if (S.charAt(i) != W.charAt(j)) return false;
>             while (i2 < n && S.charAt(i2) == S.charAt(i)) i2++;
>             while (j2 < m && W.charAt(j2) == W.charAt(j)) j2++;
>             if (i2 - i != j2 - j && i2 - i < Math.max(3, j2 - j)) return false;
>         }
>         return i == n && j == m;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String S=sc.nextLine();
> 		String[] words=sc.nextLine().split(" ");
> 		System.out.println(emphaticWord(S, words));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20106%20Solutions/Emphatic%20Word.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 106 Solutions/Emphatic Word.txt
