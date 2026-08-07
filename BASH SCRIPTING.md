- So as we use linux on a day a to day basis , there are commands that we find we have to execute everytime or often.
- Instead of repeatedly typing in the same command everyday, we can automate them.
- We do this through scripts where we input our usual set of commands and we run them through the script.
- And **Bash** is just the program interpreter used.
- To create a script:
```
nano myscript.sh
```
**NOTE>>** The **.sh** doesnt mean anything its just how scripts are normally named, u can also decide not to use it.
- We also need to make our script executable:
```
sudo chmod +x myscript.sh
```

- Example of a bash script:
```
#!/bin/bash       #shebang used to declare that it is a bash script

ls
pwd
```
- So if we run this script , it would list all files and directories **(ls)** show us our directory path **(pwd)**.
- To run a script we:
```
./myscript.sh
```

- We can also use it to print out information.
```
#!/bin/bash

echo "Current user doess not have permission"
```
* * *
## **VARIABLES**
- So we can use variable in scripting to record inputs and also reduce redundancy.
- Example:
```
#!/bin/bash

myname="Yaah"
myage="19"

echo "My name is $myname"
echo "I am $myage years old"
```
- **$** is used to reference the variable.
```
#!/bin/bash

word="awesome"
echo "Linux is $word"
echo "I am $word"
```
- Also we can use variables to "store commands".
- Example:
```
#!/bin/bash

name="Jay"

now=$(date)

echo "Hello $name"

echo "System time and date is:"

echo $now

echo "Your username is: $USER"

```
- So what happens is that **$()** is a sub-shell where the command is run in the background and the output is stored as the variable.
- So **$USER** is not declared because it is a default variable that is declared in the environment your shell is in.
- To see other default variables:
```
env
```
- Normally all default variables are in all caps.
**NOTE>>** It is proper etiquette when creating your variables to make them lowercase so you can be able to differentiate between default system variables and your variables.

* * *
## **MATH FUNCTIONS**
- So its simply about one command:
```
expr    #evaluate expression
```
- With this command we can perform several operations.
```
expr 100 + 1

expr 55 - 32

expr 100 / 25

```
- **NOTE>>** when it comes to multpilication, we cant just use the asterisk by itself.
- This is because the asterisk in bash is a wild card that means **"everything"**.
- So the solution to that:
```
expr 100 \* 20
```
- Example as variables:
```
#!/bin/bash

num1=19

num2=25

echo $num1 * num2
```
- All this may seem not as practical now but we will use them later.
  
* * *
## **IF STATEMENTS**
- We use these to execute some scripts based on conditions.
- Example:
```
#!/bin/bash

num=200

if [ $num -eq 200 ]
then
    echo "The condition is true"
fi

```
```
#!/bin/bash

num=300

if [ $num -ne 200 ]
then
    echo "The condition is false"
fi

```
- This is not as practical but its just to show how an if statement is made.
- **-eq** means **equal to**.
- **-ne** means **not equal to**.
- We also have:
   - **-gt** means **greater than**
   - **-lt** means **less than**
   - **-le** means **less than or equal**
   - **-ge** means **greater than or equal**

- A basic layout for looking for file with a script.
```
#!/bin/bash

if [ -f ~/file]
then
    echo "The file exists."
else
    echo "The file does not exists"

fi

```

- A more practical use of if statements say we want to find a file and execute something with it.
```
#!/bin/bash

program=usr/bin/htop

if [ -f $program ]
then
    echo "$program is available. let's run it..."
else
    echo "$program is NOT available , installing it..."
    sudo apt update && sudo apt install -y htop
fi
$program

```
- This looks for the program htop and  runs it if it is present , but installs it if not.
- However this is not the best or rather most efficient form of the script:
```
#!/bin/bash

program=htop

if command -v $program
then
    echo "$program is available, lets run it..."
else
    echo "$program is NOT available , installing it..."
    sudo apt update && sudo apt install -y $program
fi
$program
```

- So this is more efficient as **htop**  is not hard-coded anywhere.
- Also we use brackets only for test conditions/commands eg: **-eq and -ge** so we didnt need them here.
- **command -v** is used to check if a command exists and is a little more efficient than looking for the file in our instance.

**NOTE>>** the installation commands ive used are for **UBUNTU & DEBIAN**.

