---
kind: "coding-problem"
title: "Valid String (Day 66)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/ValidString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Valid String (Day 66)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Sherlock considers a string to be valid if all characters of the string appear the same number of times.
 It is also valid if he can remove just 1 character at one index in the string, 
 and the remaining characters will occur the same number of times. 
 Given a string S, determine if it is valid. If so, return YES, otherwise return NO.

For example, if S=abc, it is a valid string because frequencies are [a:1,b:1,c:1]. 
So is s=abcc because we can remove one c and have 1 of each character in the remaining string. 
If s=abccc however, the string is not valid as we can only remove 1 occurrence of c. 
That would leave character frequencies of [a:1, b:1,c:2].

Input Format:
A single string .

Constraints:
Each character S[i] -> [a-z] 

Output Format:
Print YES if string S is valid, otherwise, print NO.

Sample Input1:
aabbcd
Sample Output1:
NO

Explanation1:
Given S="aabbcd", we would need to remove two characters, 
both c and d -> aabb or a and b -> abcd, to make it valid. 
We are limited to removing only one character, so S is invalid.

Sample Input2:
abcdefghhgfedecba
Sample Output2:
YES

Explanation2:
All characters occur twice except for e which occurs 3 times. 
We can delete one instance of e to have a valid string.


========= Testcases Program-3 =========
case =1
input =aabbccddeefghi
output ="NO"

case =2
input =aabbcd
output ="NO"

case =3
input =abcdefghhgfedecba
output ="YES"

case =4
input =abbcccddeeeeedddccccbba
output ="NO"

case =5
input =thequickbrownfoxfoxjumpsoveroverjumpslittlelittlelazydoglazythequickbrowndog
output ="YES"

case =6
input =qwertyuiopasdfghjklmnbvcxzadfghjklpoiutrmnbvcxdwesdgj
output ="NO"

case =7
input =qwertykeypadpakedqweryty
output ="YES"

case =8
input =redivider
output ="YES"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ValidString.java
> ```java
> /*
> Sherlock considers a string to be valid if all characters of the string appear the same number of times.
>  It is also valid if he can remove just 1 character at one index in the string, 
>  and the remaining characters will occur the same number of times. 
>  Given a string S, determine if it is valid. If so, return YES, otherwise return NO.
>
> For example, if S=abc, it is a valid string because frequencies are [a:1,b:1,c:1]. 
> So is s=abcc because we can remove one c and have 1 of each character in the remaining string. 
> If s=abccc however, the string is not valid as we can only remove 1 occurrence of c. 
> That would leave character frequencies of [a:1, b:1,c:2].
>
> Input Format:
> A single string .
>
> Constraints:
> Each character S[i] -> [a-z] 
>
> Output Format:
> Print YES if string S is valid, otherwise, print NO.
>
> Sample Input1:
> aabbcd
> Sample Output1:
> NO
>
> Explanation1:
> Given S="aabbcd", we would need to remove two characters, 
> both c and d -> aabb or a and b -> abcd, to make it valid. 
> We are limited to removing only one character, so S is invalid.
>
> Sample Input2:
> abcdefghhgfedecba
> Sample Output2:
> YES
>
> Explanation2:
> All characters occur twice except for e which occurs 3 times. 
> We can delete one instance of e to have a valid string.
>
>
> ========= Testcases Program-3 =========
> case =1
> input =aabbccddeefghi
> output ="NO"
>
> case =2
> input =aabbcd
> output ="NO"
>
> case =3
> input =abcdefghhgfedecba
> output ="YES"
>
> case =4
> input =abbcccddeeeeedddccccbba
> output ="NO"
>
> case =5
> input =thequickbrownfoxfoxjumpsoveroverjumpslittlelittlelazydoglazythequickbrowndog
> output ="YES"
>
> case =6
> input =qwertyuiopasdfghjklmnbvcxzadfghjklpoiutrmnbvcxdwesdgj
> output ="NO"
>
> case =7
> input =qwertykeypadpakedqweryty
> output ="YES"
>
> case =8
> input =redivider
> output ="YES"
>
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class ValidString {
>
>     public static void main(String[] args) {
>         /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
>         Scanner scanner = new Scanner(System.in);
>         String s = scanner.next();
>         HashMap<Character, Integer> map = new HashMap<>();
>         int len = s.length();
>         for (int i = 0 ; i < len ; ++i){
>             int count = 0;
>             char ch = s.charAt(i);
>             if (map.containsKey(ch)){
>                 count = map.get(ch);
>             }
>             map.put(ch, count + 1);
>         }
>         
>         HashSet<Integer> set = new HashSet<>();
>         for (Character ch : map.keySet()){
>             set.add(map.get(ch));
>         }
>         
>         boolean isYes = false;
>         if (set.size() <= 1){
>             isYes = true;
>         }else if (set.size() > 2){
>             isYes = false;
>         }else{
>             Iterator<Integer> it = set.iterator();
>             int x = it.next();
>             int y = it.next();
>             if (y < x){
>                 int temp = x;
>                 x = y;
>                 y = temp;
>             }
>             if (y - x == 1){
>                 if (map.size() * x + 1 == len){
>                     isYes = true;
>                 }
>             }
>             if (!isYes && x == 1 && (map.size() - 1) * y + 1 == len){
>                 isYes = true;
>             }
>         }
>         
>         System.out.println(isYes ? "YES" : "NO");
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2066%20Solutions/ValidString.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/ValidString.java
