---
kind: "coding-problem"
title: "Indian Army (Day 50)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/IndianArmy.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Indian Army (Day 50)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Protection of the Indian border and safe transport of items from one point 
to another along the border are the paramount jobs for the Indian army. 
However they need some information about the protection status along the 
length of the border. The border can be viewed as the real x-axis. 
Along the axis, Indian army has N checkpoints for lookout.

We know that each checkpoint is located at an integer location xi. 
Each checkpoint must have a fleet of armed men which are responsible 
for guarding the neighboring areas of the checkpoint and provide 
military assistance of all kinds. The size of the fleet is based on 
the location of the checkpoint and how active the region is for terrorist activities.

Given the number of armed men assigned at the ith checkpoint, as pi, 
this information is available for all checkpoints.
With the skills of the armed men, it is known that if for the ith checkpoint, 
the length on the x axis that they can defend is a closed interval [xi-pi, xi+pi].

Now, your task is to transport some military items from position S to 
the end position E on the x-axis. 


### Input Format

------------
First line of the input contains 3 integers N, S and E. 
N is the number of checkpoints that the Indian Army has on the border.
Then N lines follow. ith line contains 2 integers, xi and pi.
0

### Output Format

-------------
Print the total distance of the x-axis from S to E, that is not protected by the armed forces.

Sample Input
5 229 8419
1795 95
4873 720
3149 81
6101 2325
3674 629
Sample Output
2626

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IndianArmy.java
> ```java
> /*
> Protection of the Indian border and safe transport of items from one point 
> to another along the border are the paramount jobs for the Indian army. 
> However they need some information about the protection status along the 
> length of the border. The border can be viewed as the real x-axis. 
> Along the axis, Indian army has N checkpoints for lookout.
>
> We know that each checkpoint is located at an integer location xi. 
> Each checkpoint must have a fleet of armed men which are responsible 
> for guarding the neighboring areas of the checkpoint and provide 
> military assistance of all kinds. The size of the fleet is based on 
> the location of the checkpoint and how active the region is for terrorist activities.
>
> Given the number of armed men assigned at the ith checkpoint, as pi, 
> this information is available for all checkpoints.
> With the skills of the armed men, it is known that if for the ith checkpoint, 
> the length on the x axis that they can defend is a closed interval [xi-pi, xi+pi].
>
> Now, your task is to transport some military items from position S to 
> the end position E on the x-axis. 
>
> Input Format
> ------------
> First line of the input contains 3 integers N, S and E. 
> N is the number of checkpoints that the Indian Army has on the border.
> Then N lines follow. ith line contains 2 integers, xi and pi.
> 0
> Output Format
> -------------
> Print the total distance of the x-axis from S to E, that is not protected by the armed forces.
>
> Sample Input
> 5 229 8419
> 1795 95
> 4873 720
> 3149 81
> 6101 2325
> 3674 629
> Sample Output
> 2626
>
> */
>
> import java.util.*;
>
> public class IndianArmy
> {
> 	
> 	static class pair implements Comparable<pair>
> 	{
> 		Long x, y;
> 		pair(long x,long y)
> 		{
> 			this.x=x;
> 			this.y=y;
> 		}
> 		public int compareTo(pair o) {
> 			return x.compareTo(o.x);
> 		}  
> 	}
> 	
> 	public static void main(String[] args)
> 	{
> 		
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int numCheckPoints =sc.nextInt();
> 		long startPos = sc.nextLong();
> 		long endPos = sc.nextLong();
> 		
> 		pair[] areaDefended = new pair[numCheckPoints];
> 		for(int i=0;i<numCheckPoints;i++)
> 		{
> 			long x = sc.nextLong();
> 			long p = sc.nextLong();
> 			areaDefended[i] = new pair(x-p,x+p);
> 		}
> 		
> 		Arrays.sort(areaDefended);
> 		ArrayList<pair> b = new ArrayList<pair>();
> 		
> 		long c = areaDefended[0].x;
> 		long d = areaDefended[0].y;
> 		
> 		//merging the defended segments if any
> 		for(int i=1;i<numCheckPoints;i++)
> 		{
> 			if(areaDefended[i].x<=d)
> 				d = Math.max(d, areaDefended[i].y);
> 			else
> 			{
> 				b.add(new pair(c,d));
> 				c = areaDefended[i].x;
> 				d = areaDefended[i].y;
> 			}
> 		}
> 		b.add(new pair(c,d));
> 		int i;
> 		long ans = 0;
> 		for(i=0;i<b.size();i++)
> 		{
> 			if(startPos>=endPos)
> 			{
> 				startPos = endPos;
> 				break;
> 			}
> 			//if starting position is in between current segment
> 			if(b.get(i).x<=startPos && startPos<=b.get(i).y)
> 				startPos = b.get(i).y;
> 			//if current segment is in between starting position & ending position
> 			else if(startPos<=b.get(i).x && endPos>=b.get(i).y)
> 			{
> 				ans+=b.get(i).x-startPos;
> 				startPos = b.get(i).y;
> 				
> 			}//if ending position lies between current segment
> 			else if(startPos<=b.get(i).x && endPos>=b.get(i).x &&  endPos<=b.get(i).y)
> 			{
> 				ans+=b.get(i).x-startPos;
> 				startPos = endPos;
> 			}
> 			//if starting position & ending position are before the current segment
> 			else if(startPos<=b.get(i).x && endPos<=b.get(i).x)
> 			{
> 				ans+=endPos-startPos;
> 				startPos = endPos;
> 			}
> 		}
> 		//add the distance which is not covered in above segments
> 		if(startPos<endPos)
> 			ans+=endPos-startPos;
> 		System.out.println(ans);
> 		
> 	}
> }
>
>
> /*
> ========= Testcases Program-1 =========
> case =1
> input =5 229 8419
> 1795 95
> 4873 720
> 3149 81
> 6101 2325
> 3674 629
> output =2626
>
> case =2
> input =5 229 8419
> 1795 95
> 229 720
> 3149 81
> 6101 2325
> 3674 629
> output =1906
>
> case =3
> input =5 229 1205
> 1795 95
> 100 100
> 3149 81
> 6101 2325
> 3674 629
> output =976
>
> case =4
> input =4 2325 3225 
> 1795 95
> 229 720
> 3149 81
> 6101 2325
> output =743
>
> case =5
> input =4 500 4500 
> 1795 95
> 229 720
> 3149 81
> 6101 2325
> output =2475
>
> case =6
> input =4 500 4500
> 1795 95
> 3149 81
> 3674 542
> 6501 1232
> output =2662
>
> case =7
> input =6 250 2500
> 500 123
> 1000 324
> 1350 467
> 1650 543
> 1900 1213
> 2800 1523
> output =180
>
> case =8
> input =6 250 5543
> 500 123
> 1663 324
> 2352 467
> 3657 543
> 4213 1213
> 5843 1523
> output =1024
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2050%20Solutions/IndianArmy.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/IndianArmy.java
