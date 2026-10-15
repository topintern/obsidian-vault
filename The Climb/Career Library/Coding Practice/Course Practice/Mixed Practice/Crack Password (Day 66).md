---
kind: "coding-problem"
title: "Crack Password (Day 66)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/CrackPassword.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Crack Password (Day 66)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are N users registered on a website CuteKittens.com. 
Each of them has a unique password represented by pass[1], pass[2], ..., pass[N]. 
As this a very lovely site, many people want to access those awesomely cute pics of the kittens. 
But the adamant admin does not want the site to be available to the general public, 
so only those people who have passwords can access it.

You, being an awesome hacker finds a loophole in the password verification system. 
A string which is a concatenation of one or more passwords, in any order, 
is also accepted by the password verification system. 
Any password can appear 0 or more times in that string. 
Given access to each of the n passwords, and also have a string 
loginAttempt,determinewhetherthisstringbeacceptedbythepasswordverificationsystemofwebsite.
loginAttempt$ string can be created by concatenating password strings, it is accepted.

For example, if there are 3 users with passwords=[Abra,Ka,Dabra], then some of 
the valid combinations are Abra, KaAbra, KaDabraKa,KaDabraAbra and so on. 
Supplying Abra Ka Dabra, concatenated, passes authentication.

Input Format:
- The first line contains n, the number of users with passwords.
- The second line contains n space-separated strings, passwords[i], 
   that represent the passwords of each user.
- The third line contains a string, loginAttempt, which You must test for acceptance.
Note:passwords[i] contain only lowercase latin characters ('a'-'z').


### Output Format

For each valid string, You have to print the actual order of passwords, 
separated by space, whose concatenation results into loginAttempt. 
If loginAttempt can't be accepted by the password verification system, 
then print WRONG PASSWORD.

Sample Input1:
6
because can do must we what
wedowhatwemustbecausewecan
Sample Output1:
we do what we must because we can


Sample Input2:
2
hello planet
helloworld
Sample Output2:
WRONG PASSWORD


Sample Input3:
4
gurwgrb maqz holpkhqx aowypvopu
gurwgrb
Sample Output3:
gurwgrb


### Explanation

Sample #1: "wedowhatwemustbecausewecan" is the concatenation 
of passwords {"we", "do", "what", "we", "must", "because", "we", "can"}. That is
loginAttempt = pass[5] + pass[3] + pass[6] + pass[5] +  pass[4] + pass[1] + pass[5] + pass[2]
Note that any password can repeat any number of times.

Sample #2: We can't create string "helloworld" using the strings {"hello", "planet"}.

Sample #03: We can create loginAttempt ("gurwgrb") from pass[1]. 


========= Testcases Program-1 =========
case =1
input =10
a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa
aaaaaaaaaab
output =WRONG PASSWORD

case =2
input =4
gurwgrb maqz holpkhqx aowypvopu
gurwgrb
output =gurwgrb

case =3
input =6
because can do must we what
wedowhatwemustbecausewecan
output =we do what we must because we can

case =4
input =2
hello planet
helloworld
output =WRONG PASSWORD

case =5
input =6
xkof medbc mhyewjzsdg vkuzym tbeqv xtbyhn
xtbyhnmedbcmhyewjzsdgxtbyhn
output =xtbyhn medbc mhyewjzsdg xtbyhn

case =6
input =6
alutwfal kkhbqlrxnm qyyx lwdgpchwic rdtgzvw sduh
sduhkkhbqlrxnmsduhsduhqyyx
output =sduh kkhbqlrxnm sduh sduh qyyx

case =7
input =10
yjwcocch wsta elfvzzbxq swwxfq ilwk xiqtb hnxxiot ejxtmxvf jeurpxyf glkhe
elfvzzbxqwstailwkilwk
output =elfvzzbxq wsta ilwk ilwk

