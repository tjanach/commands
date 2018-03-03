# man
man [number] command
+ 1 - commands and applications
+ 2 - system calls
+ 3 - library calls
+ 4 - drivers
+ 5 - files
e.g. 
```sh
$ man 1 passwd
$ man 5 passwd
```
___
finds all commands containing the keyword for which there exist man topics
```sh
man -k <part of command name, e.g. printf> 
```
___
finds and displays all man topics related to the keyword
```sh
man -a <e.g. printf> 
```
___
finds man topics only in command titles
```sh
man -af <e.g. printf> 
```
___
updates man pages
```sh
mandb - in ubuntu
makewhatis - in red hat
```
___
# whatis
```sh
whatis <command, e.g. git>
```
answears whether provided command is installed or not


# which
```sh
which <command, e.g. git>
```
finds path to command

# history

```sh
history
```
presents commands issued by the user
```sh
export HISTTIMEFORMAT="%d/%m/%y %T "
```
lists commands with timestamp

# disk usage
```sh
du <filenam or directory>
```
finds amount of space taken by the file or directory
```sh
du -h --max-depth=1 *
du -h -d=1 *
```
finds files or directories sizes in the current location in human readible format

# echo
```sh
echo > file
```
empty file without deleting it

# dpkg
+ does not have dependencies
___
```sh
dpkg --install <package>
```
installs package if it does not have dependencies
___

```sh
dpkg --remove <package>
```
removes package if it does not have dependencies
___
```sh
dpkg -l
```
lists all installed packages
___
```sh
dpkg -l | grep vim
```
lists installed packages related to vim
___

# apt (Debian/Ubuntu) 
## apt-get
+ manages dependencies
+ repos are in /etc/apt/sources.list
___
```sh
sudo apt-get update
```
updates the repositories, do it before installation!!!
___
```sh
sudo apt-get upgrade -yes
sudo apt-get dist-upgrade -yes
```
upgrades - installs the up-to-date packages, already installed in the system!!!
yes option, confirms all asks from the program
can be done as a cron job
dist-upgrade - can remove packages, no longer compatible with the system
___
___
```sh
sudo apt-get --download-only
```
only download required packages, that can be installed, updated latter on
the default folder for downloaded packages is: var/cache/apt
```sh
sudo apt-get install or update /var/cache/apt/package
```
installs or updates specific downloaded package
```sh
sudo apt-get autoclean
```
cleans the cache
___

## apt-mirror
+ allows to create local repo for apt-get
+ config file in /etc/apt/mirror-list
+ default download folder is /var/spool/apt-mirror
___
```sh
sudo apt-mirror
```
downloads the entire repo from Internet - long process, requires 50G on disk
___

# shell scripting
## processes
___
```sh
ps -ef | grep 
```
displays the info about all running processes in the system
___
```sh
ls -l /proc | grep 
```
displays the info about all running processes in the system
/proc is a virtual directory

```sh
ls -l /proc/pid/fd | grep 
```
displays info about file descriptors used by the process pid
___
## variables
+ no space between varname and value
___
```sh
myvar=VarValue
echo $myvar
```
sets and displays the variable
___
```sh
myvar2='My variable text'
myvar3="My variable text $myvar2"
echo $myvar
```
value closed by '' - not interpreted
value closed by "" - interpreted references to other variables
___
```sh
echo ${HOME}/mydir
```
put in curly braces to avoid misinterpretation
___
```sh
env
```
displays all environment variables
___
## commands
### cut
```sh
cut -d , -f 1,3 sample.csv
cut -d , -f 1,3 < sample.csv
cat sample.csv | cut -d , -f 1,3 
```
displays fields 1 and 3 from sample csv file, which is delimited by comma -d ,
___

### sort
+ -t delimiter
+ -r reverse order
+ -u unique lines
+ -b ignore leading spaces
+ -n numeric sorting
+ -d dictionary sorting
+ -k{column key start},{column key end}
___
```sh
sort -t , -k1,1 sample.csv
```
sorts lines of the file based on specified keys (fields)
___
### uniq
+ displays each line once, even if lines are duplicated
+ input must be sorted first
+ -u displays only unique lines (that do not have duplicates)
+ -d displays duplicated lines
+ -c count output lines
___
```sh
cat example.csv | sort -t , -k1,1 | uniq -d 
```
displays duplicated lines
___
### wc - word count
+ counts words, lines, characters
+ -l for lines
+ -w for words
+ -c for characters
___
```sh
wc -l -w -c -L example.csv
cat example.csv | wc -l -w -c -L 
```
displays number of lines, words, characters, max line legth
___
### tee
+ print to STDOUT while also being writen to a file
___
```sh
find / -name *.log | tee output.txt 
```
displays the result on screen and to file
___
### head
+ print first lines of the file
___
```sh
head output.txt 
```
displays 10 first lines of the file
```sh
head -5 output.txt 
head --lines=5 output.txt 
```
displays 5 first lines of the file

