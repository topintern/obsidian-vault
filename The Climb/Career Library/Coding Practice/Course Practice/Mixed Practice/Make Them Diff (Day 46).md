---
kind: "coding-problem"
title: "Make Them Diff (Day 46)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/MakeThemDiff.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Make Them Diff (Day 46)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given a sequence A of N integers: A1,A2,A3... AN.

You would like to make all elements in A different. To do so, you may perform operations 
of two types:

Remove an element. The cost of this operation is X coins.
Decrease the value of an element by one. The cost is Y coins.
You may perform as many operations as you wish.
It is possible and allowed that some elements will become negative
(after you decrease an element multiple times).

Your task is to find the minimum number of coins you would need in order to 
make A pairwise distinct.


### Input Format

------------
The first line contains three space-separated integers N, X, and Y 
		— the size of the sequence and costs of operations.
The second line contains N space-separated integers A1,A2,A3...AN
		— the initial sequence.


### Output Format

-------------
Print one integer — the minimum number of coins needed to make A pairwise distinct.




### Sample Input 

6 10 3
5 2 5 3 5 2


### Sample Output 

16


### Explanation 

we are given a sequence of size n=6.
The cost of removing and decreasing by one are 10 and 3 respectively.

The initial sequence is (5 2 5 3 5 2).
One optimal strategy is:

