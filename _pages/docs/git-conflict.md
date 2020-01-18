---
title: "Как разобраться с конфликтом в git"
permalink: /docs/git-conflict/
excerpt: "Как разобраться с конфликтом в git"
---

### Создаем конфликт

Меняю файл README.md локально и на гитхаб

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)

         modified:   README.md
```

добавляю локально в stage area:
```
$ git add .
```

и делаю commit
```
$ git commit -m "update"
[master 9c2c81b] update
1 file changed, 2 insertions(+)
```

при попытке сделать Push получаю сообщение
```
$ git push origin master
To git@github.com:pyneng/online-6-natasha-samoylenko.git
! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:pyneng/online-6-natasha-samoylenko.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

### Разбираемся с конфликтом

Делаем сначала pull
```
$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
Unpacking objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
From github.com:pyneng/online-6-natasha-samoylenko
6d864e7..eec8b0b  master     -> origin/master
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

В файле указано, что было локально и что на гитхабе. Надо решить, что надо оставить в файле и удалить строки <<<, >>> и ===

Содержимое файла:
```
#online-6-natasha-samoylenko

<<<<<<< HEAD
Test1
=======
Test conflict
>>>>>>> eec8b0b8c9132b23cd7a4d0e9aca40afdc82f0cc
```

После правок файл выглядит так
```
# online-6-natasha-samoylenko

Test1
Test conflict
```

Делаем add и после этого делаем commit и push
```
$ git add README.md
$ git commit -m "update after conflict"

$ git push origin master
Counting objects: 6, done.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 631 bytes | 0 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To git@github.com:pyneng/online-6-natasha-samoylenko.git
eec8b0b..dfcf490  master -> master
```
