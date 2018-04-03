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
