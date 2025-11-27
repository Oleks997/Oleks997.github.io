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

`du -sh`  розмір поточного каталога 

***

`du -sh ./*`   Розмір лише каталогів у поточній директорії

Пояснення:
du — disk usage

-s — підсумок для кожного каталогу

-h — людиночитний формат (KB/MB/GB)

*/ — тільки директорії

***

`ping -c 10 -M do -s 1572 <hostname_or_ip>`  ping нефрагментовано `-M do` , кількість 10 `-c 10`,  пакетів   розмір 1572  ` -s 1572`
