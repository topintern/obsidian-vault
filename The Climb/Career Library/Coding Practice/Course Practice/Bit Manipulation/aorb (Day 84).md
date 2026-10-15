---
kind: "coding-problem"
title: "aorb (Day 84)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/aorb-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/AorB.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# aorb (Day 84)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*********Testcases**********
case =1
input =25
B631EB5AE
601C227E1
707AC8792
output=C8582
707A00790

case =2
input =12
CAF7028FD
59B5AC1CE
CAF1B7B7F
output=8AF10287D
48B1B534E

case =3
input =3
81B9BB94E
8AB3CA95E
8BBBFB95E
output=B9BB94E
8BB3CA95E

case =4
input =8
2B
9F
58
output =8
58

case =5
input =5
B9
40
5A
output =18
42

case =6
input =2
91
BE
A8
output =-1

case =7
input =54
8CC5695B3A257A0BB671
833A22A3496652BBC06F
D85125CEB4F372EA58D9
output =14A3021720A1051
D851248684F252EA48C9    

case =8
input =15
3F66A12A7140652C2076
FBD297715038F9E9B032
6728C54E5C4572709E1E
output =-1

case =9
input =4
E7E66B003B1D1829ED65
3D5998EC58F84B900C3C
FFFFFBEC7BFD5BB9ED7D
output =27E66B003B1D1829ED65
FD5998EC58F84B900C3C

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · AorB.java
> ```java
> /*
> **********Testcases**********
> case =1
> input =25
> B631EB5AE
> 601C227E1
> 707AC8792
> output=C8582
> 707A00790
>
> case =2
> input =12
> CAF7028FD
> 59B5AC1CE
> CAF1B7B7F
> output=8AF10287D
> 48B1B534E
>
> case =3
> input =3
> 81B9BB94E
> 8AB3CA95E
> 8BBBFB95E
> output=B9BB94E
> 8BB3CA95E
>
> case =4
> input =8
> 2B
> 9F
> 58
> output =8
> 58
>
> case =5
> input =5
> B9
> 40
> 5A
> output =18
> 42
>
> case =6
> input =2
> 91
> BE
> A8
> output =-1
>
> case =7
> input =54
> 8CC5695B3A257A0BB671
> 833A22A3496652BBC06F
> D85125CEB4F372EA58D9
> output =14A3021720A1051
> D851248684F252EA48C9    
>
> case =8
> input =15
> 3F66A12A7140652C2076
> FBD297715038F9E9B032
> 6728C54E5C4572709E1E
> output =-1
>
> case =9
> input =4
> E7E66B003B1D1829ED65
> 3D5998EC58F84B900C3C
> FFFFFBEC7BFD5BB9ED7D
> output =27E66B003B1D1829ED65
> FD5998EC58F84B900C3C
>
> */
>
> import java.util.*;
> import java.math.*;
>
> public class Solution {
>     public static void main(String[] args) {
>         Scanner sc = new Scanner(System.in);
>         int q = sc.nextInt();
>         for (int i = 0; i < q; i++) {
>             int k = sc.nextInt();
>             sc.nextLine();
>             String as = sc.nextLine();
>             String bs = sc.nextLine();
>             String cs = sc.nextLine();
>             int maxLen = Math.max(as.length(), Math.max(bs.length(), cs.length()));
>             StringBuilder temp = new StringBuilder();
>             for (int j = as.length(); j < maxLen; j++)
>                 temp.append('0');
>             as = temp.toString()+as;
>             temp = new StringBuilder();
>             for (int j = bs.length(); j < maxLen; j++)
>                 temp.append('0');
>             bs = temp.toString()+bs;
>             temp = new StringBuilder();
>             for (int j = cs.length(); j < maxLen; j++)
>                 temp.append('0');
>             cs = temp.toString()+cs;
>             int[] a = new int[maxLen*4];
>             int[] b = new int[maxLen*4];
>             int[] c = new int[maxLen*4];
>             
>             for (int j = 0; j < maxLen; j++) {
>                 int ai = Integer.parseInt(""+as.charAt(j), 16);
>                 a[j*4+0] = (ai/8)%2;
>                 a[j*4+1] = (ai/4)%2;
>                 a[j*4+2] = (ai/2)%2;
>                 a[j*4+3] = (ai/1)%2;
>                 int bi = Integer.parseInt(""+bs.charAt(j), 16);
>                 b[j*4+0] = (bi/8)%2;
>                 b[j*4+1] = (bi/4)%2;
>                 b[j*4+2] = (bi/2)%2;
>                 b[j*4+3] = (bi/1)%2;
>                 int ci = Integer.parseInt(""+cs.charAt(j), 16);
>                 c[j*4+0] = (ci/8)%2;
>                 c[j*4+1] = (ci/4)%2;
>                 c[j*4+2] = (ci/2)%2;
>                 c[j*4+3] = (ci/1)%2;
>             }
>             
>             for (int j = 0; j < maxLen*4; j++) {
>                 if (c[j]==0) {
>                     if (a[j] == 1) {
>                         a[j] = 0;
>                         k--;
>                     }
>                     if (b[j] == 1) {
>                         b[j] = 0;
>                         k--;
>                     }
>                 } else if (a[j] == 0 && b[j] == 0) {
>                     b[j] = 1;
>                     k--;
>                 }
>             }
>             
>             if (k < 0) {
>                 System.out.println(-1);
>                 continue;
>             }
>             
>             for (int j = 0; j < maxLen*4; j++) {
>                 if (c[j]==1) {
>                     if (a[j]==1&&b[j]==1&&k>=1) {
>                         a[j] = 0;
>                         k--;
>                     }
>                     if (a[j]==1&&b[j]==0&&k>=2) {
>                         a[j] = 0;
>                         b[j] = 1;
>                         k-=2;
>                     }
>                 }
>             }
>             
>             StringBuilder ap = new StringBuilder();
>             StringBuilder bp = new StringBuilder();
>             boolean az = false;
>             boolean bz = false;
>             
>             for (int j = 0; j < maxLen; j++) {
>                 char num = Integer.toHexString(a[j*4+0]*8+a[j*4+1]*4+a[j*4+2]*2+a[j*4+3]*1).toUpperCase().charAt(0);
>                 if (num != '0' || az || j == maxLen-1) {
>                 	ap.append(num);
>                 	az = true;
>                 }
>                 num = Integer.toHexString(b[j*4+0]*8+b[j*4+1]*4+b[j*4+2]*2+b[j*4+3]*1).toUpperCase().charAt(0);
>                 if (num != '0' || bz || j == maxLen-1) {
>                 	bp.append(num);
>                 	bz = true;
>                 }
>             }
>             System.out.println(ap.toString());
>             System.out.println(bp.toString());
>         }
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/aorb-English-e360021a.pdf|aorb-English-e360021a.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/aorb-English-e360021a.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2084%20Solutions/aorb-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/aorb-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2084%20Solutions/AorB.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/AorB.java
