## WORKING IN DIRECTORIES
* * *
```
pwd
```
- Lists your current directory path.
```
touch <name>
```
- Used to create a file .
- If file already exists it updates the timestamp.
  ```
  touch file{1..3}.txt
  ```
- Used to create a batch of files at once

* * *
```
mkdir <name>
```
- Used to create a directory.
```
mkdir -p Storage/local/user/Documents`
```
- Used to create parent directories .
```
tree .
```
- Is used to see the whole structure of the parent directories u've created.

* * *

```
mv <name> Storage/
```
- Moves the file (name) to the Srorage directory .
```
mv old.txt new.txt
```
- Also can be used to rename file.

* * *

```
cp <name> home/Documents
```
- Copies the file into the document folder.
- ![Linux copy options.png](../_resources/Linux%20copy%20options.png)

  
* * *
**DELETION (rm)**
![Linux Deletion.png](../_resources/Linux%20Deletion.png)

* * *

```
nano <name>
```
- When u want to edit a file , it will open the nano editor that allows u to edit the file.

```
which <name>
```
- Return the path of of the file.

```
find -options
```
- used to find info about a file, the options include ![linux file conf.png](../_resources/linux%20file%20conf.png)
  
* * *

```
locate *.conf
```
- Used to find finds of a certain type , for this instance all '.conf' files.
**NOTE//**
```
find . -exec file {} \;
```
  -This means , "**Find every file  here, and for each one here, run 'file' on it**"
* * *
## FILE DESCRIPTORS AND REDIRECTORS
-**STDIN - 0**
- **STDOUT - 1**
- **STDERR - 2**
- So for example we can redirect STDERR output to the dev/null file to get rid of them

```
find /etc/ -name shadow 2>/dev/null
```

* * *
```
du -h 
```
- Shows how much space files and directories are using in a human readable form.

* * *
## FILTERING CONTENTS
1. **HEAD**
- Used when u want to read only the first lines of a file, specifically the first ten lines if not specified otherwise.
```
head /etc/passwd
```
2. **TAIL**
- Returns the last ten lines of a file unless specified otherwise.
```
tail /etc/passwd
```
3. **SORT**
- Is used to sort the output of files alphabetically or numerically.
```
cat /etc/passwd |sort
```

4. **GREP**
- Is used to search for specific results with a determined pattern.
```
cat /etc/passwd |grep "/bin/bash"
```
- So for example here we are looking for users who have set their default shell to **/bin/bash**.
  ```
  cat /etc/passwd |grep -v "false\|no login"
  ```
- And here "**-v**" is used a flag that means exclude , so the results are going to exclude all users who have set their standard shell to **/bin/false** and or **/usr/bin/nologin**.

5. **CUT**
- Specific results with different characters may be separated as delimiters. Here it is handy to know how to remove specific delimiters and show the words on a line in a specified position. One of the tools that can be used for this is cut. Therefore we use the option "-d" and set the delimiter to the colon character (:) and define with the option "-f" the position in the line we want to output.
```
cat /etc/passwd | grep -v "false\|nologin"

root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```
```
cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1

root
sync
postgres
mrb3n
cry0l1t3
htb-student
```

6. **Tr**
- Is used to replace characters in a file.
```
cat /etc/passwd |tr ":" " "
```

7. **COLUMN**
-Used to arrange file output in tabular form with "**-t**".
8. **SED**
- Used to substitute text in a standard file.
```
cat /etc/passwd |sed 's/bin/HTB/g'
```
- The "**s**" flag at the beginning stands for the substitute command. Then we specify the pattern we want to replace. After the slash **(/)**, we enter the pattern we want to use as a replacement in the third position. Finally, we use the "**g**" flag, which stands for replacing all matches.

9. **Wc**
- Used to count lines or characters . we use "**-l"** to specify counting lines.

* * *
## CHECKING LOGGED IN USERS
```
'who'   or  'w'
```

* * *
## FILE INFORMATION & INODE
- **file** - determines type of file (image, binary)
![LINUX FILE.png](../_resources/LINUX%20FILE.png)
- **stat** - gives very deatiled info about the file:
![linux stat.png](../_resources/linux%20stat.png)
- **Inode** - is a file's 'ID Number'.
- To view a files inode:
```
ls -i notes.txt
```
* * *
## MAKING TEMPORARY FILES
```
mktemp
```
- It is used to create temporary files safely.
- Example: Directory;
```
mktemp -d
```
* * *
