# linux backup

## linux commands that can be used for backup 
+ cp, tar, rsync, dump

## simple script to compute available and used disk space 
```sh
#!/bin/bash
TOTAL=0
USED=0
OUT=""
# machines' ip addresses
MACHINES=( 192.168.0.103 192.168.0.101 )
for m in "${MACHINES[@]}"
  do
    # ~ is used as separator
    OUT="$OUT"~`ssh $m 'df / | tail -n +2'`"
  done

LENGTH=${#MACHINES[@]}
LENGTH=$((LENGTH +1))

for (( i=2; i<=LENGTH; i++ ))
  do
    USED_TEMP=`echo $OUT | cut -d "~" -f $i | cut -d " " -f 3`
    TOTAL_TEMP=`echo $OUT | cut -d "~" -f $i | cut -d " " -f 2`
    USED=$((USED + USED_TEMP))
    TOTAL=$((TOTAL + TOTAL_TEMP))
  done
# convert to GB
USED=$((USED/1024/1024))
TOTAL=$((TOTAL/1024/1024))
echo "Total is" $TOTAL " GB"
echo "Total used is" $USED " GB"
```

## simple script to compute sum of sizes of modified files
```sh
#!/bin/bash
SUM=0
FILES=`find / -mount -type f -mtime -1 | xargs du -k | awk '{print $1}'`

for i in $FILES; do
  SUM=$((SUM = $i))
done
# convert to MB
SUM=$((SUM/1024))
# send email to root

echo "$SUM MB" | mail -s "$HOSTNAME free space" root 
```

## netcat can be used to do a backup on the remote machine
+ it is not ssl-based
+ on the remote server listen to port e.g. 20000 and use tar or dump able to receive incoming files
```sh
nc -l 20000 | tar -cvf -
```
+ on the client site
```sh
tar -cvf - file(s) | nc server_ip 20000 
```
