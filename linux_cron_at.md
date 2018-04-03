# cron and at jobs
## cron 
+ is controlled by crond demon as system boots
+ is uses configuration files located per each user in /var/spool/cron
  + each file is named as the user login name, whoc reated his own cron tab
+ it uses sh shel, can be configured to use other shell bash, ksh
+ the following command is used for edition of crontab of logged user
```sh
crontab -e
```
+ for edition the default editor (env $EDITOR) is used, and at the end the cron definition is checkout 
+ the execution logs are kept in /var/log/cron
+ lines are ignored by #
+ each cron tab entity consists of 6 fields
  + minut (0 - 59)
  + hour (0 - 23)
  + day (1 - 31)
  + month (1 - 12)
  + weekday (0 - 6)
  + command/script
+ 0 0 1 1 * echo "Hello new Year" > dev/console
+ * can be used for any value
+ 1-5; 1,5,6 can be used for range
+ .bash_profile or .profile are NOT EXECUTED before crone job
  + is is better to execute those file in cron tab scripts
  + PATH=/bin:/sbin:/usr/bin:/usr/sbin:/home/<user> - can be added to crontab file
+ the sigh % represents a new line in the command line field\
  + e.g. main -s Hello <user> % Welcome to the team % Enjoy .... %
+ superuser can modify the crontab in the name of a specific user
```sh
crontab -e -u <user>
```
+ list the crontab list
```sh
crontab -l
```
+ remove the user's crontab
```sh
crontab -r
```
+ the permissions to define crontabs are managed by /etc/cron.allow and /etc/cron.deny
  + if the file for a user exits in /var/spool/cron/<user> - it will be executed regardless of the above permission files
+ crontab keywords:
  + @yearly = 0 0 1 1 *
  + @monthly = 0 0 1 * * 
  + @daily = 0 0 * * *
  + @hourly = 0 * * * *
  + @reboot - at system startup
+ by default crond sends emails (with commands' output) to the user who created the crontab
  + can redirected to another user using MAIL="root" in the crontabfile, at the begining
  + MAIL="" to disable sending emails
___
## at
+ used to execute a command or srcipt once at a specified time
  + 1 am December 25
  + now + 10 min
+ when at command is issued, inteactive shell is provided for entering the commands
  + Ctrl+D when finished
+ list all at jobs
```sh
at -l 
atq
```
+ remove at job
```sh
at -d <job number> 
atrm <job number>
```
+ to provide a script as a command
```sh
at -f <script_path> now + 30 min 
```
+ at shortcuts
  + noon, midnightm, teatime, tomorrow, next week, next wednesday, fri, saturday
  + now + 1 week/hour/day/month/year/hour/min
+ the permissions to at are managed by /etc/at.allow and /etc/at.deny
  
## batch is a similar command
+ but can trigger the execution at special condition, e.g. CPU load falls below 1.5
  
  
