# file systems
## useful comands

### fdisk
+ to manipulate partitions
___
```sh
fdisk -l 
```
display partitions end exit
___

### df
+ Show information about the file system on which each FILE resides,
or all file systems by default
___
```sh
df -h <file> 
```

___
### mount
+ mounts device to filesystem
+ to mount at start time - put into file /etc/fstab
___
```sh
mount path/to/device /mountpoint
```
```sh
mount -a
```
mounts everything in the /etc/fstab
___
### unmount
+ unmounts device or filesystem
+ -l option - lazy unmount, waits till all processes leave the unmounted filesystem
+ use fuser -vc /mountpoint to see processes using the filesystem 
+ use lsof -p /mountpoint  - to list open files
___
```sh
unmount path/to/device 
unmount /mountpoint
```
___
### man hier
+ shows info about file system hierarchy

___
### ln 
+ creates links to files

```sh
ln <src> <trg> - hard link
ln -s <src> <trg> - symbolic link
ln -l <file> - lists all links related to a file
```
___
### rmdir
+ removes empty dir

### rm -r
+ removes dir recursively
___
### /dev
+ contains all devices
+ b - binary devices
+ c - char devices
+ udevd - demon connecting devices to the system

___

### unix domain sockets
+ internal sockets, used to interprocess communication
+ /proc/PID/fd - to see socket files
+ can be accessed only by processes
+ cannot be created by the users

### named pipes
+ similar to system sockets, used to interprocess communication
+ can be created by users
+ are FIFO
+ mkfifo <pipe1>
+ ls -l - the pipe1 has letter p at the begining
+ on one terminal: script -f pipe1
+ on second terminal: cat pipe1
+ the output from the first terminal will be displayed on second one

### umask
+ is used to control default permissions to newly created files and dirs
+ umask is set per process, so also per terminal
+ umask 0022 means, that the permissions will be 777-022=755 for dirs, and 666-022=644 for files

### acl - access control list
+ to control who has permissions to my files or dirs in more flexible way
+ mount -o acl /dev/sdb /mnt_point - must have the option -o acl
+ setfacl might be overwrite by chmod
```sh
getfacl <file> - displays all users:groups having access the file
setfacl [-R] -m user:username:permissions  <file> - sets permissions to the file
setfacl [-R] -m u:userA:rx  <file> - sets permissions to the file
setfacl [-R] -m g:groupB:rw  <file> - sets permissions to the file
```

