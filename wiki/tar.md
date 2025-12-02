---
title: "Tar linux"
date: 2025-12-02
description: "A relevant description (Used for SEO and search)"
tags: tag1, tag2, tag3, these are used for search
importance: 5
abstract: "Leave empty if you don't want to feature an abstract. "
---




Команда tar (сокращение от "tape archive" или "ленточный архив") позволяет объединить несколько файлов в один архив. Она имеет следующую форму:

tar [options] [имя_архива] [файлы или папки для архивации]

Вначале команде передается набор опций. Далее идет имя архива, в который надо поместить файлы/папки, или который, наоборот, надо распаковать.

Последний параметр команды представляет путь к файлам/каталогам, которые нужно заархивировать или разархивировать.

Опции позволяют управлять поведением команды и указывают, что мы хотим сделать. Но так как опций огромное множество, то перечислю наиболее используемые:

    -c, --create: создает архив

    --delete: удаляет содержимое архива

    -d, --diff, --compare: сравнивает архивы

    -r, --append: добавляет файлы в конец архива

    -t, --list: выводит содержимое архива

    -u, --update: обновляет только те файлы, которые новее одноименных файлов в архиве

    -x, --extract, --get: извлекает файлы из архива

    -f, --file=ARCHIVE: в качестве имени файла архива использует ARCHIVE

    -v, --verbose: выводит подробный список обработанных файлов

    --overwrite: перезаписывает файлы при извлечении

    --overwrite-dir: перезаписывает каталоги при извлечении

    --remove-files: удаляет файлы при добавлении их в архив

Допустим, что в домашнем каталоге пользователя лежат следующие файлы:

    hello.txt

    image.png

    index.html

Заархивируем эти файлы в архив под именем "archive.tar":

`eugene@Eugene:~$ tar -cvf archive.tar hello.txt image.png index.html`

`hello.txt`
`image.png`
`index.html`

В данном случае команде tar передаются три опции:
    -c (архивировать файл), 
    -v (выводит побробную сводку операии) 
    -f (устанавливает имя архивного файла)

Здесь предполагается, что мы находимся в домашнем каталоге, и файлы для архивирования лежат в этом каталоге, и файл архива создается в этом каталоге. Однако конкретные пути могут различаться. И в этом случае мы можем передать полные пути к файлам. Например, если файлы у нас лежат в папке "Documents":

tar -cvf ~/archive.tar ~/Documents/hello.txt ~/Documents/image.png ~/Documents/index.html

Получим информацию по созданному архиву:

`eugene@Eugene:~$ tar -tvf archive.tar
-rw-rw-r-- eugene/eugene  1572 2024-03-09 11:39 hello.txt
-rw-rw-r-- eugene/eugene 177489 2024-02-26 09:49 image.png
-rw-rw-r-- eugene/eugene     67 2024-02-23 23:07 index.html
eugene@Eugene:~$ 
`
Распакуем вышесозданный файл архива:

eugene@Eugene:~$ tar -xvf archive.tar
hello.txt
image.png
index.html

Подобным образом мы можем заархивировать весь каталог. Например, заархивируем домашний каталог пользователей в файл "/tmp/home.tar":

tar -cvf /tmp/home.tar /home

Можно даже создать таким образом бэкап для всей сиситемы, заархивировав несколько каталогов:

tar -cvf /tmp/system-backup.tar /home /srv /root /var

Добавление сжатия

Стоит отметить, что создание архива объединяет несколько файлов/каталогов в один пакет, но не сжимает их. Для сжатия файлов команде tar надо передать соответствующие опции:

    -z: для сжатия применяется утилита gzip

    -j: для сжатия применяется утилита bzip2

Например, заархивируем файлы, используя сжатие gzip:

tar -czvf archive.tar.gz hello.txt image.png index.html

В итоге создается архив archive.tar.gz. Распаковать его можно также, как и архив без сжатия:

tar -xvf archive.tar.gz

Стоит отметить, что мы можем вызвать различные компоненты создания и сжатия архивов по отдельности, построив цепочку команд:

tar -cvf test.tar test | bzip2 -9 -c > test.tar.bz2

Здесь все выполнение разбивается на три части. Вначале из папки test создаем архив "test.tar"

tar -cvf test.tar test

Далее этот архив сжимаем с помощью утилиты bzip2, применяя уровень сжатия 9 (маскимальное сжатие) и опцию -c (сжатие)