case =8
input =10
ddihmxzgdk sutvgb ifvqzlxc tmoccqna qxscvwxaif muihxrmdx olgga xjaqeq vtuc akfwn
xjaqeqvtucsutvgbakfwn
output =xjaqeq vtuc sutvgb akfwn

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CrackPassword.java
> ```java
> /*
> There are N users registered on a website CuteKittens.com. 
> Each of them has a unique password represented by pass[1], pass[2], ..., pass[N]. 
> As this a very lovely site, many people want to access those awesomely cute pics of the kittens. 
> But the adamant admin does not want the site to be available to the general public, 
> so only those people who have passwords can access it.
>
> You, being an awesome hacker finds a loophole in the password verification system. 
> A string which is a concatenation of one or more passwords, in any order, 
> is also accepted by the password verification system. 
> Any password can appear 0 or more times in that string. 
> Given access to each of the n passwords, and also have a string 
> loginAttempt,determinewhetherthisstringbeacceptedbythepasswordverificationsystemofwebsite.
> loginAttempt$ string can be created by concatenating password strings, it is accepted.
>
> For example, if there are 3 users with passwords=[Abra,Ka,Dabra], then some of 
> the valid combinations are Abra, KaAbra, KaDabraKa,KaDabraAbra and so on. 
> Supplying Abra Ka Dabra, concatenated, passes authentication.
>
> Input Format:
> - The first line contains n, the number of users with passwords.
> - The second line contains n space-separated strings, passwords[i], 
>    that represent the passwords of each user.
> - The third line contains a string, loginAttempt, which You must test for acceptance.
> Note:passwords[i] contain only lowercase latin characters ('a'-'z').
>
> Output Format
> For each valid string, You have to print the actual order of passwords, 
> separated by space, whose concatenation results into loginAttempt. 
> If loginAttempt can't be accepted by the password verification system, 
> then print WRONG PASSWORD.
>
> Sample Input1:
> 6
> because can do must we what
> wedowhatwemustbecausewecan
> Sample Output1:
> we do what we must because we can
>
>
> Sample Input2:
> 2
> hello planet
> helloworld
> Sample Output2:
> WRONG PASSWORD
>
>
> Sample Input3:
> 4
> gurwgrb maqz holpkhqx aowypvopu
> gurwgrb
> Sample Output3:
> gurwgrb
>
> Explanation:
> Sample #1: "wedowhatwemustbecausewecan" is the concatenation 
> of passwords {"we", "do", "what", "we", "must", "because", "we", "can"}. That is
> loginAttempt = pass[5] + pass[3] + pass[6] + pass[5] +  pass[4] + pass[1] + pass[5] + pass[2]
> Note that any password can repeat any number of times.
>
> Sample #2: We can't create string "helloworld" using the strings {"hello", "planet"}.
>
> Sample #03: We can create loginAttempt ("gurwgrb") from pass[1]. 
>
>
> ========= Testcases Program-1 =========
> case =1
> input =10
> a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa
> aaaaaaaaaab
> output =WRONG PASSWORD
>
> case =2
> input =4
> gurwgrb maqz holpkhqx aowypvopu
> gurwgrb
> output =gurwgrb
>
> case =3
> input =6
> because can do must we what
> wedowhatwemustbecausewecan
> output =we do what we must because we can
>
> case =4
> input =2
> hello planet
> helloworld
> output =WRONG PASSWORD
>
> case =5
> input =6
> xkof medbc mhyewjzsdg vkuzym tbeqv xtbyhn
> xtbyhnmedbcmhyewjzsdgxtbyhn
> output =xtbyhn medbc mhyewjzsdg xtbyhn
>
> case =6
> input =6
> alutwfal kkhbqlrxnm qyyx lwdgpchwic rdtgzvw sduh
> sduhkkhbqlrxnmsduhsduhqyyx
> output =sduh kkhbqlrxnm sduh sduh qyyx
>
> case =7
> input =10
> yjwcocch wsta elfvzzbxq swwxfq ilwk xiqtb hnxxiot ejxtmxvf jeurpxyf glkhe
> elfvzzbxqwstailwkilwk
> output =elfvzzbxq wsta ilwk ilwk
>
> case =8
> input =10
> ddihmxzgdk sutvgb ifvqzlxc tmoccqna qxscvwxaif muihxrmdx olgga xjaqeq vtuc akfwn
> xjaqeqvtucsutvgbakfwn
> output =xjaqeq vtuc sutvgb akfwn
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class CrackPassword {
>
>     public static void main(String[] args) {
>         Scanner input = new Scanner(System.in);
>             int numWords = input.nextInt();
>             String[] words = new String[numWords];
>             for (int j = 0; j < numWords; j++) {
>                 words[j] = input.next();
>             }
>             String password = input.next();
>             
>             noSolution = new HashSet<String>();
>             
>             String result = helper(password, words, "");
>             
>             if (!result.equals("WRONG PASSWORD")) {
>                 result = result.substring(1);
>             }
>             
>             System.out.println(result);
>     }
>     
>     public static Set<String> noSolution;
>     
>     public static String helper(String password, String[] words, String curRes) {
>         if (password.equals("")) {
>             return curRes;
>         } else if (noSolution.contains(password)) {
>             return "WRONG PASSWORD";
>         }
>         
>         for (int i = 0; i < words.length; i++) {
>             if (password.indexOf(words[i]) == 0) {
>                 String append = curRes + " " + words[i];
>                 String res = helper(password.substring(words[i].length()), words, append);
>                 
>                 if (!res.equals("WRONG PASSWORD")) {
>                     return res;
>                 }
>             }
>         }
>                 
>         noSolution.add(password);
>         
>         return "WRONG PASSWORD";        
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2066%20Solutions/CrackPassword.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/CrackPassword.java
