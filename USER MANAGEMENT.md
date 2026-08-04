## TYPES OF USERS
1. **ROOT USERS**
- They are the supersuser(have full control) and can do anything
- Username is ***root***
2. **NORMAL USERS**
- Normal accounts with limited permissions.
3. **SYSTEM USERS**
- Created for services.
- Usualy no login access.
* * *
1. **CREATING USERS**
```
sudo adduser john
```
- Creates directory ***/home/john***.
- Sets password and adds basic configs.
2. **CRITICAL FILES**
```
cat /etc/passwd
```
- Lists all users and their basic information.
![ETC.png](../_resources/ETC.png)
- Field explanations:
![ETCFIELD1.png](../_resources/ETCFIELD1.png)
![ETCFIELD2.png](../_resources/ETCFIELD2.png)
```
cat /etc/shadow
```
- It stores user's hashed passwords and their validity periods.
  ![SHADOW.png](../_resources/SHADOW.png)
- Explanation:
![SHADOWFIELDS.png](../_resources/SHADOWFIELDS.png)


3. **DELETING USERS**
```
sudo userdel john
```
- To delete with home directory
```
sudo userdel -r john
```

4. **SWITCHING USERS**
```
su - john
```
- Using root no password required.
```
sudo su - john
```

5. **LOCK USER ACCOUNT**
```
sudo usermod -l john
```
* * *

6. **SET OR CHANGE PASSWORDS**
```
sudo passwd john
```

7. **FORCE CHANGE PASSWORD ON NEXT LOGIN**
```
sudo passwd -e john
```

8.**VIEWING USER INFORMATION**
- We use **id, who , w**.
- Examples:
```
id john #used to see user john's id

who #who is connected to the system

w  #who is doing what

last #who logged in when 
```

9. **PASSWORD CHANGE (chage)**
- Used to see password state and set rules for changing.
- Eg:
```
sudo chage -l john #shows the state of the user's password

sudo chage -M 90 john #john's password should change every 90 days.

```
* * *
## GROUPS
- A set of users.

1. **CREATE GROUP**
```
sudo groupadd hackers OR sudo addgroup hackers
```

2.  **SHOWING WHAT GROUPS YOU BELONG TO**
```
groups
```
3. **CHECK GROUPS WITH A CERTAIN USER**
```
groups john
```

4. **LIST ALL GROUPS**
```
cat /etc/group
```

5. **ADD USER TO GROUP**
```
sudo usermod -aG hackers john
```

6. **CHECK MEMBERS OF A SPECIFIC GROUP**
```
grep '^groupname:' /etc/group
```

7. **DELETE GROUP**
```
sudo groupdel groupname
```



