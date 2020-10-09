# BDF Doluluk

#!/bin/sh
df -P | grep -vE '^Filesystem|media|mnt|cdrom' | awk '{ print $5 " " $6 }' | while read output;
do
  usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1  )
  partition=$(echo $output | awk '{ print $2 }' )
  if [ $usep -ge 90 ]; then
    echo "$(date) tarihindeki $(hostname) sunucusundaki disk dolulugu \"$partition ($usep%)\"" |
     mail -s "Dikkat: Disk Dolulugu $usep%" serhancatana@gmail.com
  fi
done
