---
kind: "coding-problem"
title: "Alpha Code"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/alpha code q.txt","CODING RESOURCES/coding ninjas/Dp-1/alpha code s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Alpha Code

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Alice and Bob need to send secret messages to each other and are discussing ways to encode their messages:
Alice: “Let’s just use a very simple code: We’ll assign ‘A’ the code word 1, ‘B’ will be 2, and so on down to ‘Z’ being assigned 26.”

Bob: “That’s a stupid code, Alice. Suppose I send you the word ‘BEAN’ encoded as 25114. You could decode that in many different ways!”

Alice: “Sure you could, but what words would you get? Other than ‘BEAN’, you’d get ‘BEAAD’, ‘YAAD’, ‘YAN’, ‘YKD’ and ‘BEKD’. I think you would be able to figure out the correct decoding. And why would you send me the word ‘BEAN’ anyway?”

Bob: “OK, maybe that’s a bad example, but I bet you that if you got a string of length 5000 there would be tons of different decodings and with that many you would find at least two different ones that would make sense.”

Alice: “How many different decodings?”

Bob: “Jillions!”
For some reason, Alice is still unconvinced by Bob’s argument, so she requires a program that will determine how many decodings there can be for a given string using her code.

### Input

Input will consist of multiple input sets. Each set will consist of a single line of at most 5000 digits representing a valid encryption (for example, no line will begin with a 0). There will be no spaces between the digits. An input line of ‘0’ will terminate the input and should not be processed.

### Output

For each input set, output the number of possible decodings for the input string. Print your answer taking modulo "10^9+7"

### Sample Input

```text
25114
1111111111
3333333333
0
```

### Sample Output

```text
6
89
1
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · alpha code s.txt
> ```cpp
> #include<bits/stdc++.h>
> #define mod 1000000007
> using namespace std;
> int main()
> {
>     //freopen("input6.txt", "r", stdin);
>     //freopen("output6.txt", "w", stdout);
>     string s;
>     int n, i, x;
>     long long int A[5001];
>     while(1)
>     {
>         cin>>s;
>         if(s=="0")
>         break;
>         n=s.size();
>         for(i=0;i<5000;i++)
>             A[i]=0;
>         A[0]=1;
>         for(i=1;i<n;i++)
>         {
>             x=(s[i-1]-'0')*10+s[i]-'0';
>             if(s[i]!='0')
>                 A[i]=A[i-1];
>             if(x>=10&&x<=26&&i>1)
>                 A[i]+=A[i-2];
>             else if(x>=10&&x<=26)
>                 A[i]++;
>             A[i]=A[i]%mod;
>         }
>         cout<<A[n-1]<<endl;
>     }
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/alpha%20code%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/alpha code q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/alpha%20code%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/alpha code s.txt
