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
finds all commands containing the keyword for which there exist man topics
```sh
man -k <part of command name, e.g. printf> 
``` 
finds and displays all man topics related to the keyword
```sh
man -a <e.g. printf> 
``` 
finds man topics only in command titles
```sh
man -af <e.g. printf> 
``` 
updates man pages
```sh
mandb - in ubuntu
makewhatis - in red hat
```

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
du -h -max-depth=1 *
```
finds files or directories sizes in the current location in human readible format

# echo
```sh
echo > file
```
empty file without deleting it


