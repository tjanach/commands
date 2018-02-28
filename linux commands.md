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
ls -l /proc | grep 
```
displays the info about all running processes in the system
/proc is a virtual directory
___
