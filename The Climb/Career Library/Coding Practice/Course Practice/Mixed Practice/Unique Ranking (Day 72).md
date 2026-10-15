---
kind: "coding-problem"
title: "Unique Ranking (Day 72)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/UniqueRanking.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Unique Ranking (Day 72)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The end sem exams at are over. Sneh is the class teacher of class X/C. 
She now has the hectic task of preparing the report card of her class.

Since Sneh is a computer teacher she tried to infuse some fun into his task.
Sneh knew that there are n students in class and they had k subjects. 
Subjects are numbered from 1 to k and students have unique id from 1 to n. 
She now wanted to know which student performed the worst in a group of subjects. 
She ordered those group priority wise that is if the group contained 
subjects 1 ,3 and 5 then while determining the worst performer initially 
subject 1 will be taken in consideration and only those students who have 
performed worst in subject 1(there might be a tie) will be considered 
for the next subject that is subject 3 and the rest will be eliminated 
and ultimately after all the subjects are considered the worst performer will be determined. 
If after considering all the subjects there is a tie among few students then
the student with the smallest id will be the worst performer. 

Help Sneh in determining the worst performer of his class.

Input Format:
-------------
First line contains n that is the number of students and k that is the 
toal number of subjects. 
The next n line contains k integers denoting the marks obtained by 
the students in k subjects. 
the next line contains
xn which indicates the number of subjects to be considered and 
then contains xn distinct integers(x1,x2,x3 ..) indicating the subjects to be considered 
arranged priority wise.

Output Format:
-------------
prints the unique id of the worst performer of the class.


### Sample Input 

---------------
3 3
50 60 70
40 60 80
50 60 61
3 1 2 3



### Sample Output 

---------------
2


### Explanation 

--------------

we have to consider 3 subjects .First subject to consider 
priority wise is 1 and the worst performer in this subject is 2 and 
since there is no tie this is the final answer.


========= Testcases Program-1 =========
case =1
input =3 3
50 60 70
40 60 80
50 60 61
3 1 2 3
output =2

case =2
input =3 4
50 60 70 80
40 60 80 90
50 60 61 65
4 2 3 4 1
output =3

case =3
input =4 4
50 60 70 80
50 60 61 65
40 60 80 90
50 60 61 65
4 2 3 4 1
output =2

case =4
input =6 3
50 60 70
40 60 80
50 60 61
50 60 70
50 60 75
40 60 78
3 1 2 3
output =6

case =5
input =4 4
50 60 70 80
50 60 61 65
40 60 80 90
50 58 61 65
4 4 1 3 2
output =4

case =5
input =6 6
50 60 70 80 70 85
50 60 61 65 70 84
40 60 80 80 70 84
50 60 61 65 70 84
40 60 56 80 70 84
50 62 61 65 70 84
6 5 6 2 1 4 3
output =5

case =7
input =8 4
50 60 70 80
50 60 61 65
40 60 80 90
50 58 61 65
50 60 70 80
50 60 61 65
40 60 80 90
50 55 61 65
4 4 1 3 2
output =8

