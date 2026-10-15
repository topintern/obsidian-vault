---
kind: "coding-problem"
title: "Synonym (Day 11)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/synonym.py"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Synonym (Day 11)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · synonym.py
> ```python
> '''
>
>                             Online Python Compiler.
>                 Code, Compile, Run and Debug python program online.
> Write your code in this editor and press "Run" button to execute it.
>
> '''
> import collections
> d  = collections.OrderedDict()
> n=int(input())
> for i in range(n):
>     a=input().split(" ")
>     d[a[0]]=a[1]
> s=input().split(" ")
> k = next(iter(d))
> while k in d.keys():
>     if(k in s):
>         print(" ".join(s)+",")
>         for i in s[s.index(k)+1::]:
>             if i in d.keys():
>                  a=i
>                  b=s.index(i)
>                  s[s.index(i)]=d[i]
>         print(" ".join(s)+",")
>         s[b]=a
>         s[s.index(k)]=d[k]
>         k=d[k]
> print(" ".join(s)+",")
> for i in s[s.index(k)+1::]:
>     if i in d.keys():
>         s[s.index(i)]=d[i]
> print(" ".join(s)+",")
>
>     
>
> '''
> 3
> happy joy
> sad sorrow
> joy cheerful
> I am happy today but was sad yesterday
>
> '''
>
>
>
> '''
> synonyms = [["happy","joy"],["sad","sorrow"],["joy","cheerful"]],
> text = "I am happy today but was sad yesterday"
> Output:
> ["I am cheerful today but was sad yesterday",
> ​​​​​​​"I am cheerful today but was sorrow yesterday",
> "I am happy today but was sad yesterday",
> "I am happy today but was sorrow yesterday",
> "I am joy today but was sad yesterday",
> "I am joy today but was sorrow yesterday"]
> '''
> ```

## Source provenance

- [Original PY](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2011%20Solutions/synonym.py) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/synonym.py