Remove one of three fives, e.g. the middle one. The remaining sequence is (5 2 3 5 2).
Decrease the second element by one, to get (5 1 3 5 2).
Decrease the first element by one, to get (4 1 3 5 2).
This way, you need to spend 10+3+3 =16 coins. 
The resulting sequence(4 1 3 5 2) is indeed pairwise distinct.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MakeThemDiff.java
> ```java
> /*
>  * 
> You are given a sequence A of N integers: A1,A2,A3... AN.
>
> You would like to make all elements in A different. To do so, you may perform operations 
> of two types:
>
> Remove an element. The cost of this operation is X coins.
> Decrease the value of an element by one. The cost is Y coins.
> You may perform as many operations as you wish.
> It is possible and allowed that some elements will become negative
> (after you decrease an element multiple times).
>
> Your task is to find the minimum number of coins you would need in order to 
> make A pairwise distinct.
>
> Input Format
> ------------
> The first line contains three space-separated integers N, X, and Y 
> 		— the size of the sequence and costs of operations.
> The second line contains N space-separated integers A1,A2,A3...AN
> 		— the initial sequence.
>
> Output Format
> -------------
> Print one integer — the minimum number of coins needed to make A pairwise distinct.
>
>
>
> Sample Input :
> 6 10 3
> 5 2 5 3 5 2
>
> Sample Output :
> 16
>
> Explanation :
> we are given a sequence of size n=6.
> The cost of removing and decreasing by one are 10 and 3 respectively.
>
> The initial sequence is (5 2 5 3 5 2).
> One optimal strategy is:
>
> Remove one of three fives, e.g. the middle one. The remaining sequence is (5 2 3 5 2).
> Decrease the second element by one, to get (5 1 3 5 2).
> Decrease the first element by one, to get (4 1 3 5 2).
> This way, you need to spend 10+3+3 =16 coins. 
> The resulting sequence(4 1 3 5 2) is indeed pairwise distinct.
>
>  */
>
> import java.util.*;
>
> public class MakeThemDiff {
>     public static void main(String args[] ) throws Exception {
>       
>         Scanner sc = new Scanner(System.in);
>         int n = sc.nextInt();
>         int x = sc.nextInt();
>         int y = sc.nextInt();
>         long cost = 0;
>         int[] a = new int[n];
>         for(int i=0;i<n;i++)
>         {
>             a[i] = sc.nextInt();
>         }
>         Arrays.sort(a);
>         HashMap<Integer,Integer> distinctNumbers = new HashMap<Integer,Integer>();
>         for(int i=0;i<n;i++)
>         {
>             int h = a[i];
>             if(distinctNumbers.containsKey(h))
>             {
>                 int cnt = 0;
>                 //repeat until number not found, decrement it ,increase the count 
>                 //and check for decremented value 
>                 while(distinctNumbers.containsKey(h))
>                 {
>                     h--;
>                     cnt+=1;
>                 }
>                 //check whether removal costs more or decrement costs more
>                 if(cnt*y>x)
>                 {
>                     cost+=x;
>                 }
>                 else
>                 {
>                     cost+=cnt*y;
>                     distinctNumbers.put(h,1);//add decremented number to list
>                 }
>             }
>             else
>             {
>             	distinctNumbers.put(h,1);
>             }
>         }
>         System.out.println(cost);
>     }
> }
>
>
>
> /*
> ======TestCases======
> case =1
> input =6 10 3
> 5 2 5 3 5 2
> output =16
>
> case =2
> input =15 3 2
> 10 10 10 10 10 7 7 7 7 7 8 8 8 8 8
> output =34
>
> case =3
> input =25 7 5
> 78 65 45 34 87 78 65 45 45 34 54 34 23 32 23 23 34 52 67 45 78 79 65 65 66 
> output =81
>
> case =4
> input =31 10 8
> 78 65 45 34 87 78 65 45 45 34 54 34 23 32 23 23 34 52 67 45 78 79 65 65 66 5 2 5 3 5 2
> output =146
>
> case =5
> input =50 12 11
> 103 23 45 67 23 89 103 89 23 45 33 32 32 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95
> output =328
>
> case =6
> input =80 17 14
> 103 23 45 67 23 89 103 89 23 45 33 32 32 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95 78 65 45 34 87 78 65 45 45 34 54 34 23 32 23 23 34 52 67 45 78 79 65 65 66 5 2 5 3 5
> output =840
>
> case =7
> input =80 4 5
> 103 23 45 67 23 89 103 89 23 45 33 32 32 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95 78 65 45 34 87 78 65 45 45 34 54 34 23 32 23 23 34 52 67 45 78 79 65 65 66 5 2 5 3 5
> output =204
>
> case =8
> input =100 12 6
> 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 6 7 8 9 10 1 2 3 4 5 26 27 28 29 30 31 32 33 34 35 6 7 8 9 10 41 42 43 44 45 6 7 8 9 10 51 52 53 54 5 6 7 8 9 10 61 62 63 6 5 6 7 8 9 10 71 72 3 4 5 6 7 81 9 90 1 2 3 4 5 6 7 8 9 100 1 2 3 4 5 6 7 8 9 10
> output =690
>
> case =9
> input =150 12 11
> 103 23 45 67 23 89 103 89 23 45 33 32 32 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 6 7 8 9 10 1 2 3 4 5 26 27 28 29 30 31 32 33 34 35 6 7 8 9 10 41 42 43 44 45 6 7 8 9 10 51 52 53 54 5 6 7 8 9 10 61 62 63 6 5 6 7 8 9 10 71 72 3 4 5 6 7 81 9 90 1 2 3 4 5 6 7 8 9 100 1 2 3 4 5 6 7 8 9 10
> output =1169
>
> case =10
> input =500 3 7
> 6 70 42 44 93 46 54 27 57 77 41 80 74 68 52 87 80 61 34 39 76 40 74	21	63	13	53	46	97	24	71	97	5	60	4	92	7	82	95	68	29	12	47	62	21	96	4	73	62	99	37	18	66	84	96	36	93	21	32	84	85	46	33	31	39	44	54	88	74	58	63	78	12	76	89	96	48	97	2	5	44	51	12	76	46	25	71	93	39	86	70	39	62	9	71	93	63	14	25	56	83	81	68	29	3	55	14	73	31	47	59	37	89	8	49	5	41	54	79	63	82	63	16	88	50	32	70	58	58	48	49	9	27	11	71	11	92	32	28	14	33	49	20	89	38	96	51	55	53	48	47	72	39	75	13	86	40	38	11	97	6	68	91	5	77	42	72	11	57	18	28	98	59	95	95	12	82	15	21	55	7	98	100	90	69	5	21	55	27	40	19	50	84	83	63	34	65	27	27	16	70	3	89	26	28	49	15	52	87	60	72	82	76	8	5	65	80	79	38	9	30	65	78	85	88	38	69	21	7	78	23	41	52	28	83	37	58	65	50	9	6	53	88	75	54	5	17	51	38	31	80	39	38	20	82	18	66	9	20	16	83	21	39	70	59	62	77	77	65	95	42	85	19	80	10	83	92	34	72	60	9	56	86	51	3	25	81	11	84	82	100	56	59	20	76	96	90	5	72	2	23	74	5	43	66	56	50	75	32	34	42	19	44	83	22	24	74	6	10	51	75	39	72	99	52	81	96	61	53	48	4	80	22	5	72	79	72	21	24	38	93	29	39	28	58	77	79	84	28	36	44	53	12	38	6	73	92	86	39	35	57	76	49	74	37	13	44	97	49	17	32	62	17	95	52	6	50	96	97	23	54	45	27	97	100	38	15	58	68	11	33	69	96	15	73	37	12	21	97	31	18	35	78	49	21	49	49	68	96	69	47	25	48	53	21	98	30	74	31	15	10	59	72	2	17	96	90	88	44	73	2	54	29	43	44	8	74	30	40	84	55	13	12	29	92	40	13	56	58	19	37	3	64	45	41	15	94	10	37	73	71	11	59	54	20	53	81	19	90	20	7	37 64 73 35 83 46 94 73 47 42 26 20 52 24 16 73 64 61 45 35 50 91 92 22 1 31 88 25 51
> output =1203
>
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2046%20Solutions/MakeThemDiff.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/MakeThemDiff.java
