---
kind: "coding-problem"
title: "String Permutations (Day 35)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/StringPermutations.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# String Permutations (Day 35)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write a program to print all permutations of a given string

Example-1:
    Input=  ABC
    Output= ABC ACB BAC BCA CBA CAB


Note:
print output in lexicographic order

======TestCases=======
case =1
input =bacd
output =abcd abdc acbd acdb adbc adcb bacd badc bcad bcda bdac bdca cabd cadb cbad cbda cdab cdba dabc dacb dbac dbca dcab dcba 

case =2
input =AAAA
output =AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA 

case =3
input =DbEcA                                                                                                                  
output =ADEbc ADEcb ADbEc ADbcE ADcEb ADcbE AEDbc AEDcb AEbDc AEbcD AEcDb AEcbD AbDEc AbDcE AbEDc AbEcD AbcDE AbcED AcDEb AcDbE AcEDb AcEbD AcbDE AcbED DAEbc DAEcb DAbEc DAbcE DAcEb DAcbE DEAbc DEAcb DEbAc DEbcA DEcAb DEcbA DbAEc DbAcE DbEAc DbEcA DbcAE DbcEA DcAEb DcAbE DcEAb DcEbA DcbAE DcbEA EADbc EADcb EAbDc EAbcD EAcDb EAcbD EDAbc EDAcb EDbAc EDbcA EDcAb EDcbA EbADc EbAcD EbDAc EbDcA EbcAD EbcDA EcADb EcAbD EcDAb EcDbA EcbAD EcbDA bADEc bADcE bAEDc bAEcD bAcDE bAcED bDAEc bDAcE bDEAc bDEcA bDcAE bDcEA bEADc bEAcD bEDAc bEDcA bEcAD bEcDA bcADE bcAED bcDAE bcDEA bcEAD bcEDA cADEb cADbE cAEDb cAEbD cAbDE cAbED cDAEb cDAbE cDEAb cDEbA cDbAE cDbEA cEADb cEAbD cEDAb cEDbA cEbAD cEbDA cbADE cbAED cbDAE cbDEA cbEAD cbEDA 

case =4
input =aba
output =aab aab aba aba baa baa

case =5
input =a
output =a

case =6
input =xmaz
output =amxz amzx axmz axzm azmx azxm maxz mazx mxaz mxza mzax mzxa xamz xazm xmaz xmza xzam xzma zamx zaxm zmax zmxa zxam zxma

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StringPermutations.java
> ```java
> /*
> Write a program to print all permutations of a given string
>
> Example-1:
>     Input=  ABC
>     Output= ABC ACB BAC BCA CBA CAB
>
>
> Note:
> print output in lexicographic order
>
> ======TestCases=======
> case =1
> input =bacd
> output =abcd abdc acbd acdb adbc adcb bacd badc bcad bcda bdac bdca cabd cadb cbad cbda cdab cdba dabc dacb dbac dbca dcab dcba 
>
> case =2
> input =AAAA
> output =AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA 
>
> case =3
> input =DbEcA                                                                                                                  
> output =ADEbc ADEcb ADbEc ADbcE ADcEb ADcbE AEDbc AEDcb AEbDc AEbcD AEcDb AEcbD AbDEc AbDcE AbEDc AbEcD AbcDE AbcED AcDEb AcDbE AcEDb AcEbD AcbDE AcbED DAEbc DAEcb DAbEc DAbcE DAcEb DAcbE DEAbc DEAcb DEbAc DEbcA DEcAb DEcbA DbAEc DbAcE DbEAc DbEcA DbcAE DbcEA DcAEb DcAbE DcEAb DcEbA DcbAE DcbEA EADbc EADcb EAbDc EAbcD EAcDb EAcbD EDAbc EDAcb EDbAc EDbcA EDcAb EDcbA EbADc EbAcD EbDAc EbDcA EbcAD EbcDA EcADb EcAbD EcDAb EcDbA EcbAD EcbDA bADEc bADcE bAEDc bAEcD bAcDE bAcED bDAEc bDAcE bDEAc bDEcA bDcAE bDcEA bEADc bEAcD bEDAc bEDcA bEcAD bEcDA bcADE bcAED bcDAE bcDEA bcEAD bcEDA cADEb cADbE cAEDb cAEbD cAbDE cAbED cDAEb cDAbE cDEAb cDEbA cDbAE cDbEA cEADb cEAbD cEDAb cEDbA cEbAD cEbDA cbADE cbAED cbDAE cbDEA cbEAD cbEDA 
>
> case =4
> input =aba
> output =aab aab aba aba baa baa
>
> case =5
> input =a
> output =a
>
> case =6
> input =xmaz
> output =amxz amzx axmz axzm azmx azxm maxz mazx mxaz mxza mzax mzxa xamz xazm xmaz xmza xzam xzma zamx zaxm zmax zmxa zxam zxma 
>
> */
> import java.util.*;
>
> public class StringPermutations {
>     public static ArrayList<String> permutedStrings=new ArrayList<String>();
> 	 public static void main(String[] args) 
> 	    { 
> 		 Scanner sc = new Scanner(System.in);
> 			String str=sc.next();
>
> 	        int n = str.length(); 
> 	        StringPermutations permutation = new StringPermutations(); 
> 	        permutation.permute(str, 0, n-1); 
> 	        Collections.sort(permutedStrings);
> 	        for(String s:permutedStrings)
> 	        System.out.print(s+" ");
> 	    } 
> 	  
> 	    /** 
> 	     * permutation function 
> 	     * @param str string to calculate permutation for 
> 	     * @param l starting index 
> 	     * @param r end index 
> 	     */
> 	    private static void permute(String str, int l, int r) 
> 	    { 
> 	        if (l == r) 
> 	            permutedStrings.add(str); 
> 	        else
> 	        { 
> 	            for (int i = l; i <= r; i++) 
> 	            { 
> 	                str = swap(str,l,i); 
> 	                permute(str, l+1, r); 
> 	                str = swap(str,l,i); 
> 	            } 
> 	        } 
> 	    } 
> 	  
> 	    /** 
> 	     * Swap Characters at position 
> 	     * @param a string value 
> 	     * @param i position 1 
> 	     * @param j position 2 
> 	     * @return swapped string 
> 	     */
> 	    public static String swap(String a, int i, int j) 
> 	    { 
> 	        char temp; 
> 	        char[] charArray = a.toCharArray(); 
> 	        temp = charArray[i] ; 
> 	        charArray[i] = charArray[j]; 
> 	        charArray[j] = temp; 
> 	        return String.valueOf(charArray); 
> 	    } 
> 	    
> 	    
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2035%20Solutions/StringPermutations.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/StringPermutations.java
