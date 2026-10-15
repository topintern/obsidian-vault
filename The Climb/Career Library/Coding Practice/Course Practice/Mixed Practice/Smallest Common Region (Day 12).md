---
kind: "coding-problem"
title: "Smallest Common Region (Day 12)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/SmallestCommonRegion.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Smallest Common Region (Day 12)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given some lists of areas where the first area of each list includes all other areas in that list.
Naturally, if a area A contains another area B then A is bigger than B. Also by definition a area A contains itself.
Given two areas area1, area2, find out the smallest area that contains both of them.
If you are given areas a1, a2 and a3 such that a1 includes a3, it is guaranteed there is no a2 such that a2 includes a3.
It's guaranteed the smallest area exists.

Example 1:
Input=	5
			Earth-North America-South America
			North America-United States-Canada
			United States-New York-Boston
			Canada-Ontario-Quebec
			South America-Brazil
			Quebec			//area-1
			New York		//area-2

Output= North America
 
Build family tree from offsprings to their parents;
Use a HashSet to construct ancestry history of area1;
Retrieve ancestry of area2 by family tree till find the first common ancestry in ancestry history of area1.
 
----TestCase----
case =1
input =4
Bharath-Telangana-Hyderabad-Dilshukhnagar
Telangana-Rangareddy-Lbnagar
Hyderabad-Dilshukhnagar-Gaddiannaram
Rangareddy-Lbnagar-saroornagar
Gaddiannaram
saroornagar
output =Bharath

case =2
input =4
India-Telangana-Hyderabad
Telangana-Rangareddy-Lbnagar
Telangana-Dilshukhnagar-Gaddiannaram
Rangareddy-Lbnagar-saroornagar
Gaddiannaram
saroornagar
output =Telangana

case =3
input =5
Earth-Asia-China-Biejing
Asia-India-New Delhi-Red fort-India Gate
India-Telangana-Hyderabad-Charminar
Telangana-Secunderbad-Paradise
Hyderabad-Narayanaguda-Kmit
Kmit
Charminar
output =India

case =4
input =5
Earth-North America-South America
South America-United States-Canada-West Indies
United States-New York-Boston-WHO
Canada-Ontario-Quebec
South America-Brazil-Federal District
Ontario
Federal District
output =South America
 

case =5
input =5
Asia-China-Biejing
Asia-India-New Delhi-Red fort-India Gate
India-Telangana-Hyderabad-Charminar
Telangana-Secunderbad-Paradise
Hyderabad-Narayanaguda-Kmit
Paradise
India Gate
output =Asia

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SmallestCommonRegion.java
> ```java
> /*
> You are given some lists of areas where the first area of each list includes all other areas in that list.
> Naturally, if a area A contains another area B then A is bigger than B. Also by definition a area A contains itself.
> Given two areas area1, area2, find out the smallest area that contains both of them.
> If you are given areas a1, a2 and a3 such that a1 includes a3, it is guaranteed there is no a2 such that a2 includes a3.
> It's guaranteed the smallest area exists.
>
> Example 1:
> Input=	5
> 			Earth-North America-South America
> 			North America-United States-Canada
> 			United States-New York-Boston
> 			Canada-Ontario-Quebec
> 			South America-Brazil
> 			Quebec			//area-1
> 			New York		//area-2
>
> Output= North America
>  
> Build family tree from offsprings to their parents;
> Use a HashSet to construct ancestry history of area1;
> Retrieve ancestry of area2 by family tree till find the first common ancestry in ancestry history of area1.
>  
> ----TestCase----
> case =1
> input =4
> Bharath-Telangana-Hyderabad-Dilshukhnagar
> Telangana-Rangareddy-Lbnagar
> Hyderabad-Dilshukhnagar-Gaddiannaram
> Rangareddy-Lbnagar-saroornagar
> Gaddiannaram
> saroornagar
> output =Bharath
>
> case =2
> input =4
> India-Telangana-Hyderabad
> Telangana-Rangareddy-Lbnagar
> Telangana-Dilshukhnagar-Gaddiannaram
> Rangareddy-Lbnagar-saroornagar
> Gaddiannaram
> saroornagar
> output =Telangana
>
> case =3
> input =5
> Earth-Asia-China-Biejing
> Asia-India-New Delhi-Red fort-India Gate
> India-Telangana-Hyderabad-Charminar
> Telangana-Secunderbad-Paradise
> Hyderabad-Narayanaguda-Kmit
> Kmit
> Charminar
> output =India
>
> case =4
> input =5
> Earth-North America-South America
> South America-United States-Canada-West Indies
> United States-New York-Boston-WHO
> Canada-Ontario-Quebec
> South America-Brazil-Federal District
> Ontario
> Federal District
> output =South America
>  
>
> case =5
> input =5
> Asia-China-Biejing
> Asia-India-New Delhi-Red fort-India Gate
> India-Telangana-Hyderabad-Charminar
> Telangana-Secunderbad-Paradise
> Hyderabad-Narayanaguda-Kmit
> Paradise
> India Gate
> output =Asia
>
> */
>
> import java.io.*;
> import java.util.*;
>
> class SmallestCommonArea {
>
> 	public static String findSmallestArea(List<List<String>> areas, String area1, String area2) {
>         Map<String, String> parents = new HashMap<>();
>         Set<String> ancestryHistory = new HashSet<>();
>         for (List<String> area : areas)
>             for (int i = 1; i < area.size(); ++i)
>                 parents.put(area.get(i), area.get(0));
>         while (area1 != null) {
>             ancestryHistory.add(area1);
>             area1 = parents.get(area1);
>         }
>         while (!ancestryHistory.contains(area2))
>             area2 = parents.get(area2);
>         return area2;
>     }
> 	
> 	public static void main(String args[] ) throws IOException {
> 		 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			int n=Integer.parseInt(br.readLine());
> 			List<List<String>> areas = new ArrayList<List<String>>();
> 			
>
> 		       for(int i=0; i<n; i++)
> 		       {
> 		    	   List<String> combi = new ArrayList<String>();
>
> 		          
> 		        	  String line=br.readLine();
> 		        	  String words[]=line.split("-");
> 					  for(String s:words)
> 		        	   combi.add(s);
> 		        	   		          
> 		        	   areas.add(combi);
> 		       }
> 		      // System.out.println(synonyms);
> 		      String area1 =br.readLine();
> 		      String area2 =br.readLine();
> 		      System.out.println(findSmallestArea(areas,area1,area2));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2012%20Solutions/SmallestCommonRegion.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/SmallestCommonRegion.java
