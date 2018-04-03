# cron and at jobs
# cron 
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




