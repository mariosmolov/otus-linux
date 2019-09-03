# Инструкции

* [Как начать Git](git_quick_start.md)
* [Как начать Vagrant](vagrant_quick_start.md)

## otus-linux

Используйте этот [Vagrantfile](Vagrantfile) - для тестового стенда.

## Сломать/починить RAID

Сделать это можно искусственно зафейлив одно из блочных устройств

**mdadm /dev/md0 --fail /dev/sde**

Посмотрим как это отразилось на RAID

**cat /proc/mdstat**

> Personalities : [raid6] [raid5] [raid4]
> md0 : active raid6 sdf[4] sde[3](F) sdd[2] sdc[1] sdb[0]
>  761856 blocks super 1.2 level 6, 512k chunk, algorithm 2 [5/4] [UUU_U]

Теперь удалим сломанный диск из массива

**mdadm /dev/md0 --remove /dev/sde**

И подключим заново

**mdadm /dev/md0 --add /dev/sde**

Проверим что всё хорошо

**mdadm -D /dev/md0**
