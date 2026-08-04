**NOTE** - How to check for a specific files permission
```
ls -l <filename>
```
Eg:
![FILEPERMS1.png](../_resources/FILEPERMS1.png)

## FLAGS
1. **r** - read
2. **w** - write
3. **x** - execute
4. **-** - no permission

**PERMISSION VALUES (Octal)**
1. Read (r) - 4
2. Write (w) - 2
3. Execute (x) - 1

- So:
  - **rwx** - 4 + 2 + 1 = 7
  - **rw** - 4 + 2 = 6
  - **rx** - 4 + 1 = 5
  - **x** - 1
  ![CHMOD 600.png](../_resources/CHMOD%20600.png)
![chmod 777.png](../_resources/chmod%20777.png)
##  SPECIAL PERMISSIONS
1. **SUID** - **4000** allows u to run as the file owner.
2. **SGID** - **2000** files created inside inherit the directory's group.
3. **STICKY BIT** - **1000** only file owner can delete their file.
![SUID.png](../_resources/SUID.png)
![SGID.png](../_resources/SGID.png)
* * *
## FILE ATTRIBUTES (chattr & lsattr)
- Provides stonger protection that permissions by making a file immutable.
- **chattr +i file** - Locks file not even root can delete it.
- **lsattr file** - shows attributes.
**NOTE>>** - use **sudo chattr -i file** to unlock file.

* * *
1. **chmod** - change mode , used to change file permissions.
```
chmod g+w file.txt  #adds write permission to the groups that owns the file
```

2. **chown** - changes owner of file.
```
chown john file.txt # now the owner is john

chown john:admins #changes owner and group
```

3. **chgrp** - changes file group  only.
```
chgrp developers file.txt
```

