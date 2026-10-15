---
kind: "coding-problem"
title: "Decode Word (Day 105)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 105 Solutions/DecodeWord.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Decode Word (Day 105)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

“Enigma” is a German encoding machine which was used to transmit messages as numbers. 
    Alan Turing a British cryptologist has hired KMIT students to break the code and save England. 
    
    Alan has figured out and informed you that each letter is represented as number in enigma 
    with 'a' being 1 'b' being 2,.. and 'z' being 26. 
    
    However a number 211 can mean “ua” or “baa” or “bk”. Further Turing has also supplied you 
    with a dictionary of potential targets which Germany is 
    likely to attack like “london” ,”reading” , “york”  etc. 
    
    Given an enigma generated message, you should help Turing inform the British Defence system
    about the next target. For example 12151441514 means the next attack is on London. 
    Similarly 25151811 means York will be attacked.
    
    Input Format:
    -------------
    Line-1 -> space seperated Strings, dictionary of potential targets.
    Line-2 -> a String, enigma generated message.
    
    Output Format:
    --------------
    Print the potential target.
    
    
    Sample Input-1:
    ---------------
    london reading york cambridge oxford norwich bradford 
    12151441514
    
    Sample Output-1:
    ----------------
    london
    
    Sample Input-2:
    ---------------
    london reading york cambridge oxford norwich bradford
    31132189475
    
    Sample Output-2:
    ----------------
    cambridge

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DecodeWord.txt
> ```java
> /*
> 	“Enigma” is a German encoding machine which was used to transmit messages as numbers. 
>     Alan Turing a British cryptologist has hired KMIT students to break the code and save England. 
>     
>     Alan has figured out and informed you that each letter is represented as number in enigma 
>     with 'a' being 1 'b' being 2,.. and 'z' being 26. 
>     
>     However a number 211 can mean “ua” or “baa” or “bk”. Further Turing has also supplied you 
>     with a dictionary of potential targets which Germany is 
>     likely to attack like “london” ,”reading” , “york”  etc. 
>     
>     Given an enigma generated message, you should help Turing inform the British Defence system
>     about the next target. For example 12151441514 means the next attack is on London. 
>     Similarly 25151811 means York will be attacked.
>     
>     Input Format:
>     -------------
>     Line-1 -> space seperated Strings, dictionary of potential targets.
>     Line-2 -> a String, enigma generated message.
>     
>     Output Format:
>     --------------
>     Print the potential target.
>     
>     
>     Sample Input-1:
>     ---------------
>     london reading york cambridge oxford norwich bradford 
>     12151441514
>     
>     Sample Output-1:
>     ----------------
>     london
>     
>     Sample Input-2:
>     ---------------
>     london reading york cambridge oxford norwich bradford
>     31132189475
>     
>     Sample Output-2:
>     ----------------
>     cambridge
>     
>
>
> */
>
> import java.util.*;
>
> class DecodeWord {
>  
>     static String findMatch(String encode, String decode) {
>         String match="";
> 		for(int i=0;i<decode.length();i++){
> 			match=match+(decode.charAt(i)-96);
> 		}
> 		return match;
>     }
>     public static String findDecode(String str[],String encode) {
>         for(String decode:str){
> 			if(encode.equals(findMatch(encode,decode)))
> 				return decode;
> 		}
>         return "No Match";
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		String[] str=sc.nextLine().split(" ");
> 		String en=sc.next();
> 		System.out.println(findDecode(str,en));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20105%20Solutions/DecodeWord.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 105 Solutions/DecodeWord.txt
