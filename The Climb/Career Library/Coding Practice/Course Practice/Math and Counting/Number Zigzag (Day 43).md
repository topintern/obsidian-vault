---
kind: "coding-problem"
title: "Number Zigzag (Day 43)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/NumberZigzag.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Number Zigzag (Day 43)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a number N denoting the number of rows. 
The task is to print the zigzag pattern with N rows as shown in 
the below example.

Note: Based type of 'N' (i.e Priority Order is 1. Prime 2. Even 3. Odd)
Example-1:
Input : 
        6
Output : 
        1 
        3 2 
        4 5 6 
        10 9 8 7 
        11 12 13 14 15
        21 20 19 18 17 16

Example-2:
Input : 
        3
Output : 
        1 
        2 3 
        4 5 6 
        
Example-3:
Input : 
        9
Output : 
        1 
        2 3 
        6 5 4
        7 8 9 10
        15 14 13 12 11
        16 17 18 19 20 21 
        28 27 26 25 24 23 22
        29 30 31 32 33 34 35 36 
        45 44 43 42 41 40 39 38 37

 
----------TestCases-----------
case =1
input =5
output =1 
2 3 
4 5 6 
7 8 9 10 
11 12 13 14 15 

case =2
input =6
output =1 
3 2 
4 5 6 
10 9 8 7 
11 12 13 14 15 
21 20 19 18 17 16 

case =3
input =4
output =1 
3 2 
4 5 6 
10 9 8 7 

case =4
input =3
output =1 
2 3 
4 5 6 

case =5
input =8
output =1 
3 2 
4 5 6 
10 9 8 7 
11 12 13 14 15 
21 20 19 18 17 16 
22 23 24 25 26 27 28 
36 35 34 33 32 31 30 29 

case =6
input =7
output =1 
2 3 
4 5 6 
7 8 9 10 
11 12 13 14 15 
16 17 18 19 20 21 
22 23 24 25 26 27 28 

case =7
input =1
output =1

case =8
input =2
output =1
2 3

case =9
input =9
output =1 
2 3 
6 5 4 
7 8 9 10 
15 14 13 12 11 
16 17 18 19 20 21 
28 27 26 25 24 23 22 
29 30 31 32 33 34 35 36 
45 44 43 42 41 40 39 38 37 

case =10
input =10
output =1 
3 2 
4 5 6 
10 9 8 7 
11 12 13 14 15
21 20 19 18 17 16
22 23 24 25 26 27 28
36 35 34 33 32 31 30 29
37 38 39 40 41 42 43 44 45 
55 54 53 52 51 50 49 48 47 46 

case =11
input =11
output =1 
2 3 
4 5 6 
7 8 9 10 
11 12 13 14 15  
16 17 18 19 20 21 
22 23 24 25 26 27 28 
29 30 31 32 33 34 35 36 
37 38 39 40 41 42 43 44 45 
46 47 48 49 50 51 52 53 54 55 
56 57 58 59 60 61 62 63 64 65 66

case =12
input =-2
output =-1