* * *
## **EXIT CODES**
-So the basic exit codes are **0** and **non-zero**.
- **0** is when a script is executed successfully.
- **non-zero** is when an error occurs while executing the script.
- If u want to look at the exit code of some commands or script , after running them , u can the type :
```
echo $?

```
- This variable will already be declared when u run ur command or script.
- A more practical example where we have more control of our exit codes:
```
#!/bin/bash

directory=/etc

if [ -d $directory ]
then 
    echo "The directory $directory  exist"
    exit 0  
else 
    echo "The directory $directory does not exist"
    exit 1
fi 
 echo "You will not see this text in your output"

```
- So the **exit** command allows us to exit/leave the script with the code we want.
- This also means that all lines after the exit commands will not be executed.
- This would be useful if u want to execute something else based on the exit code.
- I advice using manual exit codes as there are some complications that may occur as bash looks at exit code of the most recent command.

 **NOTE>>** ***MORE ON THE COMPLICATIONS OF EXIT CODES CAN BE FOUND ON  VIDEO 6 OF BASH SCRIPTING BY LEARN LINUX TV (YOUTUBE)***

 
* * *
## **WHILE LOOPS**
- So they are used to execute certain commands as long as a certain condition is true.
- A simple example:
```
#!/bin/bash

myvar=1

while [ $myvar -le 10 ]
do
   echo $myvar
   myvar=$(( $myvar +1 ))
   sleep 0.5
done
```
- So this is a basic while loop that will print out 1 - 10.
- The loop will first print out our variable that is **1** then it will check if it is lees than  or equal to 10 according to our test condition.
- If it is , it will then add **1** making it **2** and then print it out , and repeat the process till it reaches **10**.
- It would print out **10** then still check it against our test condition, add **1** but because our new number is greater than than 10 it would exit out of the loop.
- **sleep** command is used to delay  each iteration by 0.5 seconds.
- A more practical example would be:
```
#!/bin/bash

while [ -f ~/testfile ]
do
  echo "As of $(date) testfile exists."
  sleep 5
done

echo "As of $(date) testfile does not exist."
```

- This can be used to monitor a file in a system.
- It checks our home directory if the file exists and updates us with the **date** command too.
- **Sleep** is used to ensure that it updates us every 5 seconds and the moment the file is deleted , it would exit out of the loop and notify us.


* * *
## **FOR LOOPS**
- We use this too go through items in a collectiions , say files in a folder.
- So a basic example of a for loop is :
```
#!/bin/bash

for n in {1..10}
do
  echo $n
  sleep 1
done
```

- So this goes through our list from **1-10** printing each character out.
- A more practical example of this:
```
#!/bin/bash

for file in LINUXNOTES/*.txt
do
  bzip2 $file 
done

```
- So this loop goes through our folder looking for all files that are named with **.txt**`and compresses them using **bzip2**.
- We will pick this up again later.
* * *
## **UPDATE SCRIPTS**
- These are scripts we can use to automatically update our linux servers and distros.
- A basic rough example:
```
#!bin/bash

if [ -d /etc/pacman.d ]
then
    #this is based on Arch distro
    sudo pacman -Syu

fi

if [ -d /etc/apt ]
then
    # this is based on Debian / Ubuntu
    sudo apt update
    sudo apt dist-upgrade

fi
```
- So this script would look for those files and based on the ones found , update and upgrade the systems.
- A semi-practical more efficient way of doing this:
```
#!/bin/bash

release_file=/etc/os-release

if grep -q "arch" $release_file
then
    #this is based on Arch distro
    sudo pacman -Syu
fi

if grep -q "debian" $release_file || grep -q "ubuntu" $release_file
then
    # this is based on Debian / Ubuntu
    sudo apt update
    sudo apt full-upgrade

fi  

```
- So the **/etc/os-release** is a configuration file that stores an operating system's identifcation data.
- So this script basically goes throught the file looking for the distros name and based on the name found , executes the update and upgrade command.

* * *
## **STORING SCRIPTS**
- It is efficient to store and run scripts from one place for security and efficienty purposes.
- In linux , we usually store them in the ***/usr/local/bin*** directory.
- So how we move files into the directory:
```
sudo mv myscript.sh /usr/local/bin/
```
- Check if it is in the direcory :
```
ls -l /usr/local/bin
```

- So a main reason for this was for security purposes and to further ensure that only authorised users in a system are allowed to access the scripts, we can change the owners/permissions of the directories.
- For this instance changing the owner is the best action.
```
sudo chown root:root /usr/local/bin

