---
kind: "coding-problem"
title: "Synonymous Sentences (Day 11)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/SynonymousSentences.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Synonymous Sentences (Day 11)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of pairs of equivalent words synonyms and a sentence text, Return all possible synonymous sentences sorted lexicographically.
 

Example 1:

Input:
synonyms = [["happy","joy"],["sad","sorrow"],["joy","cheerful"]],
text = "I am happy today but was sad yesterday"
Output:
["I am cheerful today but was sad yesterday",
​​​​​​​"I am cheerful today but was sorrow yesterday",
"I am happy today but was sad yesterday",
"I am happy today but was sorrow yesterday",
"I am joy today but was sad yesterday",
"I am joy today but was sorrow yesterday"]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SynonymousSentences.java
> ```java
> /*
>  * 
>  Given a list of pairs of equivalent words synonyms and a sentence text, Return all possible synonymous sentences sorted lexicographically.
>  
>
> Example 1:
>
> Input:
> synonyms = [["happy","joy"],["sad","sorrow"],["joy","cheerful"]],
> text = "I am happy today but was sad yesterday"
> Output:
> ["I am cheerful today but was sad yesterday",
> ​​​​​​​"I am cheerful today but was sorrow yesterday",
> "I am happy today but was sad yesterday",
> "I am happy today but was sorrow yesterday",
> "I am joy today but was sad yesterday",
> "I am joy today but was sorrow yesterday"]
>  
>  
>  
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
> import java.util.stream.Collectors;
>
> public class SynonymousSentences {
>
> 	 public static List<String> generateSentences(List<List<String>> synonyms, String text) {
> 	        Map<String, List<String>> graph = new HashMap<>();
> 	        for (List<String> synonymPair : synonyms) {
> 	            String w1 = synonymPair.get(0), w2 = synonymPair.get(1);
> 	            connect(graph, w1, w2);
> 	            connect(graph, w2, w1);
> 	        }
> 	        // BFS
> 	        Set<String> ans = new TreeSet<>();
> 	        Queue<String> q = new LinkedList<>();
> 	        q.add(text);
> 	        while (!q.isEmpty()) {
> 	            String out = q.remove();
> 	            ans.add(out); // Add to result
> 	            String[] words = out.split("\\s");
> 	            for (int i = 0; i < words.length; i++) {
> 	                String word = words[i];
> 	                if (graph.get(word) == null) continue;
> 	                for (String neighbor : graph.get(word)) {
> 	                    words[i] = neighbor;
> 	                    String newText = Arrays.stream(words).collect(Collectors.joining(" "));
> 	                    if (!ans.contains(newText)) q.add(newText);
> 	                }
> 	            }
> 	        }
> 	        return new ArrayList<>(ans);
> 	    }
>
> 	    private static void connect(Map<String, List<String>> graph, String v1, String v2) {
> 	        if (graph.get(v1) == null) graph.put(v1, new LinkedList<>());
> 	        graph.get(v1).add(v2);
> 	    }
> 	    
> 	    public static void main(String args[] ) throws IOException {
> 			 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 				int n=Integer.parseInt(br.readLine());
> 				List<List<String>> synonyms = new ArrayList<List<String>>();
> 				
>
> 			       for(int i=0; i<n; i++)
> 			       {
> 			    	   List<String> combi = new ArrayList<String>();
>
> 			          
> 			        	  String line=br.readLine();
> 			        	  String words[]=line.split(" ");
> 			        	   combi.add(words[0]);
> 			        	   combi.add(words[1]);
> 			   			
> 			          
> 			           synonyms.add(combi);
> 			         
> 			           
> 			       }
> 			      // System.out.println(synonyms);
> 			      String text =br.readLine();
> 			      System.out.println(generateSentences(synonyms,text));
> 		}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2011%20Solutions/SynonymousSentences.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 11 Solutions/SynonymousSentences.java