```sh
head --lines=-3 output.txt 
```
displays all lines except the last 3 lines of the file
___

### tail
+ print last lines of the file
___
```sh
tail output.txt 
```
displays 10 last lines of the file
```sh
tail -5 output.txt 
tail --lines=5 output.txt 
```
displays 5 last lines of the file

```sh
tail --lines=-3 output.txt 
```
displays all lines except the first 3 of the file

```sh
tail --lines=+15 output.txt 
```
displays all last lines starting from 15th line of the file

```sh
tail --lines=+2 output.txt | sort -t , -k1,1 
```
sorting without the geader line

```sh
tail -15 -f --pis=PID output.txt 
```
displays last 15 lines of the file, keep the file open, command is closed when the process PID is finished
___
### grep
+ searches for text in stdin and output the results into stdout
+ regular expressions can be provided
+ -c counts the number of matches
+ -i ignore case when searching
+ -v matches if text is not present
+ -l prints file names containing the matched text
+ -R performs recursive search, in the current directory and in all subdirectories
___
```sh
grep "text to searched" 
```
searches for provided text

```sh
ps -ef | grep -v grep | grep watchdog -c 
```
counts the number of watchdog processes, excluding grep proccess
___
## shell scripting
+ # is a comment
+ ; semicolon is used to separate commands in the same line
+ #!/bin/bash - put at the beggining to make the script selfexecutable
+ selfexecutable scripts require to chmod +x script.sh

```sh
sh script.sh
./script.sh
```
script execution
___
### printf vs echo
```sh
printf "Hello\n"
echo "Hello\n"
```
printf interprets special characters \t \n, etc, echo does not

```sh
echo -e "Hello\n"
```
echo -e interprets the special characters
```sh
echo -n "Enter your name:"
```
echo -n stays in the same line, useful fro providing input from user
___
### read
```sh
read variable_name
```
reads the input from the user and sets the variable
```sh
#!/bin/bash
echo -n "Please provide your name: "
read user_name
echo "Hello " $user_name
```
___
### scripts arguments
+ $0 name of the script file
+ $1, $2, $3 ... - consecutive arguments
+ $# - number of arguments passed to the script
+ $* - all arguments as a one string

```sh
#!/bin/bash
echo "script name: " $0
echo "parameter 1: " $1
echo "parameter 2: " $2
echo "parameter 3: " $3
echo "parameter 4: " $4
echo "parameters #: " $#
echo "parameters *: " $*

if [[ $# -eq 0 ]]; then
        echo "usage: " $0 "user_name"
        exit 1
fi
echo "hello:" $1
exit 0
```
___
### shell functions
+ function funtion_name {code}
+ can be added to .bash_profile and can be used as commands, aliases
+ all variables are global, and can be accessed by functions
+ functions can have local variables, local var_name=var_value
```sh
#!/bin/bash
function usage {
        echo "usage: " $0 "user_name"
}
echo "script name: " $0
echo "parameter 1: " $1
echo "parameter 2: " $2
echo "parameter 3: " $3
echo "parameter 4: " $4
echo "parameters #: " $#
echo "parameters *: " $*

if [[ $# -eq 0 ]]; then
        usage
        exit 1
fi
echo "hello:" $1
exit 0
```
___
### if statement
+ spaces after [ and before ] !!!! 
+ -eq, -ne, -gt, -lt, -gte, -lte for numbers
+ =, != for strings
+ all operators in man test
```sh
#!/bin/bash
if [[ $# -eq 0 ]]; then
        command_A
        exit 1
elif [[ cond ]]
        command_B
else
        command_C
fi
exit 0
```
___
### testing for file attributes
+ provided into test command, which is called in if statement
+ -d direcory - is directory
+ -e file - file exists
+ -f file - file exists and is regular file (not a block device)
+ -r file - file is readable
+ -s file - file is not empty
+ -w file - file is writable
___
### looping
+ for..in
```sh
#!/bin/bash
for i in user1 user2 uesr3; do
    echo $i
done
exit 0
```
___
+ for..in with globing
```sh
#!/bin/bash
for f in *.log; do
    gzip $f
done
exit 0
```
globing files using *, ?,
___
+ classic for loop
```sh
#!/bin/bash
for (( i=0; i<$count; i++ )); do
    echo $i
done
exit 0
```
___
+ while loop
```sh
#!/bin/bash
while [[ condition ]]; do
    code
done
exit 0
```
___
+ while loop with delay
```sh
#!/bin/bash
while true; do
    code
    sleep n seconds
done
exit 0
```
___
+ while loop waiting for Y
```sh
#!/bin/bash
input
while [[ $input != 'Y' ]]; do
    echo -n "Enter Y for continue "
    read input
done
exit 0
```
___
