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
___
## mdadm - creation and management of RAID - disk array
+ fdisk -l to see if the new disk is attached (/dev/sdb..c..d)
+ fdisk /dev/sdx - create 1 primary partitions on each disk
+ create md0 - RAID
```sh
mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1
```
+ create fs on the md0 
```sh
mkfs -t ext4 /dev/md0
```
+ mount the md0 
```sh
mount /dev/md0 /mnt
```
+ current RAID configuration can be fount in /proc/mdstat file
+ to activate the RAID on startup - fill /etc/mdadm/mdadm.conf
```sh
mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```
+ to start RAID
```sh
mdadm -As /dev/md0
```
+ to stop RAID
```sh
mdadm -S /dev/md0
```
+ to mark faulty disk in RAID
```sh
mdadm /dev/md0 -f /dev/sdb1
```
+ to remove faulty disk in RAID
```sh
mdadm /dev/md0 -r /dev/sdb1
```
+ to add a new disk into RAID
```sh
mdadm /dev/md0 -a /dev/sdb1
```
___
## LVM
+ creation of physical volume
```sh
pvcreate /dev/sdb1
```
+ display all physical volumes
```sh
pvdisplay
pvs - more concise output
```
+ volume group creation
```sh
vgcreate vgName /dev/sdb1 /dev/sdc1 /dev/sdd1 
```
+ display all volume groups
```sh
vgdisplay
vgs - more concise output
```
+ creation of logical volume
```sh
lvcreate -L 100M -n lvName vgName
```
+ display all logical volumes 
```sh
lvdisplay
lvs - more concise output
```
+ making fs on logical volume
```sh
mkfs -t ext4 /dev/vgName/lvName
```
+ mount logical volume
```sh
mount /dev/vgName/lvName /lv_mount_point
```
+ extension of volume group
```sh
pvcreate /dev/sde1 - added partition
vgextend vgName /dev/sde1
```
### logical volume snapshot creation
+ unmount the logical volume
```sh
umount /lv_mount_point
```
+ create snapshot
```sh
lvcreate -L 100M -s -n lvName-snap vgName/lvName 
```
+ mount the snapshot to original mount point 
```sh
mount /dev/vgName/lvName-snap /lv_mount_point
```
+ snapshot removal 
```sh
umount /dev/vgName/lvName-snap
or 
umount /lv_mount_point
lvremove /dev/vgName/lvName-snap
```
+ snapshot merged with the original logical volume 
```sh
umount /dev/vgName/lvName-snap
or 
umount /lv_mount_point
lvconvert ++merge /dev/vgName/lvName
mount /dev/vgName/lvName /lv_mount_point
```

