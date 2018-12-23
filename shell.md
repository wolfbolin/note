# Shell相关的奇技淫巧

## 机械硬盘休眠

该命令可以检测硬盘是否处于活跃状态，若硬盘在60秒内无任务，则控制硬盘进入休眠状态，避免硬盘空转。

```shell
#!/bin/bash
DISKNAME='sda'
counter=0
for i in `seq 0 60`
do
    num=`cat /proc/diskstats | grep -w $DISKNAME | awk '{print $(NF-2)}'`
    counter=`expr $counter + $num`
    sleep 1
done
NOW=`date "+%Y-%m-%d %H:%M:%S"`
echo $NOW
if [ $counter == 0 ]; then
    echo "Silent state, stop device."
    hdparm -y /dev/$DISKNAME
else
    echo "Active state, keep running."
fi
echo "================================"
exit 0
```

