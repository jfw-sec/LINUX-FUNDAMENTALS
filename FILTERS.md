## GREP
- It is used to search for patterns inside files.
- Basic syntax:
```
grep "pattern" filename
```
 - For example:
```
grep "hello" home.txt
```
- Shows all lines in the ***home.txt*** that contains the word ***hello***.
* * *
**IMPORTANT OPTIONS**
1. **IGNORE CASE (-i)**
- Ignores upper or lower cases in the word.
```
grep -i "Word" hello.txt
```
2. **SHOW LINE NUMBERS**
```
grep -n "word" hello.txt
```
3. **-c** - counts the found lines(matches).
4. **-o** - shows only the matches.
5. **-v** - shows the lines without the certain word.
6. **-w** - exact word matching.
7. **INSIDE FOLDERS**
```
grep -r "word"
```
8. **MATCH NUMBERS**
```
grep "[0-9]" hello.txt
```
9. **MATCH LINES THAT START WITH SOMETHING**
```
grep "^word" hello.txt
```
10. **MATCH LINES THAT END WITH SOMETHING**
```
grep "word$" hello.txt
```

![GREP.png](../_resources/GREP.png)
- For example:
![grep.png](../_resources/grep-1.png)
* * *

## HEAD 
- Is used to view a specific number of lines from the start/top of the file.
- Example:
```
head -n 3 file.txt  #read the first 3 lines of file.txt
```
##  TAIL 
- Used to view a specific number of lines at the bottom of the file.
- Example:
```
tail -n 3 file.txt  #read the last 3 lines of file.txt
```

- **NOTE** >> If you want to watch a log file (watching real time incoming requests to a server):
```
tail -f /var/log/syslog
```

## SORT 
- **sort** - sorts the lines in alphabetic or numerical order.
- **sort -n** - sorts the lines numerically in ascending order.
- **sort -rn** - sorts the lines numerically in descending order.

## UNIQ
- FIlters consequtively repeated files.
 - **uniq -c** - counts how many times each line appears consecutively and prints the count before of line.
- **uniq -u** - prints only the line that occurs once.

## WC (Word Count)
- Helps you understand how much data a file contains.
- Example:
![WORDCOUNT.png](../_resources/WORDCOUNT.png)
![WCexample.png](../_resources/WCexample.png)

## CUT
- Splits lines into specified columns .
- EXample:
![CUT.png](../_resources/CUT.png)
- **d** = delimiter , **f** = field

## AWK
- It reads lines and splits them into columns and processes them based on specified conditions.
![AWK.png](../_resources/AWK.png)

## SED 
- It is used for various edits like adding , deleting or replacing between files.
![SED.png](../_resources/SED.png)  

## DIFF
- Shows the difference btwn files.
![DIFF.png](../_resources/DIFF.png)

## TR
- Used to transform characters or character replacements.
![TR.png](../_resources/TR.png)
  
