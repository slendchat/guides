Для синхронизации каталогов directory1 и directory2 на одной операционной системе, введите:

`rsync -r directory1/ directory2`

Синхронизация с удаленным каталогом выполняется по аналогии с синхронизацией локальных каталогов. Используйте команду в следующем формате:

`rsync -a ~/directory1 username@remote_host:destination_directory`

Если вы передаете файлы, которые еще не были сжаты, например, текстовые файлы, то включить сжатие можно с помощью опции -z:

`rsync -az source destination`

Для отображения процесса синхронизации можно использовать флаг -P:

`rsync -azP source destination`

В качестве примера можно привести параметр --delete, удаляющий файлы из каталога назначения в том случае, если они удалены из источника:

```plaintext
rsync -a --delete <источник> <приёмник>
```

Ещё одним полезным параметром может стать --exclude, исключающий из передачи файлы или каталоги по заданному шаблону:

```plaintext
rsync -a --exclude=<шаблон_для_исключения> <источник> <приёмник>
```

Например, --exclude='.*' исключит из синхронизации скрытые файлы и папки, которые могут содержать чувствительные данные, что важно для обеспечения информационной безопасности. Также для экономии места на диске и сетевого трафика из передачи можно исключить временные файлы и другие данные, не представляющие ценности. Конечно, параметров --exclude может быть несколько.

Вы также можете ограничить максимальный размер передаваемых файлов с помощью параметра --max-size=РАЗМЕР.

При необходимости можно также ограничить скорость передачи файлов, указав параметр --bwlimit=СКОРОСТЬ. Скорость здесь задаётся в килобайтах в секунду. Ограничение скорости передачи может быть полезно в случае низкой пропускной способности канала связи.

После успешной передачи rsync может удалить исходные файлы. Для этого нужно добавить параметр --remove-source-files.

Другие полезные параметры:

- --include="<шаблон_для_игнорирования_исключения>" — не исключать файлы по шаблону.
- -z, --compress — сжимать поток передачи данных.
- -l, --links — при обнаружении символьной ссылки пересоздать её на приёмной стороне.
- -H, --hard-links — пересоздать жесткие ссылки на стороне получателя в соответствии с тем, что имеется в источнике.
- -r, --recursive — рекурсивно переносить подкаталоги.
- -o, --owner — сохранять владельца.
- -g, --group — сохранять группу.
- -p, --perms — сохранять разрешения.
- -t, --times — сохранять время правки.
- -D, --devices --specials — сохранять файлы устройств и специальные файлы.
- -P, --partial --progress — выводить информацию о ходе передачи и сохранять частично переданные файлы.
- -e, --rsh=КОМАНДА — использовать указанную команду удалённой оболочки (remote shell). По умолчанию используется SSH, что соответствует параметру -e ssh. Также в значении этого параметра можно передавать дополнительную информацию, например порт, расположение ключа авторизации и так далее.
- -h, --human-readable — выводить числа в «человекочитаемом» формате.

Приведённый выше параметр -а эквивалентен набору -rlptgoD.

### Dump
Dump requires ext2, ext3 or ext4 file systems.
Basic dump syntax is as follows.
```
dump parameters destination-target source-target
```

The **destination-target** is where the backup job will be stored. The **source-target** is the file system you're backing up.
A level 0 backup is a full backup job.
at level 3 will grab any new or changed files since the level 2 backup.
running from level 0 to level 9 in days or weeks provide incremental backup.

To back up **/home** to a directory named **/recovery/backups** on a remote server named fileserver09, type the following.
```
rdump 0uf fileserver09:/recovery/backups /home
```

|Option|Description|
|---|---|
|r|Extract the entire archive to the current directory.|
|f|The next object is the backup job location.|
|t|List the names found in the archive.|
|C|Compare the archive with the current directory.|
|x|Extract only the specified files instead of the entire archive.|
|v|Display verbose output.|
