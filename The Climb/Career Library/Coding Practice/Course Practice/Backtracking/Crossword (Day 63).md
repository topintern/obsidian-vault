---
kind: "coding-problem"
title: "Crossword (Day 63)"
collection: "Course Practice"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 63 Solutions/Crossword.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Crossword (Day 63)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A 10*10 Crossword grid is provided to you, along with a set of words (or names of places) 
which need to be filled into the grid. Cells are marked either + or -. Cells marked 
with a - are to be filled with the word list.

The following shows an example crossword from the input crossword grid and the list of words to fit, :

Input 	   				Output

++++++++++ 		++++++++++
+------+++ 			+POLAND+++
+++-++++++ 		+++H++++++
+++-++++++ 		+++A++++++
+++-----++ 			+++SPAIN++
+++-++-+++ 		+++A++N+++
++++++-+++ 		++++++D+++
++++++-+++ 		++++++I+++
++++++-+++ 		++++++A+++
++++++++++ 		++++++++++

POLAND;	LHASA;	SPAIN;	INDIA

Input Format:
Each of the first 10 lines represents crossword[i], each of which has 10 characters, crossword[i][j].
The last line contains a string consisting of semicolon delimited words[i] to fit.

Output Format:
Position the words appropriately in the 10*10 grid, then return your array of strings for printing.

Sample Input1:
	+-++++++++
	+-++++++++
	+-++++++++
	+-----++++
	+-+++-++++
	+-+++-++++
	+++++-++++
	++------++
	+++++-++++
	+++++-++++
	LONDON;DELHI;ICELAND;ANKARA

Sample Output1:
	+L++++++++
	+O++++++++
	+N++++++++
	+DELHI++++
	+O+++C++++
	+N+++E++++
	+++++L++++
	++ANKARA++
	+++++N++++
	+++++D++++
	
	
Sample Input2:
	+-++++++++
	+-++++++++
	+-------++
	+-++++++++
	+-++++++++
	+------+++
	+-+++-++++
	+++++-++++
	+++++-++++
	++++++++++
	AGRA;NORWAY;ENGLAND;GWALIOR
Sample Output2:
	+E++++++++
	+N++++++++
	+GWALIOR++
	+L++++++++
	+A++++++++
	+NORWAY+++
	+D+++G++++
	+++++R++++
	+++++A++++
	++++++++++


Sample Input3:
	XXXXXX-XXX
	XX------XX
	XXXXXX-XXX
	XXXXXX-XXX
	XXX------X
	XXXXXX-X-X
	XXXXXX-X-X
	XXXXXXXX-X
	XXXXXXXX-X
	XXXXXXXX-X
	ICELAND;MEXICO;PANAMA;ALMATY

Sample Output3:
	XXXXXXIXXX
	XXMEXICOXX
	XXXXXXEXXX
	XXXXXXLXXX
	XXXPANAMAX
	XXXXXXNXLX
	XXXXXXDXMX
	XXXXXXXXAX
	XXXXXXXXTX
	XXXXXXXXYX

========= Testcases Program-2 =========
case =1
input =+-++++++++
+-++++++++
+-++++++++
+-----++++
+-+++-++++
+-+++-++++
+++++-++++
++------++
+++++-++++
+++++-++++
LONDON;DELHI;ICELAND;ANKARA
output =+L++++++++
+O++++++++
+N++++++++
+DELHI++++
+O+++C++++
+N+++E++++
+++++L++++
++ANKARA++
+++++N++++
+++++D++++

case =2
input =+-++++++++
+-++++++++
+-------++
+-++++++++
+-++++++++
+------+++
+-+++-++++
+++++-++++
+++++-++++
++++++++++
AGRA;NORWAY;ENGLAND;GWALIOR
output =+E++++++++
+N++++++++
+GWALIOR++
+L++++++++
+A++++++++
+NORWAY+++
+D+++G++++
+++++R++++
+++++A++++
++++++++++

case =3
input =+-++++++++
+-++-+++++
+-------++
+-++-+++++
+-++-+++++
+-++-+++++
++++-+++++
++++-+++++
++++++++++
----------
CALIFORNIA;NIGERIA;CANADA;TELAVIV
output =+C++++++++
+A++T+++++
+NIGERIA++
+A++L+++++
+D++A+++++
+A++V+++++
++++I+++++
++++V+++++
++++++++++
CALIFORNIA

case =4
input =+-++++++++
+-++-+++++
+-------++
+-++-++-++
+-++-++-++
+-++-++-++
++++-++-++
+--------+
++++++++++
----------
CALIFORNIA;LASVEGAS;NIGERIA;CANADA;TELAVIV;ALASKA
output =+C++++++++
+A++T+++++
+NIGERIA++
+A++L++L++
+D++A++A++
+A++V++S++
++++I++K++
+LASVEGAS+
++++++++++
CALIFORNIA