```
- So with this action , we change the owner i.e user and group of our directory to root.

* * *
## **DATA STREAMS**
- There are 3 main data streams:
   - Standard input
   - Standard output **(1)**
   - Standard errors **(2)**
- So **standard output** and **standard errors** are represented by the codes **1** and **2** respectively.
- So say we run this command:
```
find /etc -type f
```
- If u go through the output of the files you will find that there are some file we could not access due to permission restrictions.
- So we could use this to illustrate some practical use of data streams.
- We could decide to redirect our errors to another file:
```
find /etc -type f 2> /dev/null

```
 - This is a popular way of handling errors.
 - By redirecting errors to the **/dev/null** file we erase them from our system "like a blackhole".
 - But if we want to see our errors:
```
find /etc -type f 2> error.txt
```
- Or we can decide to print only standard output in a file:
```
find /etc/ -type f 1> files.txt
```

- So a good use case of this in a script can be :
```
#!/bin/bash

release_file=/etc/os-release
logfile=/var/log/update.log
errorlog=/var/log/update_errors.log

if grep -q "arch" $release_file
then
    #this is based on Arch distro
    sudo pacman -Syu 1>> $logfile 2>> $errorlog
    if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi

    if [ $? -eq 0 ]
    then
        echo "System upgrade complete"
    fi
fi

if grep -q "debian" $release_file || grep -q "ubuntu" $release_file
then
    # this is based on Debian / Ubuntu
    sudo apt update 1>> $logfile 2>> $errorlog
        if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi
    sudo apt full-upgrade 1>> $logfile 2>> $errorlog
        if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi

    if [ $? -eq 0 ]
    then
        echo "System upgrade complete"
    fi

fi

```

- We have added data streams to our update script to handle the different outputs.
- So we redirect our standard output and errors to their respective log files by appending as we do not want to overwrite previous logs that may already exist.
- ***/var/log*** is the directory where log files are stored.
- On running this script u will not see any output on your terminal its all redirected and if you want to view your progress:
```
tail -f /var/log/update.log


#or


tail -f /var/log/update_errors.log
```
- For standard input , we may need to read a user input , example:
```
#!/bin/bash

echo "Please enter name"
read myname
echo "User's name is $myname"
```

* * *
## **FUNCTIONS**
- So we use these to consolidate our scripts and reduce redundancy.
- Lets use our previous script:

```
  #!/bin/bash

release_file=/etc/os-release
logfile=/var/log/update.log
errorlog=/var/log/update_errors.log

if grep -q "arch" $release_file
then
    #this is based on Arch distro
    sudo pacman -Syu 1>> $logfile 2>> $errorlog
    if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi

    if [ $? -eq 0 ]
    then
        echo "System upgrade complete"
    fi
fi

if grep -q "debian" $release_file || grep -q "ubuntu" $release_file
then
    # this is based on Debian / Ubuntu
    sudo apt update 1>> $logfile 2>> $errorlog
        if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi
    sudo apt full-upgrade 1>> $logfile 2>> $errorlog
        if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi

    if [ $? -eq 0 ]
    then
        echo "System upgrade complete"
    fi

fi
```

- **UPDATED SCRIPT**


```

#!/bin/bash

release_file=/etc/os-release
logfile=/var/log/update.log
errorlog=/var/log/update_errors.log

check_exit_status() {
    if [ $? -ne 0 ]
    then
        echo "An error occurred, please view the $errorlog file."
    fi
}

success() {
    if [ $? -q 0]
    then
        echo "System upgrade complete"
    fi
}


if grep -q "arch" $release_file
then
    #this is based on Arch distro
    sudo pacman -Syu 1>> $logfile 2>> $errorlog
    check_exit_status
    success
    
fi

if grep -q "debian" $release_file || grep -q "ubuntu" $release_file
then
    # this is based on Debian / Ubuntu
    sudo apt update 1>> $logfile 2>> $errorlog
    check_exit_status

    sudo apt full-upgrade -y 1>> $logfile 2>> $errorlog
    check_exit_status
    success    
fi
```
- So our new functions are ***check_exit_status*** and ***success*** which are initialized /declare with a set of parantheses followed by curly braces.
- These functions hosts our if statements that would have been  repeated multiple times in our previous script.
- So instead of repeatedly running the same command all over our script, we just call the function.
- **Advantages of functions are**:
     - Improves efficiency as if you want to edit a command you just edit it in the function that holds it.
	 - Reduces redundancy hence the script becomes cleaner.

* * *
## **CASE STATEMENTS**
```

#!/bin/bash

finished=0

