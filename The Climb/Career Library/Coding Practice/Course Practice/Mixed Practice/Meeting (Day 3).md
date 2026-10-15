---
kind: "coding-problem"
title: "Meeting (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Meeting.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Meeting (Day 3)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

Example 1:

Input: 3
0 30
5 10 
15 20
Output: 2
Example 2:

Input: 2
7 10
2 4
Output: 1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Meeting.java
> ```java
>
>
> /*
>  * 
> Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.
>
> Example 1:
>
> Input: 3
> 0 30
> 5 10 
> 15 20
> Output: 2
> Example 2:
>
> Input: 2
> 7 10
> 2 4
> Output: 1
>
>  */
> import java.util.*;
> public class Meeting {
> 	    public static class myComparator implements Comparator<int[]>{
> 	        public int compare(int a[],int b[]){
> 	            return a[0]-b[0];
> 	        }
> 	    }
> 	    
> 	    public static int minMeetingRooms(int[][] intervals) {
> 	        if(intervals.length==0) return 0;
> 	        //sort the intervals according to its start time
> 	        Arrays.sort(intervals,new myComparator());
> 	        int room = 1;
> 	        
> 	        //use a priority queue to store the earliest end time
> 	        //if current time < earliest time, it means there is no task ends before current time, so #room+1
> 	        //if current time >= earliest time, it means when the task is over, there will be at least one empty room left 
> 	        
> 	        PriorityQueue<Integer> end_time = new PriorityQueue<Integer>();
> 	        for(int i=0;i<intervals.length;i++){
> 	            if(!end_time.isEmpty()){
> 	                int last_end_time = end_time.peek();
> 	                if(intervals[i][0]>=last_end_time){
> 	                    //this task is over
> 	                    end_time.poll();
> 	                }else{
> 	                    room++;
> 	                }
> 	            }
> 	            end_time.offer(intervals[i][1]);
> 	        }
> 	        return room;
> 	    }
> 	    public static void main(String args[] ) {
> 			 Scanner scan = new Scanner(System.in);
> 				int n=scan.nextInt();
> 				
> 				int[][] meetingtimes=new int[n][2];
> 			       for(int i=0; i<n; i++)
> 			       {
> 			           for(int j=0; j<2; j++)
> 			           {
> 			        	   meetingtimes[i][j] = scan.nextInt();
> 			           }
> 			       }
> 			       System.out.println(minMeetingRooms(meetingtimes));
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/Meeting.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Meeting.java