case =5
input =+-++++++++
+-++++++++
+-------++
+-++++++++
+-----++++
+-+++-++++
+++-----++
+++++-++++
+++++-++++
+++++-++++
SYDNEY;TURKEY;DETROIT;EGYPT;PARIS
output =+S++++++++
+Y++++++++
+DETROIT++
+N++++++++
+EGYPT++++
+Y+++U++++
+++PARIS++
+++++K++++
+++++E++++
+++++Y++++

case =6
input =+----+++++
++++-+++++
++++-+++++
++++------
++++-+++-+
++++-+++-+
++++-+++-+
++++-+++-+
++++-+++++
++++++++++
TREE;ELEPHANTS;PICKLE;LEMON
output =+TREE+++++
++++L+++++
++++E+++++
++++PICKLE
++++H+++E+
++++A+++M+
++++N+++O+
++++T+++N+
++++S+++++
++++++++++

case =7
input =+-++++++++
+-------++
+-++-+++++
+-------++
+-++-++++-
+-++-++++-
+-++------
+++++++++-
++++++++++
++++++++++
ANDAMAN;MANIPUR;ICELAND;ALLEPY;YANGON;PUNE
output =+M++++++++
+ANDAMAN++
+N++L+++++
+ICELAND++
+P++E++++P
+U++P++++U
+R++YANGON
+++++++++E
++++++++++
++++++++++

