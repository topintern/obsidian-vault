---
kind: "coding-problem"
title: "Bitonic Array (Day 38)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/BitonicArray.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Bitonic Array (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a bitonic sequence of n distinct elements, 
 write a program to find a given element x in the bitonic sequence in O(log n) time. 
 A Bitonic Sequence is a sequence of numbers which is first strictly increasing then 
 after a point strictly decreasing.

Examples:

Input : 
-3 9 8 20 17 5 1
20
Output :3

Input :
5 6 7 8 9 10 1 2 3
30
Output : -1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BitonicArray.txt
> ```java
> /*
>  * 
>  Given a bitonic sequence of n distinct elements, 
>  write a program to find a given element x in the bitonic sequence in O(log n) time. 
>  A Bitonic Sequence is a sequence of numbers which is first strictly increasing then 
>  after a point strictly decreasing.
>
> Examples:
>
> Input : 
> -3 9 8 20 17 5 1
> 20
> Output :3
>
> Input :
> 5 6 7 8 9 10 1 2 3
> 30
> Output : -1 
>
>
>
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class BitonicArray {
>
> 	// CPP code to search key in bitonic array  
> 	// Function for binary search in ascending part  
> 	    static int ascendingBinarySearch(int arr[], int low, 
> 	            int high, int key) { 
> 	        while (low <= high) { 
> 	            int mid = low + (high - low) / 2; 
> 	            if (arr[mid] == key) { 
> 	                return mid; 
> 	            } 
> 	            if (arr[mid] > key) { 
> 	                high = mid - 1; 
> 	            } else { 
> 	                low = mid + 1; 
> 	            } 
> 	        } 
> 	        return -1; 
> 	    } 
> 	  
> 	// Function for binary search in descending part of array  
> 	    static int descendingBinarySearch(int arr[], int low, 
> 	            int high, int key) { 
> 	        while (low <= high) { 
> 	            int mid = low + (high - low) / 2; 
> 	            if (arr[mid] == key) { 
> 	                return mid; 
> 	            } 
> 	            if (arr[mid] < key) { 
> 	                high = mid - 1; 
> 	            } else { 
> 	                low = mid + 1; 
> 	            } 
> 	        } 
> 	        return -1; 
> 	    } 
> 	  
> 	// finding bitonic point  
> 	    static int findBitonicPoint(int arr[], int n, int l, int r) { 
> 	        int mid; 
> 	  
> 	        mid = (r + l) / 2; 
> 	        if (arr[mid] > arr[mid - 1] && arr[mid] > arr[mid + 1]) { 
> 	            return mid; 
> 	        } else { 
> 	            if (arr[mid] > arr[mid - 1] && arr[mid] < arr[mid + 1]) { 
> 	                findBitonicPoint(arr, n, mid, r); 
> 	            } else { 
> 	                if (arr[mid] < arr[mid - 1] && arr[mid] > arr[mid + 1]) { 
> 	                    findBitonicPoint(arr, n, l, mid); 
> 	                } 
> 	            } 
> 	        } 
> 	        return mid; 
> 	    } 
> 	  
> 	// Function to search key in bitonic array  
> 	    static int searchBitonic(int arr[], int n, int key, int index) { 
> 	        if (key > arr[index]) { 
> 	            return -1; 
> 	        } else if (key == arr[index]) { 
> 	            return index; 
> 	        } else { 
> 	            int temp = ascendingBinarySearch(arr, 0, index - 1, key); 
> 	            if (temp != -1) { 
> 	                return temp; 
> 	            } 
> 	  
> 	            // Search in right of k  
> 	            return descendingBinarySearch(arr, index + 1, n - 1, key); 
> 	        } 
> 	    } 
> 	  
> 	// Driver program to test above function  
> 	    public static void main(String args[])  throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray(); 
> 	        int key; 
> 	        key=Integer.parseInt(br.readLine());
> 	        int n, l, r; 
> 	        n = arr.length; 
> 	        l = 0; 
> 	        r = n - 1; 
> 	        int index; 
> 	        index = findBitonicPoint(arr, n, l, r); 
> 	  
> 	        int x = searchBitonic(arr, n, key, index); 
> 	  
> 	        if (x == -1) { 
> 	            System.out.println("-1"); 
> 	        } else { 
> 	            System.out.println(x); 
> 	        } 
> 	  
> 	    } 
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/BitonicArray.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/BitonicArray.txt
