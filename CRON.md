- It is a time-based job scheduler used in linux
- It  automatically runs commands and scripts on specific times without human intervention.
* * *
## **CRON JOB**
  - is the individual task scheduled by cron.
 
**NOTE**>> **So basically *CRON* is the service (daemon) that is always running in the background while the *CRON JOB* is  and individual task that only runs at a specific time.**

- Viewing your cronjobs:
```
crontab -l
```

- Editing your cron jobs:
```
crontab -e
```
* * *
## **CRON TAB**
- Is a file that stores scheduled jobs.
- Each user can have their own crontab.
- Crontab syntax:
```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day of month
│ └──────── Hour
└────────── Minute
```

- Example:
```
30 14 * * * echo "Hello"
```
- This means at 2:30pm everyday execute the command.
* * *
## THE 5 FIELDS
**MINUTE**
- Range : **0 - 59**
```
15 * * * *      #every hour at xx:15
```

**HOUR**
- Range:**0 - 23**
```
0 16 * * *     #execute a command at 16:00 every day
```

**DAY OF MONTH**
- Range: **1 - 31**
```
0 12 5 * *     #execute a command at 12:00pm on the 5th of every month
```

**MONTH**
-Range: **1 - 12**
```
0 0 5 3 *    #execute a command at 12:00am on the 5th of March
```

**DAY OF WEEK**
- Range: **0 - 7**
- 0 - Sunday, 1 - Monday......., 6 - Saturday.
- Some systems take 7 as Sunday
* * *
## LISTS
**RUN AT MULTIPLE TIMES**
```
0 3,15 * * *    #Runs at 3:00am and 3:00pm everyday
```
* * *
## RANGES
- Example : 1-5
```
0 9 * * 1-5    #runs at 9:00am from Monday through Friday
```
* * *
## STEPS
- Example : */5 (means every 5 minutes).
```
*/10 * * * *   #runs after every 10 minutes
```

* * *
- Where do cron jobs live:
1. **USER CRON JOBS**
```
/var/spool/cron/

or

/var/spool/cron/crontabs
```

2. **SYSTEM CRONTABS**
```
/etc/crontab
```
- Contains system-wide scheduled tasks.