case =8
input =XXXXXX-XXX
XX------XX
XXXXXX-XXX
XXXXXX-XXX
XXX------X
XXXXXX-X-X
XXXXXX-X-X
XXXXXXXX-X
XXXXXXXX-X
XXXXXXXX-X
ICELAND;MEXICO;PANAMA;ALMATY
output =XXXXXXIXXX
XXMEXICOXX
XXXXXXEXXX
XXXXXXLXXX
XXXPANAMAX
XXXXXXNXLX
XXXXXXDXMX
XXXXXXXXAX
XXXXXXXXTX
XXXXXXXXYX

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Crossword.java
> ```java
> /*
> A 10*10 Crossword grid is provided to you, along with a set of words (or names of places) 
> which need to be filled into the grid. Cells are marked either + or -. Cells marked 
> with a - are to be filled with the word list.
>
> The following shows an example crossword from the input crossword grid and the list of words to fit, :
>
> Input 	   				Output
>
> ++++++++++ 		++++++++++
> +------+++ 			+POLAND+++
> +++-++++++ 		+++H++++++
> +++-++++++ 		+++A++++++
> +++-----++ 			+++SPAIN++
> +++-++-+++ 		+++A++N+++
> ++++++-+++ 		++++++D+++
> ++++++-+++ 		++++++I+++
> ++++++-+++ 		++++++A+++
> ++++++++++ 		++++++++++
>
> POLAND;	LHASA;	SPAIN;	INDIA
>
> Input Format:
> Each of the first 10 lines represents crossword[i], each of which has 10 characters, crossword[i][j].
> The last line contains a string consisting of semicolon delimited words[i] to fit.
>
> Output Format:
> Position the words appropriately in the 10*10 grid, then return your array of strings for printing.
>
> Sample Input1:
> 	+-++++++++
> 	+-++++++++
> 	+-++++++++
> 	+-----++++
> 	+-+++-++++
> 	+-+++-++++
> 	+++++-++++
> 	++------++
> 	+++++-++++
> 	+++++-++++
> 	LONDON;DELHI;ICELAND;ANKARA
>
> Sample Output1:
> 	+L++++++++
> 	+O++++++++
> 	+N++++++++
> 	+DELHI++++
> 	+O+++C++++
> 	+N+++E++++
> 	+++++L++++
> 	++ANKARA++
> 	+++++N++++
> 	+++++D++++
> 	
> 	
> Sample Input2:
> 	+-++++++++
> 	+-++++++++
> 	+-------++
> 	+-++++++++
> 	+-++++++++
> 	+------+++
> 	+-+++-++++
> 	+++++-++++
> 	+++++-++++
> 	++++++++++
> 	AGRA;NORWAY;ENGLAND;GWALIOR
> Sample Output2:
> 	+E++++++++
> 	+N++++++++
> 	+GWALIOR++
> 	+L++++++++
> 	+A++++++++
> 	+NORWAY+++
> 	+D+++G++++
> 	+++++R++++
> 	+++++A++++
> 	++++++++++
>
>
> Sample Input3:
> 	XXXXXX-XXX
> 	XX------XX
> 	XXXXXX-XXX
> 	XXXXXX-XXX
> 	XXX------X
> 	XXXXXX-X-X
> 	XXXXXX-X-X
> 	XXXXXXXX-X
> 	XXXXXXXX-X
> 	XXXXXXXX-X
> 	ICELAND;MEXICO;PANAMA;ALMATY
>
> Sample Output3:
> 	XXXXXXIXXX
> 	XXMEXICOXX
> 	XXXXXXEXXX
> 	XXXXXXLXXX
> 	XXXPANAMAX
> 	XXXXXXNXLX
> 	XXXXXXDXMX
> 	XXXXXXXXAX
> 	XXXXXXXXTX
> 	XXXXXXXXYX
>
> ========= Testcases Program-2 =========
> case =1
> input =+-++++++++
> +-++++++++
> +-++++++++
> +-----++++
> +-+++-++++
> +-+++-++++
> +++++-++++
> ++------++
> +++++-++++
> +++++-++++
> LONDON;DELHI;ICELAND;ANKARA
> output =+L++++++++
> +O++++++++
> +N++++++++
> +DELHI++++
> +O+++C++++
> +N+++E++++
> +++++L++++
> ++ANKARA++
> +++++N++++
> +++++D++++
>
> case =2
> input =+-++++++++
> +-++++++++
> +-------++
> +-++++++++
> +-++++++++
> +------+++
> +-+++-++++
> +++++-++++
> +++++-++++
> ++++++++++
> AGRA;NORWAY;ENGLAND;GWALIOR
> output =+E++++++++
> +N++++++++
> +GWALIOR++
> +L++++++++
> +A++++++++
> +NORWAY+++
> +D+++G++++
> +++++R++++
> +++++A++++
> ++++++++++
>
> case =3
> input =+-++++++++
> +-++-+++++
> +-------++
> +-++-+++++
> +-++-+++++
> +-++-+++++
> ++++-+++++
> ++++-+++++
> ++++++++++
> ----------
> CALIFORNIA;NIGERIA;CANADA;TELAVIV
> output =+C++++++++
> +A++T+++++
> +NIGERIA++
> +A++L+++++
> +D++A+++++
> +A++V+++++
> ++++I+++++
> ++++V+++++
> ++++++++++
> CALIFORNIA
>
> case =4
> input =+-++++++++
> +-++-+++++
> +-------++
> +-++-++-++
> +-++-++-++
> +-++-++-++
> ++++-++-++
> +--------+
> ++++++++++
> ----------
> CALIFORNIA;LASVEGAS;NIGERIA;CANADA;TELAVIV;ALASKA
> output =+C++++++++
> +A++T+++++
> +NIGERIA++
> +A++L++L++
> +D++A++A++
> +A++V++S++
> ++++I++K++
> +LASVEGAS+
> ++++++++++
> CALIFORNIA
>
> case =5
> input =+-++++++++
> +-++++++++
> +-------++
> +-++++++++
> +-----++++
> +-+++-++++
> +++-----++
> +++++-++++
> +++++-++++
> +++++-++++
> SYDNEY;TURKEY;DETROIT;EGYPT;PARIS
> output =+S++++++++
> +Y++++++++
> +DETROIT++
> +N++++++++
> +EGYPT++++
> +Y+++U++++
> +++PARIS++
> +++++K++++
> +++++E++++
> +++++Y++++
>
> case =6
> input =+----+++++
> ++++-+++++
> ++++-+++++
> ++++------
> ++++-+++-+
> ++++-+++-+
> ++++-+++-+
> ++++-+++-+
> ++++-+++++
> ++++++++++
> TREE;ELEPHANTS;PICKLE;LEMON
> output =+TREE+++++
> ++++L+++++
> ++++E+++++
> ++++PICKLE
> ++++H+++E+
> ++++A+++M+
> ++++N+++O+
> ++++T+++N+
> ++++S+++++
> ++++++++++
>
> case =7
> input =+-++++++++
> +-------++
> +-++-+++++
> +-------++
> +-++-++++-
> +-++-++++-
> +-++------
> +++++++++-
> ++++++++++
> ++++++++++
> ANDAMAN;MANIPUR;ICELAND;ALLEPY;YANGON;PUNE
> output =+M++++++++
> +ANDAMAN++
> +N++L+++++
> +ICELAND++
> +P++E++++P
> +U++P++++U
> +R++YANGON
> +++++++++E
> ++++++++++
> ++++++++++
>
> case =8
> input =XXXXXX-XXX
> XX------XX
> XXXXXX-XXX
> XXXXXX-XXX
> XXX------X
> XXXXXX-X-X
> XXXXXX-X-X
> XXXXXXXX-X
> XXXXXXXX-X
> XXXXXXXX-X
> ICELAND;MEXICO;PANAMA;ALMATY
> output =XXXXXXIXXX
> XXMEXICOXX
> XXXXXXEXXX
> XXXXXXLXXX
> XXXPANAMAX
> XXXXXXNXLX
> XXXXXXDXMX
> XXXXXXXXAX
> XXXXXXXXTX
> XXXXXXXXYX
>
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class Crossword {
>  
>     private static void print(char[][] board) {
>         for (int r = 0; r < 10; r++) {
>             System.out.println(new String(board[r]));
>         }
>     }
>  
>     private static boolean solve(char[][] board, List<String> words, List<Integer[]> h, List<Integer[]> v, Set<String> used) {
>  
>         if (used.size() == words.size()) {
>             print(board);
>             return true;
>         }
>  
>         for (String w : words) {
>             if (!used.contains(w)) {
>  
>                 // HORIZONTAL
>  
>                 for (Integer[] pos : h) {
>                     int row = pos[0];
>                     int col = pos[1];
>                     boolean fit = true;
>  
>                     // Backup
>                     char[] backup = Arrays.copyOf(board[row], 10);
>  
>                     // Place the word
>                     for (int i = col; i < col + w.length(); i++) {
>                         if (i >= 10 || board[row][i] == '+' || (board[row][i] != '-' && board[row][i] != w.charAt(i - col))) {
>                             fit = false;
>                             break;
>                         }
>                         board[row][i] = w.charAt(i - col);
>                     }
>  
>                     // Recursive call
>                     if (fit) {
>                         used.add(w);
>                         boolean found = solve(board, words, h, v, used);
>  
>                         if (found) {
>                             return true;
>                         }
>  
>                         used.remove(w);
>                     }
>  
>                     // Restore
>                     board[row] = Arrays.copyOf(backup, 10);
>                 }
>  
>                 // VERTICAL
>  
>                 for (Integer[] pos : v) {
>                     int row = pos[0];
>                     int col = pos[1];
>                     boolean fit = true;
>  
>                     // Backup
>                     char[] backup = new char[10];
>                     for (int r = 0; r < 10; r++) {
>                         backup[r] = board[r][col];
>                     }
>  
>                     // Place the word
>                     for (int i = row; i < row + w.length(); i++) {
>                         if (i >= 10 || board[i][col] == '+' || (board[i][col] != '-' && board[i][col] != w.charAt(i - row))) {
>                             fit = false;
>                             break;
>                         }
>                         board[i][col] = w.charAt(i - row);
>                     }
>  
>                     // Recursive call
>                     if (fit) {
>                         used.add(w);
>                         boolean found = solve(board, words, h, v, used);
>  
>                         if (found) {
>                             return true;
>                         }
>                         used.remove(w);
>                     }
>  
>                     // Restore
>                     for (int r = 0; r < 10; r++) {
>                         board[r][col] = backup[r];
>                     }
>                 }
>  
>             }
>         }
>  
>         return false;
>     }
>  
>     public static void main(String[] args) {
>         //System.setIn(new FileInputStream(System.getProperty("user.home") + "/" + "in.txt"));
>         Scanner in = new Scanner(System.in);
>  
>         char[][] board = new char[10][10];
>         for (int r = 0; r < 10; r++) {
>             board[r] = in.next().toCharArray();
>         }
>  
>         String[] w = in.next().split(";");
>  
>         List<String> words = new ArrayList<String>();
>         for (String word : w) {
>             words.add(word);
>         }
>  
>         // Precompute possible word starting positions: left most column of horizontal '-..-' lines
>         // or top most row of vertical lines '-..-'.
>         List<Integer[]> h = new ArrayList<Integer[]>();
>         List<Integer[]> v = new ArrayList<Integer[]>();
>         for (int r = 0; r < 10; r++) {
>             for (int c = 0; c < 10; c++) {
>                 if (board[r][c] == '-') {
>                     // HORIZONTAL
>                     // Go all the way to the left
>                     int start = c;
>                     while (start > 0 && board[r][start - 1] == '-') {
>                         start--;
>                     }
>                     h.add(new Integer[] { r, start });
>  
>                     // VERTICAL
>                     // Go all the way up
>                     start = r;
>                     while (start > 0 && board[start - 1][c] == '-') {
>                         start--;
>                     }
>                     v.add(new Integer[] { start, c });
>                 }
>             }
>         }
>  
>         solve(board, words, h, v, new HashSet<String>());
>     }
>  
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2063%20Solutions/Crossword.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 63 Solutions/Crossword.java
