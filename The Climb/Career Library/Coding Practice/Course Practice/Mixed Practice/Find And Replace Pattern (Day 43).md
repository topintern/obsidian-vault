---
kind: "coding-problem"
title: "Find And Replace Pattern (Day 43)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/FindAndReplacePattern.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find And Replace Pattern (Day 43)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have a list of words and a pattern, and you want to know which words in words matches the pattern.

A word matches the pattern if there exists a permutation of letters p so that after replacing 
every letter x in the pattern with p(x), we get the desired word.

(Recall that a permutation of letters is a bijection from letters to letters: 
every letter maps to another letter, and no two letters map to the same letter.)

Return a list of the words in words that match the given pattern. 

print the answer in ascending order.

Note:
1 <= words.length <= 50
1 <= pattern.length = words[i].length <= 20


### Sample Input: 

abc deq mee aqq dkd ccc 
abb


### Sample Output

aqq mee


### Explanation: 

"mee" matches the pattern because there is a permutation {a -> m, b -> e, ...}. 
"ccc" does not match the pattern because {a -> c, b -> c, ...} is not a permutation,
since a and b map to the same letter.

----------TestCases-----------
case =1
input =abc deq mee aqq dkd ccc
abb
output =aqq mee

case =2
input =abc def ghi ijk ikl imn jkl
aef
output =abc def ghi ijk ikl imn jkl

case =3
input =aghh ammk akmm annk nggk kllm klll nmmn tkkt
seed
output =ammk annk kllm nggk

case =4
input =ajmkl kjjak mkkle kllmn needs aeeba abbca abbka mnnmn
ajjka
output =abbca abbka aeeba kjjak

case =5
input =ala lol mom non kjk lll klj iki uuk hhj gyy trr
mam
output =ala iki kjk lol mom non

case =6
input =venkat kmohan trendy keshav rabbit carrot
abcdef
output =keshav kmohan trendy venkat

case =7
input =cool bull bell tool mood dell kill bill well soon noon
abbc
output =cool mood soon tool

case =8
input =cool bull bell tool mood dell kill bill well soon noon
abcc
output =bell bill bull dell kill well

case =9
input =ala lol mom non kjk lll klj iki uuk hhj gyy trr
aab
output =hhj uuk

case =10
input =alaa loll momm nonn kjjj llll kljj ikii uukk hhjk gyyy trrr
abbb
output =gyyy kjjj trrr

case =11
input =alaa loll momm nonn kjjj llll kljj ikii uukk hhjk gyyy trrr alaa cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon 
alaa
output =""

case =12
input =abbbtrewyer456789345ertyufghjaaa accctrewyer456789345ertyufghjaaa dbbbtrewyer456789345ertyufghjddd
abbbtrewyer456789345ertyufghjaaa
output =""

case =13
input =ajmkl kjajk mkkle kllmn needs aebae abbca babka mnnmn
ajjka
output =abbca

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindAndReplacePattern.java
> ```java
> /*
>  * 
> You have a list of words and a pattern, and you want to know which words in words matches the pattern.
>
> A word matches the pattern if there exists a permutation of letters p so that after replacing 
> every letter x in the pattern with p(x), we get the desired word.
>
> (Recall that a permutation of letters is a bijection from letters to letters: 
> every letter maps to another letter, and no two letters map to the same letter.)
>
> Return a list of the words in words that match the given pattern. 
>
> print the answer in ascending order.
>
> Note:
> 1 <= words.length <= 50
> 1 <= pattern.length = words[i].length <= 20
>
> Sample Input: 
> abc deq mee aqq dkd ccc 
> abb
>
> Sample Output:
> aqq mee
>
> Explanation: 
> "mee" matches the pattern because there is a permutation {a -> m, b -> e, ...}. 
> "ccc" does not match the pattern because {a -> c, b -> c, ...} is not a permutation,
> since a and b map to the same letter.
>
> ----------TestCases-----------
> case =1
> input =abc deq mee aqq dkd ccc
> abb
> output =aqq mee
>
> case =2
> input =abc def ghi ijk ikl imn jkl
> aef
> output =abc def ghi ijk ikl imn jkl
>
> case =3
> input =aghh ammk akmm annk nggk kllm klll nmmn tkkt
> seed
> output =ammk annk kllm nggk
>
> case =4
> input =ajmkl kjjak mkkle kllmn needs aeeba abbca abbka mnnmn
> ajjka
> output =abbca abbka aeeba kjjak
>
> case =5
> input =ala lol mom non kjk lll klj iki uuk hhj gyy trr
> mam
> output =ala iki kjk lol mom non
>
> case =6
> input =venkat kmohan trendy keshav rabbit carrot
> abcdef
> output =keshav kmohan trendy venkat
>
> case =7
> input =cool bull bell tool mood dell kill bill well soon noon
> abbc
> output =cool mood soon tool
>
> case =8
> input =cool bull bell tool mood dell kill bill well soon noon
> abcc
> output =bell bill bull dell kill well
>
> case =9
> input =ala lol mom non kjk lll klj iki uuk hhj gyy trr
> aab
> output =hhj uuk
>
> case =10
> input =alaa loll momm nonn kjjj llll kljj ikii uukk hhjk gyyy trrr
> abbb
> output =gyyy kjjj trrr
>
> case =11
> input =alaa loll momm nonn kjjj llll kljj ikii uukk hhjk gyyy trrr alaa cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon cool bull bell tool mood dell kill bill well soon noon 
> alaa
> output =""
>
> case =12
> input =abbbtrewyer456789345ertyufghjaaa accctrewyer456789345ertyufghjaaa dbbbtrewyer456789345ertyufghjddd
> abbbtrewyer456789345ertyufghjaaa
> output =""
>
> case =13
> input =ajmkl kjajk mkkle kllmn needs aebae abbca babka mnnmn
> ajjka
> output =abbca
>
>  * 
>  */
>
> import java.util.*;
>
> public class FindAndReplacePattern {
>
> 	public static List<String> findAndReplacePattern(String[] words, String pattern) {
> 		List<String> ans = new ArrayList();
> 		for (String word : words)
> 			if (match(word, pattern))
> 				ans.add(word);
> 		return ans;
> 	}
>
> 	public static boolean match(String word, String pattern) {
> 		Map<Character, Character> m1 = new HashMap();
> 		Map<Character, Character> m2 = new HashMap();
>
> 		for (int i = 0; i < word.length(); ++i) {
> 			char w = word.charAt(i);
> 			char p = pattern.charAt(i);
> 			if (!m1.containsKey(w))
> 				m1.put(w, p);
> 			if (!m2.containsKey(p))
> 				m2.put(p, w);
> 			if (m1.get(w) != p || m2.get(p) != w)
> 				return false;
> 		}
>
> 		return true;
> 	}
>
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		String wordsString = sc.nextLine();
> 	    	String words[]= wordsString.split(" ");
> 	    	String pattern= sc.next();
> 	    	List<String> ans = new ArrayList();
> 	    	ans = findAndReplacePattern(words,pattern);
> 			Collections.sort(ans);
> 	    	ans.stream().forEach(s -> System.out.print(s+" "));
>
>         
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2043%20Solutions/FindAndReplacePattern.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/FindAndReplacePattern.java
