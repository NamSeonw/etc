#! /bin/bash

NAME=`date +%y%m%d_%H-%M`
echo done $NAME
mysqldump --defaults-file=/home/bodyfriend/shell/.my.cnf -u root bodyfriend > /home/bodyfriend/dump/body_backup_$NAME.sql

cnt=0
list1=`ls -pr /home/bodyfriend/dump | grep -v / | grep ".sql"`

for FILENAME in $list1
do
  cnt=$((cnt + 1))
  if [ \( $cnt -gt 14 \) ]; then
    echo "del /home/bodyfriend/dump/$FILENAME"
     `rm -f /home/bodyfriend/dump/$FILENAME`
    continue
  fi
  echo "keep $FILENAME"
done