bzip2 -9 -c

Далее перенаправляем результат утилиты bzip2 в файл test.tar.bz2 и таким образом мы получаем сжатый архив.
Управлением именами

При создании архива следует учитывать, что все файлы/каталоги сохраняются в нем по полным путям. Например, пусть в папке "Documents" есть каталог "test", который мы хотим заархивировать:

eugene@Eugene:~$ tar -cvf archive.tar ~/Documents/test
tar: Removing leading `/' from member names
/home/eugene/Documents/test/
/home/eugene/Documents/test/image.png
/home/eugene/Documents/test/index.html
/home/eugene/Documents/test/hello.txt
/home/eugene/Documents/test/output.txt
eugene@Eugene:~$ 

Здест мы видим, что каждый файл из папки "tests" сохраняется в архиве по пути "home/eugene/Documents/test" (который соответствует его реальному пути в файловой системе). Однако теперь распакуем архив:

eugene@Eugene:~$ tar -xvf archive.tar
home/eugene/Documents/test/
home/eugene/Documents/test/image.png
home/eugene/Documents/test/index.html
home/eugene/Documents/test/hello.txt
home/eugene/Documents/test/output.txt
eugene@Eugene:~$ 

В итоге в текущем катаооге будет создана папка home/eugene/Documents/test/, в которой будут находиться файлы папки "test".

Подобное поведение по умолчанию может быть не самым желательным. Возможно, мы хотим распаковать архив не в "home/eugene/Documents/test/", в папку "test" или вовсе в текущую папку. В этом случае у нас есть два варианта:

    Сразу переходить в терминале в папку, содержимое которой надо архивировать, и из этой папки производить архивацию. Таким образом, мы избежим добавления полных путей к файлам

    Использовать при архивации опцию -C, которая позволит включить к архив только относительные имена файлов и каталогов

Например, используем второй вариант:

eugene@Eugene:~$ tar -cvf archive.tar -C ~/Documents/test .
./
./image.png
./index.html
./hello.txt
./output.txt
eugene@Eugene:~$ 

После опции -C указывается путь к файлам внутри архива. Точка . указывает, что содержимое папки "test" будет помещаться в архив без каки-либо путей. При распаковке все файлы архива распакуются в текущую папку:

eugene@Eugene:~$ tar -xvf archive.tar
./
./image.png
./index.html
./hello.txt
./output.txt
eugene@Eugene:~$ 

Другой пример - запакуем все содержимое папки ~/Documents/test по пути "test":

eugene@Eugene:~$ tar -cvf archive.tar -C ~/Documents test
test/
test/image.png
test/index.html
test/hello.txt
test/output.txt
eugene@Eugene:~$ 

При распаковке все файлы архива распакуются в папку "test" в текущей папке:

eugene@Eugene:~$ tar -xvf archive.tar
test/
test/image.png
test/index.html
test/hello.txt
test/output.txt
eugene@Eugene:~$ 

При распаковке с помощью опции -C мы также можем настроить путь, по которому архив будет распаковываться

eugene@Eugene:~$ mkdir test_new
eugene@Eugene:~$ tar -xvf archive.tar -C test_new
./
./image.png
./index.html
./hello.txt
./output.txt
eugene@Eugene:~$ 

В данном случае сначала создаем папку "test_new", а затем распаковываем в нее архив
Инкрементальный бекап

Опция -g позволяет создать инкрементальный бэкап. Например, забекапим папку "test"

mkdir backup
tar -czvg backup/snapshot-file -f backup/backup-initial.tar.gz  test

В данном случае бэкапы помещаются в папку "backup", которую предварительно создаем. Вторая команда создаст файл "snapshot-file", который содержит список всех файлов, входящих в бекап. А файл "backup-initial.tar.gz" собственно будет представлять бекап.

После создания начального бэкапа через некоторое время мы произвели некоторые изменение в папке test, например, изменили уже существующие файлы или добавили новые и решили создать следующий бэкап:

tar -czvg backup/snapshot-file -f backup/backup-11032024.tar.gz  test

Со временем мы нечаянно удалили папку test и решили ее восстановить. В этом случае нам последовательно надо выполнить разархивацию бэкапов, начиная с самых старых:

tar -xzvf backup/backup-initial.tar.gz
tar -xzvf backup/backup-11032024.tar.gz 

