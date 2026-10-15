---
kind: "coding-problem"
title: "Castle Stones (Day 54)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/CastleStones.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Castle Stones (Day 54)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Phineas is Building a castle in his backyard to impress Isabella ( strange, isn't it? ). 
He has got everything delivered and ready. Even the ground floor has been finished. 
Now is time to make the upper part. This is where the things become interesting. 
As Ferb is sleeping in the house after a long day painting the fence (and you folks helped him, didn't ya!),
Phineas has to do all the work himself. He is good at this, 
and all he wants you to do is operate the mini crane to lift the stones. 
Stones for the wall has been cut and ready waiting for you to lift them up.

Now we don't have Ferb to operate the mini crane, in which he is an expert, 
we got to do the job as quick as possible. 
We are given the maximum lifting capacity of the crane, and the weight of each stone. 
Since it's a mini crane, we cannot place more then 2 stones (of any possible size) at a time, 
or it will disturb the balance of the crane. 
we need to find out in how many turns we can deliver the stones to Phineas, 
who is building the castle.

INPUT: first line gives M, the maximum lifting capacity of the crane. 
second line , first integer N of next line gives the number of stones, 
followed by N numbers, specifying the weight of individual stone X.

OUTPUT:print the minimum number of turns the crane is operated for all stones to be lifted.


### Sample Output

6
5 3 5 4 2 1


### Sample Output

3


### Explanation

Minimum number of turns required are 3.
One of the way of transporting stones in 3 turns is to transport as (1,5),(2,3) and (4).

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CastleStones.java
> ```java
> /*
>  * 
> Phineas is Building a castle in his backyard to impress Isabella ( strange, isn't it? ). 
> He has got everything delivered and ready. Even the ground floor has been finished. 
> Now is time to make the upper part. This is where the things become interesting. 
> As Ferb is sleeping in the house after a long day painting the fence (and you folks helped him, didn't ya!),
> Phineas has to do all the work himself. He is good at this, 
> and all he wants you to do is operate the mini crane to lift the stones. 
> Stones for the wall has been cut and ready waiting for you to lift them up.
>
> Now we don't have Ferb to operate the mini crane, in which he is an expert, 
> we got to do the job as quick as possible. 
> We are given the maximum lifting capacity of the crane, and the weight of each stone. 
> Since it's a mini crane, we cannot place more then 2 stones (of any possible size) at a time, 
> or it will disturb the balance of the crane. 
> we need to find out in how many turns we can deliver the stones to Phineas, 
> who is building the castle.
>
> INPUT: first line gives M, the maximum lifting capacity of the crane. 
> second line , first integer N of next line gives the number of stones, 
> followed by N numbers, specifying the weight of individual stone X.
>
> OUTPUT:print the minimum number of turns the crane is operated for all stones to be lifted.
>
> Sample Output:
> 6
> 5 3 5 4 2 1
>
> Sample Output:
> 3
>
> Explanation:
> Minimum number of turns required are 3.
> One of the way of transporting stones in 3 turns is to transport as (1,5),(2,3) and (4).
>
>
>  * 
>  */
>
> import java.util.*;
>  
> class CastleStones {
>     public static void main(String args[] ) throws Exception {
> 	
> 	    Scanner sc=new Scanner(System.in);
> 		int m=sc.nextInt();
> 		int n=sc.nextInt();
> 		int arr[]=new int[n];
> 		for(int j=0;j<n;j++)
> 			arr[j]=sc.nextInt();
> 		Arrays.sort(arr);
> 		int x=n-1;
> 		int j=0,count=0;
> 		while(j<=x)
> 			{
> 				if((arr[j]+arr[x])<=m )
> 					{
> 						count++;
> 						j++;x--;
> 					}
> 				else if(arr[x]>m)
> 						x--;
> 				else
> 					{
> 						count++;
> 						x--;
> 					}
> 			}
> 		System.out.println(count);
>         
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2054%20Solutions/CastleStones.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/CastleStones.java
