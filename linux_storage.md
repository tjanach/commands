# storage
+ when a disk is connected to the system the linux automatically recognizes it and creates appropriate file in /dev
+ sda, sdb, sdc - first, second, third scasi disk
+ sda1, sdb2, sdc3 - first disc first partition, second disk second partition, third disk third partition

## ls -l /dev/disk/by-id, by-path, by-uuid
+ displays info about attached disks
+ uuid can be used when mounting as some linux changes symbols sda, sdb... at reboot

## fdisk -l or parted -l
+ displays info about attached disks and partitions
___
## adding a disk
+ attach the disk physically and reboot the machine
+ fdisk -l to see if the new disk is attached (/dev/sdb..c..d..e)
+ fdisk /dev/sdb
  + a - add a new partition
  + p - primary type
  + 1-4 - number of partition (1)
  + select sectors or cylinders
  + w - to write the partition
  + fdisk -l - to check if the partition has been created
+ pvcreate /dev/sdb1 - to create physical volume
+ vgcreate vgTest /dev/sdb1 - to create volume group
+ lvcreate -l 100%FREE -n lvTest vgTest - to create logical volume
+ mkfs -t ext4 /dev/vgTest/lvTest - format logical volume
+ mount /dev/vgTest/lvTest /mnt_point
+ add to /etc/fstab : /dev/vgTest/lvTest /mnt_point ext4 defaults 0 0 
+ umount /mnt_point
+ mount -a - mount averything in /etc/fstab - to see if there are no errors and everything were mounted
+ df -h - check if the file system has been added


```sh
finger root 
```
