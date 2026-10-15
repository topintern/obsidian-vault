---
kind: "coding-problem"
title: "Receive Mails (Day 6)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/ReceiveMails.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Receive Mails (Day 6)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of emails which consists of a local name and a domain name, separated by the @ sign.
For example, in john@kmit.com ,  john is the local name, and kmit.com is the domain name.
Besides lowercase letters, these emails may contain '.' s or '+' s.

If you add periods ( '.' ) between some characters in the local name part of an email address, 
mail sent there will be forwarded to the same address without dots in the local name.  

For example, "john.z@kmit.com" 
and "johnz@kmit.com" forward to the same email address.  (Note that this rule does not apply for domain names.)

If you add a plus ( '+' ) in the local name, everything after the first plus sign will be ignored. 
This allows certain emails to be filtered, for example  m.y+name@email.com  will be forwarded to  my@email.com
(Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.
Given a list of emails , we send one email to each address in the list.  

How many different addresses actually receive mails? 
 
Example 1:
Input:3
test.email+venkaty@kmit.com
test.e.mail+venkat.sai@kmit.com
testemail+gopi@kmit.eng.com

Output: 2
Explanation: "testemail@kmit.com" and "testemail@kmit.eng.com" actually receive mails

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ReceiveMails.java
> ```java
> /*
>  
>  
>  
>  
> Given a list of emails which consists of a local name and a domain name, separated by the @ sign.
> For example, in john@kmit.com ,  john is the local name, and kmit.com is the domain name.
> Besides lowercase letters, these emails may contain '.' s or '+' s.
>
> If you add periods ( '.' ) between some characters in the local name part of an email address, 
> mail sent there will be forwarded to the same address without dots in the local name.  
>
> For example, "john.z@kmit.com" 
> and "johnz@kmit.com" forward to the same email address.  (Note that this rule does not apply for domain names.)
>
> If you add a plus ( '+' ) in the local name, everything after the first plus sign will be ignored. 
> This allows certain emails to be filtered, for example  m.y+name@email.com  will be forwarded to  my@email.com
> (Again, this rule does not apply for domain names.)
>
> It is possible to use both of these rules at the same time.
> Given a list of emails , we send one email to each address in the list.  
>
> How many different addresses actually receive mails? 
>  
> Example 1:
> Input:3
> test.email+venkaty@kmit.com
> test.e.mail+venkat.sai@kmit.com
> testemail+gopi@kmit.eng.com
>
> Output: 2
> Explanation: "testemail@kmit.com" and "testemail@kmit.eng.com" actually receive mails
>
>
>  
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class ReceiveMails {
>
> 	 public int numUniqueEmails(String[] emails) {
> 	        Set<String> seen = new HashSet();
> 	        for (String email: emails) {
> 	            int i = email.indexOf('@');
> 	            String local = email.substring(0, i);
> 	            String rest = email.substring(i);
> 	            if (local.contains("+")) {
> 	                local = local.substring(0, local.indexOf('+'));
> 	            }
> 	            local = local.replace(".", "");
> 	            seen.add(local + rest);
> 	        }
>
> 	        return seen.size();
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			
> 		    ReceiveMails rm=new ReceiveMails();
> 			int num = Integer.parseInt(br.readLine());
> 			String[] emails= new String[num];
> 			for(int i=0;i<num;i++){
> 			 emails[i] = br.readLine();
> 			}
> 			System.out.println(rm.numUniqueEmails(emails));   
> 			
> 			}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day-6-Solutions/ReceiveMails.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/ReceiveMails.java