case =8
input =9 6
50 60 70 80 70 85
50 60 61 65 70 84
40 60 80 80 70 84
50 60 56 65 70 84
50 62 55 65 70 84
50 60 54 80 70 85
50 60 61 65 70 84
40 60 59 80 70 84
40 60 52 80 70 84
6 5 6 2 1 4 3
output =9

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · UniqueRanking.java
> ```java
> /*
>
> The end sem exams at are over. Sneh is the class teacher of class X/C. 
> She now has the hectic task of preparing the report card of her class.
>
> Since Sneh is a computer teacher she tried to infuse some fun into his task.
> Sneh knew that there are n students in class and they had k subjects. 
> Subjects are numbered from 1 to k and students have unique id from 1 to n. 
> She now wanted to know which student performed the worst in a group of subjects. 
> She ordered those group priority wise that is if the group contained 
> subjects 1 ,3 and 5 then while determining the worst performer initially 
> subject 1 will be taken in consideration and only those students who have 
> performed worst in subject 1(there might be a tie) will be considered 
> for the next subject that is subject 3 and the rest will be eliminated 
> and ultimately after all the subjects are considered the worst performer will be determined. 
> If after considering all the subjects there is a tie among few students then
> the student with the smallest id will be the worst performer. 
>
> Help Sneh in determining the worst performer of his class.
>
> Input Format:
> -------------
> First line contains n that is the number of students and k that is the 
> toal number of subjects. 
> The next n line contains k integers denoting the marks obtained by 
> the students in k subjects. 
> the next line contains
> xn which indicates the number of subjects to be considered and 
> then contains xn distinct integers(x1,x2,x3 ..) indicating the subjects to be considered 
> arranged priority wise.
>
> Output Format:
> -------------
> prints the unique id of the worst performer of the class.
>
> Sample Input :
> ---------------
> 3 3
> 50 60 70
> 40 60 80
> 50 60 61
> 3 1 2 3
>
>
> Sample Output :
> ---------------
> 2
>
> Explanation :
> --------------
>
> we have to consider 3 subjects .First subject to consider 
> priority wise is 1 and the worst performer in this subject is 2 and 
> since there is no tie this is the final answer.
>
>
> ========= Testcases Program-1 =========
> case =1
> input =3 3
> 50 60 70
> 40 60 80
> 50 60 61
> 3 1 2 3
> output =2
>
> case =2
> input =3 4
> 50 60 70 80
> 40 60 80 90
> 50 60 61 65
> 4 2 3 4 1
> output =3
>
> case =3
> input =4 4
> 50 60 70 80
> 50 60 61 65
> 40 60 80 90
> 50 60 61 65
> 4 2 3 4 1
> output =2
>
> case =4
> input =6 3
> 50 60 70
> 40 60 80
> 50 60 61
> 50 60 70
> 50 60 75
> 40 60 78
> 3 1 2 3
> output =6
>
> case =5
> input =4 4
> 50 60 70 80
> 50 60 61 65
> 40 60 80 90
> 50 58 61 65
> 4 4 1 3 2
> output =4
>
> case =5
> input =6 6
> 50 60 70 80 70 85
> 50 60 61 65 70 84
> 40 60 80 80 70 84
> 50 60 61 65 70 84
> 40 60 56 80 70 84
> 50 62 61 65 70 84
> 6 5 6 2 1 4 3
> output =5
>
> case =7
> input =8 4
> 50 60 70 80
> 50 60 61 65
> 40 60 80 90
> 50 58 61 65
> 50 60 70 80
> 50 60 61 65
> 40 60 80 90
> 50 55 61 65
> 4 4 1 3 2
> output =8
>
> case =8
> input =9 6
> 50 60 70 80 70 85
> 50 60 61 65 70 84
> 40 60 80 80 70 84
> 50 60 56 65 70 84
> 50 62 55 65 70 84
> 50 60 54 80 70 85
> 50 60 61 65 70 84
> 40 60 59 80 70 84
> 40 60 52 80 70 84
> 6 5 6 2 1 4 3
> output =9
>
>
>
>
> */
>
>
> import java.util.Scanner;
>
> public class UniqueRanking {
>  
>  
>     public static void main(String args[] ) throws Exception {
>        
>        
>        Scanner sc = new Scanner(System.in);
>        int n = sc.nextInt();//number of students
>        int k = sc.nextInt();//number of subjects
>        int [][]a=new int [n][k];
>        
>        
>        for(int i=0;i<n;i++)
>        {   
>            for(int j=0;j<k;j++)
>            {
>                a[i][j]= sc.nextInt();//reading subject wise marks of each student
>            }
>            
>        }
>        
>            int l=sc.nextInt();//number of subjects to be considered for priority
>            int []order=new int[l];
>            for(int j=0;j<l;j++) order[j]=sc.nextInt();//reading subjects priority
>            
>            
>            boolean []b=new boolean[n];
>            
>            for(int x=0;x<l;x++)
>            {
>                int minvalue=Integer.MAX_VALUE;
>                int temp=order[x]-1;
>                for(int y=0;y<n;y++)
>                {
>                    //find worst performer who has minimum marks
>                    if(!b[y] && a[y][temp]<minvalue) 
>                    {
>                        minvalue=a[y][temp];
>                    }
>                    
>                    
>                }
>                int count=0;
>                for(int y=0;y<n;y++)
>                {
>                //mark the student(s) as worst performer by assigning "false" 
>                if(!b[y] && a[y][temp]==minvalue) {b[y]=false;count++;}
>                else b[y]=true;
>                }
>                if(count==1) break;
>                
>            }
>            /*
>             If after considering all the subjects there is a tie among few students 
>             then the student with the smallest id will be the worst performer
>             */
>            for(int x=0;x<n;x++)
>            if(b[x]==false) {System.out.println(x+1);}
>        
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2072%20Solutions/UniqueRanking.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/UniqueRanking.java