while [ $finished -ne 1 ]
do
  echo "Enter numerical digits only"
  echo "What is your favorite linux distribution"
  echo "1 - Arch"
  echo "2 - CentOS"
  echo "3 - Mint"
  echo "4 - Ubuntu"
  echo "5 - Debian"
  echo "6 - Something else..."
  echo "7 - Exit the script."

  read distro;

#case statement
  case $distro in
      1) echo "Arch is a rolling release.";;
      2) echo "CentOs is popular on servers.";;
      3) echo "Mint is popular on desktops and laptops";;
      4) echo "Ubuntu is popular on both servers and computers";;
      5) echo "Oooh a bit of a hacker are you!";;
      6) echo "THere are many distributions out there.";;
      7) finished=1 ;;
      *) echo "You didn't enter an appropriate choice.";;
       
  esac
done
```

- So this is a basic example of a case statement ignoring the while loop that hosts it.
- We initialize/declare it using the word **case** where we use the variable **distro**.
- So a case statement is used to execute commands based on a chosen item from an array.
- Notice each line in the case statement ends with two semi-colons , without them , the case statement won't work.
- To exit a case statement you type case in reverse - **esac**.
- So we incorporated the case statement in a while loop just to show how different items interact in bash scripting.
- So this script will continue to execute till you choose to exit it yourself.
- We set a variable **finished** to 0 to enable our while loop.

* * *
## **SCHEDULING JOBS**
- So we can schedule our scripts to run at a later time in different ways.
- First method we can use is with ***at*** .
- Check if you have at:
```
which at
```
- if not , install:
```
sudo apt install at
```
- So the scheddling syntax:
```
at <time> -f <script>
```
- Example:
```
at 14:00 -f ./myscript.sh
```

- We can also schedule further in the future i.e
```
at 12:00 090126 -f ./myscript.sh

```
- You can check for the jobs waiting to be executed by:
```
atq
```
- Example of an ouput:
![Screenshot from 2026-08-05 15-23-19.png](../_resources/Screenshot%20from%202026-08-05%2015-23-19.png)
- **3** is the job id/no.
- To delete a job :
```
atrm <id>
```
- Example:
```
atrm 3
```

* * *
## **ARGUMENTS**
- Are values passed to a script when you run it.

**POSITIONAL PARAMETERS**
- Each argument is stored in a numerical variable.
- Example:
**PARAMETER**
```
 $0 - script name
 $1-$9 - postional arguments
 $# - number of arguments
 $@ - all arguments , all kept separate
 ```
- Example in a script:
```#!/bin/bash

echo "Script Name : $0"
echo "First Name  : $1"
echo "Age         : $2"
echo "City        : $3"
```
- To run this :
```
./arg.sh Jeff 20 Nairobi
```
- Expected output:

![ARG.png](../_resources/ARG.png)

## **BACKUP SCRIPT**

- So this is a real use case of a script to back up files.
```
#!/bin/bash

#Checking to see if the user has enteres exactly two arguments.

if [ $# -ne 2 ]
then 
    echo "Usage: backup.sh <source_directory> <target_directory>"
    echo "Try again:"
    exit 1

fi

#Check to see if rsync is installed

if ! command -v rsync > /dev/null  2>&1
then 
    echo "This script requires rsync to be installed"
    echo "Please use your distribution's package manager to install it and try again"
    exit 2
 fi
 
 #Capture the current date and  store it in the format YYYY-MM-DD

current_date=$(date +%F)

#Backing up files

rsync_options="-avb --backup-dir $2/$current_date --delete "

$(which rsync) $rsync_options $1 $2/current >> backup_$current_date.log

```

- So first this script checks two see if two arguments are , entered then if **rsync** is installed .
- So for the main backup part:
   - **-avb**
       - **a** - preserves the files' metadate i.e permissions, timestamp , owner
	   - **v** - show files transferred
	   - **b** - creates a directory for files that are going to be overwritten.
	   - **-h** - Human-readable file sizes
       - **--progress** - Display transfer progress
       - **--dry-run** - Preview changes without making them
	- **--backup-dir**
	   - Tells rsync to store backup files to a different directory than the overwritten files.

- Rsync will then create a sub-directory **current_date** that is also a variable under the target destination for all files that are about to be deleted or overwritten.
   - **--delete** then ensures that **destination** directory is a clone of the **source** directory i.e if a file exists in the destination that is no longer in the source , delete it.
    - **--dry-run** allows this script to run without actually execute it to ilustrate how the script would actually behave.This allows us to polish , edit and countercheck our script.
    - **$(which rsync)** - allows the script to run the actual fully qualified command.
- The files are then backed up into a sub-directory under the destination in the file backup_$current_date.log.
