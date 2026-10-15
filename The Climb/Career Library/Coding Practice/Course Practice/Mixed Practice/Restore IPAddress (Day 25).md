---
kind: "coding-problem"
title: "Restore IPAddress (Day 25)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elie Day 25 Solutions/RestoreIPAddress.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Restore IPAddress (Day 25)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

Example:

Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RestoreIPAddress.java
> ```java
> /*
>  * 
>  Given a string containing only digits, restore it by returning all possible valid IP address combinations.
>
> Example:
>
> Input: "25525511135"
> Output: ["255.255.11.135", "255.255.111.35"]
>
>
>  */
>
> import java.util.*;
>
> public class RestoreIPAddress {
>
>     public List<String> restoreIpAddresses(String s) {
>         List<String> res = new ArrayList<String>();
>         int len = s.length();
>         for(int i = 1; i<4 && i<len-2; i++){
>          for(int j = i+1; j<i+4 && j<len-1; j++){
>           for(int k = j+1; k<j+4 && k<len; k++){
> 	                String s1 = s.substring(0,i); 
> 			String s2 = s.substring(i,j);
> 			String s3 = s.substring(j,k); 
> 			String s4 = s.substring(k,len);
>                     
> if(isValid(s1) && isValid(s2) && isValid(s3) && isValid(s4)){
>                         res.add(s1+"."+s2+"."+s3+"."+s4);
>                     }
>                 }
>             }
>         }
>         return res;
>     }
>
>     public boolean isValid(String s){
>         if(s.length()>3 || s.length()==0 || (s.charAt(0)=='0' && s.length()>1) || Integer.parseInt(s)>255)
>             return false;
>         return true;
>     }
>
> 	  
> 	  public static void main(String args[] ) {
> 		Scanner sc = new Scanner(System.in);
> 		String str=sc.next();
> 		RestoreIpAddress ria=new RestoreIpAddress();
> 		System.out.println(ria.restoreIpAddresses(str));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elie%20Day%2025%20Solutions/RestoreIPAddress.java) · CODING RESOURCES/ELITE FS COMPLETE/Elie Day 25 Solutions/RestoreIPAddress.java
