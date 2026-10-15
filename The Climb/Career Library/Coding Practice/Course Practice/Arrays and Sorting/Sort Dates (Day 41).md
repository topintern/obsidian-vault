---
kind: "coding-problem"
title: "Sort Dates (Day 41)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/SortDates.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sort Dates (Day 41)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of dates, sort them in ascending order, 
Dates are described below

Each date is in the form dd mmm yyyy where 
dd has 0-31
mmm has Jan,Feb,Mar,Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec
yyyy is four digits

For Example dates = ['01 Mar 2017','03 Feb 2017','15 Jan 1998'] 
would sort to 
['15 Jan 1998','03 Feb 2017','01 Mar 2017'];

Sample Input
------------
10
20 Oct 2052
06 Jun 1933
26 May 1960
20 Sep 1958
16 Mar 2068
25 May 1912
16 Dec 2018
26 Dec 2061
04 Nov 2030
28 Jul 1963

Sample Output
-------------
25 May 1912
06 Jun 1933
20 Sep 1958
26 May 1960
28 Jul 1963
16 Dec 2018
04 Nov 2030
20 Oct 2052
26 Dec 2061
16 Mar 2068




----------------------------------------------------------------------------------

case=1
input=8
21 Oct 2053
07 Jun 1934
27 May 1934
21 Sep 1958
17 Mar 2068
26 May 1912
17 Dec 2012
27 Dec 2061

output=26 May 1912
27 May 1934
07 Jun 1934
21 Sep 1958
17 Dec 2012
21 Oct 2053
27 Dec 2061
17 Mar 2068

output=26 May 1912
27 May 1934
7 Jun 1934
21 Sep 1958
17 Dec 2012
21 Oct 2053
27 Dec 2061
17 Mar 2068

case=2
input=7
07 Jun 1934
07 Jun 1934
21 Sep 1958
17 Mar 2068
26 May 2012
17 Dec 2012
27 Dec 2061

output=07 Jun 1934
07 Jun 1934
21 Sep 1958
26 May 2012
17 Dec 2012
27 Dec 2061
17 Mar 2068

output=7 Jun 1934
7 Jun 1934
21 Sep 1958
26 May 2012
17 Dec 2012
27 Dec 2061
17 Mar 2068

case=3
input=3
07 Jan 1934
07 Dec 1934
21 Sep 1934

output=07 Jan 1934
21 Sep 1934
07 Dec 1934

output=7 Jan 1934
21 Sep 1934
7 Dec 1934

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SortDates.java
> ```java
> /*
>  * 
> Given a list of dates, sort them in ascending order, 
> Dates are described below
>
> Each date is in the form dd mmm yyyy where 
> dd has 0-31
> mmm has Jan,Feb,Mar,Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec
> yyyy is four digits
>
> For Example dates = ['01 Mar 2017','03 Feb 2017','15 Jan 1998'] 
> would sort to 
> ['15 Jan 1998','03 Feb 2017','01 Mar 2017'];
>
> Sample Input
> ------------
> 10
> 20 Oct 2052
> 06 Jun 1933
> 26 May 1960
> 20 Sep 1958
> 16 Mar 2068
> 25 May 1912
> 16 Dec 2018
> 26 Dec 2061
> 04 Nov 2030
> 28 Jul 1963
>
> Sample Output
> -------------
> 25 May 1912
> 06 Jun 1933
> 20 Sep 1958
> 26 May 1960
> 28 Jul 1963
> 16 Dec 2018
> 04 Nov 2030
> 20 Oct 2052
> 26 Dec 2061
> 16 Mar 2068
>
>
>
>
> ----------------------------------------------------------------------------------
>
> case=1
> input=8
> 21 Oct 2053
> 07 Jun 1934
> 27 May 1934
> 21 Sep 1958
> 17 Mar 2068
> 26 May 1912
> 17 Dec 2012
> 27 Dec 2061
>
> output=26 May 1912
> 27 May 1934
> 07 Jun 1934
> 21 Sep 1958
> 17 Dec 2012
> 21 Oct 2053
> 27 Dec 2061
> 17 Mar 2068
>
> output=26 May 1912
> 27 May 1934
> 7 Jun 1934
> 21 Sep 1958
> 17 Dec 2012
> 21 Oct 2053
> 27 Dec 2061
> 17 Mar 2068
>
> case=2
> input=7
> 07 Jun 1934
> 07 Jun 1934
> 21 Sep 1958
> 17 Mar 2068
> 26 May 2012
> 17 Dec 2012
> 27 Dec 2061
>
> output=07 Jun 1934
> 07 Jun 1934
> 21 Sep 1958
> 26 May 2012
> 17 Dec 2012
> 27 Dec 2061
> 17 Mar 2068
>
> output=7 Jun 1934
> 7 Jun 1934
> 21 Sep 1958
> 26 May 2012
> 17 Dec 2012
> 27 Dec 2061
> 17 Mar 2068
>
> case=3
> input=3
> 07 Jan 1934
> 07 Dec 1934
> 21 Sep 1934
>
> output=07 Jan 1934
> 21 Sep 1934
> 07 Dec 1934
>
> output=7 Jan 1934
> 21 Sep 1934
> 7 Dec 1934
>
>  * 
>  */
> import java.io.*;
> import java.text.SimpleDateFormat;
> import java.util.*;
> public class SortDates {
> 	public static void main(String args[]) throws Exception {
>
> 		ArrayList<Date> date = new ArrayList<>();
> 		SimpleDateFormat format = new SimpleDateFormat("d MMM yyyy");
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		int numOfDates = Integer.parseInt(br.readLine());
> 		for (int i = 0; i < numOfDates; i++) {
> 			Date date1 = format.parse(br.readLine());
> 			date.add(date1);
> 		}
>
> 		Collections.sort(date);
> 		date.forEach(action -> System.out.println(format.format(action)));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2041%20Solutions/SortDates.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/SortDates.java
