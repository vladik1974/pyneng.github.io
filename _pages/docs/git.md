---
title: "Использование Git"
permalink: /docs/git/
excerpt: "Git"
---

### О Git

Система контроля версий (Version Control System, VCS):

* отслеживает изменения в файлах
* хранит несколько версий одного файла
* позволяет откатить изменения
* знает кто и когда сделал изменения

Git:

* распределенная система контроля версий
* широко используется
* выпущен под лицензией GNU GPL v2


Git хранит изменения как snapshot всего репозитория.
Этот snapshot выполняется после каждого commit.

![git](https://git-scm.com/figures/18333fig0105-tn.png)

Файл в Git может быть в таких состояниях:

* committed - файл сохранен в локальной базе
* modified - файл был изменен, но еще не сохранен в локальной базе
* staged - файл отмечен на добавление в следующий commit


![git areas](https://git-scm.com/book/en/v2/images/areas.png)

Соответственно, есть три основные части проекта Git:

* каталог Git (.git) - тут хранятся метаданные и база данных объектов проект
* рабочий каталог -  копия определённой версии проекта
* область подготовленных файлов (staging area) - информация о том, что должно попасть в следующий commit

### Установка Git

Установка Git
```
$ sudo apt-get install git
```

### Первичная настройка Git

Для начала работы с Git необходимо указать имя и email пользователя, которые будут использоваться в commit:

```
$ git config --global user.name "pyneng"
$ git config --global user.email "github_email@gmail.com"
```

Посмотреть настройки можно таким образом:
```
$ git config --list
```

### Инициализация репозитория

Создадим с нуля репозиторий Git.

Для начала, надо создать каталог, в котором будет находиться репозиторий:
```
[~/tools]
$ mkdir first_repo
```

И перейти в него:
```
[~/tools]
$ cd first_repo
```

Теперь, в новом каталоге необходимо дать команду git init:
```
[~/tools/first_repo]
$ git init
Initialized empty Git repository in /home/vagrant/tools/first_repo/.git/
```

После этой команды, в каталоге создается каталог .git, в котором содержится вся информация, которая необходима для работы Git.

### Отображение статуса репозитория в командной строке

> Это дополнительный функционал, который не требуется для работы с Git, но очень помогает в этом.

При работе с Git, очень удобно, когда вы сразу знаете находитесь вы в обычном каталоге или в репозитории Git.
И, кроме того, было бы хорошо понимать статус текущего репозитория.

Для этого можно установиться [специальную утилиту](https://github.com/magicmonty/bash-git-prompt), которая будет показывать статус репозитория.

Процесс установки достаточно прост.
Надо скопировать репозиторий в домашний каталог пользователя, под которым вы работаете:
```
cd ~
git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1
```

А затем добавить в файл ```~/.bashrc``` такие строки:
```
GIT_PROMPT_ONLY_IN_REPO=1
source ~/.bash-git-prompt/gitprompt.sh
```

Для того чтобы изменения применились, перезапустить bash:
```
exec bash
```

> В моей конфигурации приглашение командной строки разнесено на несколько строк, поэтому у вас оно будет отличаться. Главное, обратите внимание на то, что появляется дополнительная информация, при переходе в репозиторий.


Теперь, если вы находитесь в обычном каталоге, приглашение выглядит так:
```
[~]
vagrant@jessie-i386:
$ 
```

Если же перейти в репозиторий Git:
```
[~]
vagrant@jessie-i386:
$ cd tools/first_repo/

[~/tools/first_repo]
vagrant@jessie-i386: [master L|✔] 
```


### Работа с Git

Прежде чем мы начнем добавлять файлы в репозиторий, посмотрим информацию о текущем состоянии репозитория.

__git status__

Для этого в Git есть команда git status:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|✔] 
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)

```

Git сообщает, что мы находимся в ветке master (эта ветка создается сама и используется по умолчанию) и что ему нечего добавлять в commit.
Кроме этого, git предлагает создать или скопировать файлы и после этого воспользоваться командой git add, чтобы git начал за ними следить.

Создадим первый файл README и добавим в него пару произвольных строк текста:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|✔] 
$ echo "First try" > README

```

После этого приглашение выглядит таким образом:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|…2] 

```

Почему-то в приглашении показано, что есть два файла, за которыми git еще не следит.
Посмотрим в git status откуда взялся второй файл:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|…2] 
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    .README.un~
    README

nothing added to commit but untracked files present (use "git add" to track)

```

Git сообщает, что есть файлы за которыми он не следит, подсказывает какой командой это сделать.

Два файла получились из-за того, что у меня настроены undo файлы для vim.
Это специальные файлы, благодаря которым, можно отменять изменения не только в текущем открытии файла, но и прошлые.

__.gitignore__

.README.un~ - это служебный файл, который не нужно добавлять в репозиторий.

В git есть возможность сказать, что какие-то файлы или каталоги нужно игнорировать.
Для этого, надо указать соответствующие шаблоны в файле .gitignore в текущем каталоге:

Для того чтобы git игнорировал undo файлы vim, можно добавить, например, такую строку в файл .gitignore:
```
*.un~
```

Это значит, что Git должен игнорировать все файлы, которые заканчиваются на ```.un~```.

После этого, git status показывает:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|…2] 
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    .gitignore
    README

nothing added to commit but untracked files present (use "git add" to track)

```

Обратите внимание, что теперь в выводе нет файла .README.un~.
Как только в репозитории добавлен файл .gitignore, файлы, которые указаны в нем, игнорируются.

__git add__

Для того чтобы Git начал следить за файлами, используется команда git add.

Можно указать, что надо следить за конкретным файлом:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|…2] 
$ git add README
```

Или за всеми файлами:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|●1…1] 
$ git add .

[~/tools/first_repo]
vagrant@jessie-i386: [master L|●2] 
$ 

```


Проверим как теперь выглядит вывод git status:
```
[~/tools/first_repo]
vagrant@jessie-i386: [master L|●2] 
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   .gitignore
    new file:   README

```

Теперь файлы находятся в секции "Changes to be committed".

__git commit__



![alt]({{ site.url }}{{ site.baseurl }}/assets/images/checked_task_inline_comment.png)
