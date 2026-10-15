---
kind: "coding-problem"
title: "Journey To Moon (Day 70)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 70 Solutions/JourneyToMoon.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Journey To Moon (Day 70)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The member states of the UN are planning to send 2 people to the moon. 
They want them to be from different countries. 
You will be given a list of pairs of astronaut ID's. 
Each pair is made of astronauts from the same country. 
Determine how many pairs of astronauts from different countries they can choose from.

For example, we have the following data on 2 pairs of astronauts, and 4 astronauts total, 
numbered 0 through 3.
1   2
2   3
Astronauts by country are [0] and [1,2,3]. 
There are 3 pairs to choose from: [0,1], [0,2] and [0,3].

Input Format:
The first line contains two integers n and p, the number of astronauts and the number of pairs.
Each of the next p lines contains 2 space-separated integers denoting astronaut ID's 
of two who share the same nationality.


### Output Format

- An integer that denotes the number of ways to choose a pair of astronauts from different coutries.

Sample Input1:
5 3
0 1
2 3
0 4
Sample Output1:
6
Explanation1:
Persons numbered [0,1,4] belong to one country, 
and those numbered [2,3] belong to another. 
The UN has 6 ways of choosing a pair:
[0,2],[0,3],[1,2],[1,3],[4,2],[4,3]

Sample Input2:
4 1
0 2
Sample Output2:
5
Explanation2:
Persons numbered [0,2] belong to the same country, 
but persons 1 and 3 don't share countries with anyone else. 
The UN has 5 ways of choosing a pair:
[0,1],[0,3],[2,1],[2,3],[1,3]


========= Testcases Program-2 =========
case =1
input =4 1
0 2
output =5

case =2
input =5 3
0 1
2 3
0 4
output =6

case =3
input =6 3
1 2
3 4
1 4
output =9

case =4
input =8 5
0 1
2 3
4 2
5 6
0 5
output =19

case =5
input =7 4
0 1
1 2
2 3
3 4
output =11

case =6
input =9 5
0 1
2 3
3 4
4 5
1 6
output =27

case =7
input =9 6
0 1
1 2
3 4
4 5
5 6
6 7
output =23

case =8
input =10 5
1 8
2 7
3 6
4 5
5 9
output =39

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · JourneyToMoon.java
> ```java
> /*
> The member states of the UN are planning to send 2 people to the moon. 
> They want them to be from different countries. 
> You will be given a list of pairs of astronaut ID's. 
> Each pair is made of astronauts from the same country. 
> Determine how many pairs of astronauts from different countries they can choose from.
>
> For example, we have the following data on 2 pairs of astronauts, and 4 astronauts total, 
> numbered 0 through 3.
> 1   2
> 2   3
> Astronauts by country are [0] and [1,2,3]. 
> There are 3 pairs to choose from: [0,1], [0,2] and [0,3].
>
> Input Format:
> The first line contains two integers n and p, the number of astronauts and the number of pairs.
> Each of the next p lines contains 2 space-separated integers denoting astronaut ID's 
> of two who share the same nationality.
>
> Output Format
> - An integer that denotes the number of ways to choose a pair of astronauts from different coutries.
>
> Sample Input1:
> 5 3
> 0 1
> 2 3
> 0 4
> Sample Output1:
> 6
> Explanation1:
> Persons numbered [0,1,4] belong to one country, 
> and those numbered [2,3] belong to another. 
> The UN has 6 ways of choosing a pair:
> [0,2],[0,3],[1,2],[1,3],[4,2],[4,3]
>
> Sample Input2:
> 4 1
> 0 2
> Sample Output2:
> 5
> Explanation2:
> Persons numbered [0,2] belong to the same country, 
> but persons 1 and 3 don't share countries with anyone else. 
> The UN has 5 ways of choosing a pair:
> [0,1],[0,3],[2,1],[2,3],[1,3]
>
>
> ========= Testcases Program-2 =========
> case =1
> input =4 1
> 0 2
> output =5
>
> case =2
> input =5 3
> 0 1
> 2 3
> 0 4
> output =6
>
> case =3
> input =6 3
> 1 2
> 3 4
> 1 4
> output =9
>
> case =4
> input =8 5
> 0 1
> 2 3
> 4 2
> 5 6
> 0 5
> output =19
>
> case =5
> input =7 4
> 0 1
> 1 2
> 2 3
> 3 4
> output =11
>
> case =6
> input =9 5
> 0 1
> 2 3
> 3 4
> 4 5
> 1 6
> output =27
>
> case =7
> input =9 6
> 0 1
> 1 2
> 3 4
> 4 5
> 5 6
> 6 7
> output =23
>
> case =8
> input =10 5
> 1 8
> 2 7
> 3 6
> 4 5
> 5 9
> output =39
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class JourneyToMoon {
> 	static Map<Integer,ArrayList<Integer>> planets=new HashMap<Integer,ArrayList<Integer>>();
> 	static Map<Integer,ArrayList<Integer>> components=new HashMap<Integer,ArrayList<Integer>>();
> 	public static void main(String args[]) throws IOException {
> 		BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
> 		String s=br.readLine();
> 		int n=Integer.parseInt(s.split(" ")[0]), k=Integer.parseInt(s.split(" ")[1]);
> 		int a1,a2,temp;
> 		for(int i=1;i<=n;i++) planets.put(i, new ArrayList<Integer>());
> 		StringTokenizer st;
> 		for(int i=0;i<k;i++) {
> 			st=new StringTokenizer(br.readLine());
> 			a1=Integer.parseInt(st.nextToken()); a2=Integer.parseInt(st.nextToken());
> 			planets.get(a1+1).add(a2+1);
> 			planets.get(a2+1).add(a1+1);
> 		}
> 		int offset=1,el,neighbour,component=1;
> 		boolean isVisited[]=new boolean[n+1];
> 		Arrays.fill(isVisited, false);
> 		Queue<Integer> q=new LinkedList<Integer>();
> 		Iterator<Integer> itr;
> 		while(offset<n) {
> 			q.clear();
> 			//Search for first element which is not visited
> 			while(offset<n && isVisited[offset]) offset++;
> 			if(offset==n && isVisited[offset]) break;
> 			
> 			components.put(component, new ArrayList<Integer>());
> 			q.add(offset);
> 			components.get(component).add(offset);
> 			
> 			isVisited[offset]=true;
> 			while(q.size()>0) {
> 				el=q.remove();
> 				itr=planets.get(el).iterator();
> 				while(itr.hasNext()) {
> 					neighbour=itr.next();
> 					if(!isVisited[neighbour]) {
> 						isVisited[neighbour]=true;
> 						q.add(neighbour);
> 						components.get(component).add(neighbour);
> 					}
> 				}
> 			}
> 			component++;
> 		}
> 		int []a=new int[components.size()];
> 		itr=components.keySet().iterator();
> 		int i=0,sum=0;
> 		while(itr.hasNext()) {
> 			a[i]=components.get(itr.next()).size();
> 			sum+=a[i];
> 			i++;
> 		}
> 		long ways=0;
> 		for(i=0;i<a.length-1;i++) {
> 			sum-=a[i];
> 			ways+=a[i]*sum;
> 		}
> 		System.out.println(ways);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2070%20Solutions/JourneyToMoon.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 70 Solutions/JourneyToMoon.java
