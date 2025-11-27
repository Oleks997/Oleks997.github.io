---
title: "Команди windows PowerShell"
date: 2025-11-27
description: "A relevant description (Used for SEO and search)"
tags: tag1, tag2, tag3, these are used for search
importance: 5
abstract: "Leave empty if you don't want to feature an abstract. "
---

Встановлення linux в серидовищі Windiws
***
 
 `wsl --list --online  `  показати список доступних дистрибутивів
 
 `wsl --install Ubuntu ` встановлення вибраного дистрибутива

 `wsl `                  Запуск емулятора Linux
 
***
***
Інформація про безпроаодне підключення

***
`netsh wlan show interfaces`

***
SSH

***
`ssh -t ed25519_sk -C "mail@examole.com" ` Створення ключа для пыдключення по SSH

`ssh -i C:\Users\sun\.ssh\id_ed25519_sk msn@192.168.56.234`  Використання ключа, для підключення по SSH

З приводу yubico
Робив наступним чином
1) в windows команду 
ssh-keygen -t ed25519-sk -C "your_email@example.com"
буде створено
id_ed25519_sk.pub
id_ed25519_sk
Із файла id_ed25519_sk.pub, ключ копіюємо на сервер в user/ssh/authorized_keys

2) на тестовому Proxmox, в /etc/ssh/sshd_config добавив
PubkeyAuthentication yes
PasswordAuthentication no
AuthenticationMethods publickey

для підключення через cmd
ssh -i C:\Users\sash/.ssh/id_ed25519_sk msn@192.168.56.234
після цього, вспливає вікно - торкніться на ключ, 
"торкаєш" і заходиш


