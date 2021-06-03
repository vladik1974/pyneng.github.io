---
title: "Репозиторий курса"
permalink: /docs/pyneng-github/
---

В [репозитории курса](https://github.com/pyneng/pyneng-online-11-jun-aug-2021) выложены задания и примеры, которые будут рассматриваться на курсе.


Перед тем, как читать дальше, прочитайте документы:

* [Основы Git](https://pyneng.github.io/docs/git-basics/)
* [Настройка Git и GitHub](https://pyneng.github.io/docs/git-github-setup/)


### Копирование репозитория с GitHub

Все обновления в заданиях и примерах, которые выполняются по ходу курса, будут выложены в этот репозиторий.
Поэтому будет удобней скопировать локально этот репозиторий и обновлять его, когда были внесены какие-то изменения.

> Обо всех изменениях я буду говорить в Slack

Для копирования репозитория с GitHub, выполните команду git clone:
```
$ git clone https://github.com/pyneng/pyneng-online-11-jun-aug-2021
Cloning into 'pyneng-online-11-jun-aug-2021'...
remote: Counting objects: 500, done.
remote: Compressing objects: 100% (41/41), done.
remote: Total 500 (delta 20), reused 47 (delta 10), pack-reused 443
Receiving objects: 100% (500/500), 1.34 MiB | 732 KiB/s, done.
Resolving deltas: 100% (116/116), done.
```

### Обновление локальной копии репозитория

При необходимости обновить локальную версию репозитория, чтобы синхронизировать её с версией на GitHub, надо выполнить git pull внутри созданного каталога pyneng-online-11-jun-aug-2021.

Если обновлений не было, вывод будет таким:
```
$ cd pyneng-online-11-jun-aug-2021/

$ git pull
Already up-to-date.
```

Если обновления были, вывод будет примерно таким:
```
$ git pull
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/pyneng/pyneng-online-11-jun-aug-2021
   49e9f1b..1eb82ad  main     -> origin/main
Updating 49e9f1b..1eb82ad
Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Обратите внимание на информацию о том, что изменился только файл README.md.

