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
