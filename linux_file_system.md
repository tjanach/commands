# file systems
##useful comands

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
___
```sh
unmount path/to/device 
unmount /mountpoint
```
___
