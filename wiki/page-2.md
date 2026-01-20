---
title: "Команди Linux"
date: 2025-11-27
description: "A relevant description (Used for SEO and search)"
tags: tag1, tag2, tag3, these are used for search
importance: 5
abstract: "Leave empty if you don't want to feature an abstract. "
---

 linux

***
***
`alias ll='ls -lFa --color' `   створення власного скорочення команди

`find /mnt/monitor/ -mtime +120 -exec rm {} \;`  знайти та видалити старі файли

`find . -type f -size -1k` пошук файлів, розміром < 1k
-type f — тільки файли

-size -1k — розмір менше 1 Кібібайта (1024 байт)
(- — менше, + — більше, без знака — рівно)

`du -sh`  розмір поточного каталога 

***

`du -sh ./*`   Розмір лише каталогів у поточній директорії

Пояснення:
du — disk usage

-s — підсумок для кожного каталогу

-h — людиночитний формат (KB/MB/GB)

*/ — тільки директорії

***

`ping -c 10 -M do -s 1572 <hostname_or_ip>`  
ping нефрагментовано `-M do` , 

кількість 10 `-c 10`,  
пакетів   розмір 1572  `-s 1572`

***

`root@tacacs:~# for i in {0..15}; do echo "port $i ont-auto-find enable"; done;`  вивід цикла з рядка 

***
`tar -cvf /tmp/home.tar /home`  заархівувати каталог /home

`tar -cvf /tmp/system-backup.tar /home /srv /root /var`   заархівувати каталог /home та /srv /root /var

    -z: для сжатия применяется утилита gzip

    -j: для сжатия применяется утилита bzip2
    
`tar -czvf archive.tar.gz hello.txt image.png index.html`  

`tar -xvf archive.tar.gz` розахівувати

***
`for i in {1..24}; do n=$((300 + i)); echo "vlan $n"; echo "fixed 25-28";echo "untagged 1-24"; echo "exit"; done`

виконання скрипта в циклі