case =13
input =0
output =-1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NumberZigzag.txt
> ```java
> /*
>  * 
>  
>  Given a number N denoting the number of rows. 
> The task is to print the zigzag pattern with N rows as shown in 
> the below example.
>
> Note: Based type of 'N' (i.e Priority Order is 1. Prime 2. Even 3. Odd)
> Example-1:
> Input : 
>         6
> Output : 
>         1 
>         3 2 
>         4 5 6 
>         10 9 8 7 
>         11 12 13 14 15
>         21 20 19 18 17 16
>
> Example-2:
> Input : 
>         3
> Output : 
>         1 
>         2 3 
>         4 5 6 
>         
> Example-3:
> Input : 
>         9
> Output : 
>         1 
>         2 3 
>         6 5 4
>         7 8 9 10
>         15 14 13 12 11
>         16 17 18 19 20 21 
>         28 27 26 25 24 23 22
>         29 30 31 32 33 34 35 36 
>         45 44 43 42 41 40 39 38 37
>
>  
> ----------TestCases-----------
> case =1
> input =5
> output =1 
> 2 3 
> 4 5 6 
> 7 8 9 10 
> 11 12 13 14 15 
>
> case =2
> input =6
> output =1 
> 3 2 
> 4 5 6 
> 10 9 8 7 
> 11 12 13 14 15 
> 21 20 19 18 17 16 
>
> case =3
> input =4
> output =1 
> 3 2 
> 4 5 6 
> 10 9 8 7 
>
> case =4
> input =3
> output =1 
> 2 3 
> 4 5 6 
>
> case =5
> input =8
> output =1 
> 3 2 
> 4 5 6 
> 10 9 8 7 
> 11 12 13 14 15 
> 21 20 19 18 17 16 
> 22 23 24 25 26 27 28 
> 36 35 34 33 32 31 30 29 
>
> case =6
> input =7
> output =1 
> 2 3 
> 4 5 6 
> 7 8 9 10 
> 11 12 13 14 15 
> 16 17 18 19 20 21 
> 22 23 24 25 26 27 28 
>
> case =7
> input =1
> output =1
>
> case =8
> input =2
> output =1
> 2 3
>
> case =9
> input =9
> output =1 
> 2 3 
> 6 5 4 
> 7 8 9 10 
> 15 14 13 12 11 
> 16 17 18 19 20 21 
> 28 27 26 25 24 23 22 
> 29 30 31 32 33 34 35 36 
> 45 44 43 42 41 40 39 38 37 
>
> case =10
> input =10
> output =1 
> 3 2 
> 4 5 6 
> 10 9 8 7 
> 11 12 13 14 15
> 21 20 19 18 17 16
> 22 23 24 25 26 27 28
> 36 35 34 33 32 31 30 29
> 37 38 39 40 41 42 43 44 45 
> 55 54 53 52 51 50 49 48 47 46 
>
> case =11
> input =11
> output =1 
> 2 3 
> 4 5 6 
> 7 8 9 10 
> 11 12 13 14 15  
> 16 17 18 19 20 21 
> 22 23 24 25 26 27 28 
> 29 30 31 32 33 34 35 36 
> 37 38 39 40 41 42 43 44 45 
> 46 47 48 49 50 51 52 53 54 55 
> 56 57 58 59 60 61 62 63 64 65 66
>
> case =12
> input =-2
> output =-1
>
> case =13
> input =0
> output =-1
>
>  * 
>  */
>
> import java.util.*;
> class NumberZigzag
> {
>  public static void main (String[] args) {
>     
>     Scanner sc=new Scanner(System.in);
>     int n=sc.nextInt();
>     int flag=0;
>     if(n<=0)
>     {
>         System.out.println("-1");
>     }
>     else if(n==2 || checkPrime(n))
>     {
>         int c=1;
>         for(int i=1;i<=n;i++)
>         {
>             for(int j=1;j<=i;j++)
>             {
>                 System.out.print(c+" ");
>                 c++;
>             }
>             System.out.println();
>         }
>     }
>     else if(n%2==0)
>     {
>      System.out.println("1");
>      flag=1;
>      int c=2;
>      for(int i=2;i<=n;i++)
>      {
>          if(flag==1)
>          {
>          int k=c+i-1;
>          for(int j=1;j<=i;j++)
>          {
>              System.out.print(k+" ");
>              k--;
>          }
>          c=c+i;
>          flag=0;
>          }
>          else
>          {
>              for(int j=1;j<=i;j++)
>              {
>                  System.out.print(c+" ");
>                  c++;
>              }
>              flag=1;
>          }
>          System.out.println();
>          
>      }
>     }
>     else 
>     {
>      System.out.println("1");
>      flag=0;
>      int c=2;
>      for(int i=2;i<=n;i++)
>      {
>          if(flag==1)
>          {
>          int k=c+i-1;
>          for(int j=1;j<=i;j++)
>          {
>              System.out.print(k+" ");
>              k--;
>          }
>          c=c+i;
>          flag=0;
>          }
>          else
>          {
>              for(int j=1;j<=i;j++)
>              {
>                  System.out.print(c+" ");
>                  c++;
>              }
>              flag=1;
>          }
>          System.out.println();
>          
>      }
>     }
>  }
>  public static boolean checkPrime(int n)
>  {
>      for(int i=2;i<n;i++)
>      {
>          if(n%i==0)
>          {
>              return false;
>          }
>      }
>      return true;
>  }
>  
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2043%20Solutions/NumberZigzag.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/NumberZigzag.txt
