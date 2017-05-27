---
title: "Cloud 9"
permalink: /docs/cloud/
excerpt: "Cloud 9"
---

## Начало работы

Перед началом работы с Cloud 9, прочитайте документы:

* [Основы Git](https://pyneng.github.io/docs/git-basics/)
* [Настройка Git и GitHub](https://pyneng.github.io/docs/git-github-setup/)

### Регистрация

Для регистрации на Cloud 9 вам нужно пройти по ссылке в письме с заголовком "Team pyneng has invited you to join their team on Cloud9".

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_invite.png)

### Создание workspace

После прохождения регистрации, ваш профиль будет выглядеть так.

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_user_home.png)

Нажмите знак плюс, для создания своей рабочей области.

В открывшемся окне заполните выделенные поля.

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_create_workspace_marked.png)

* workspace name - может быть любым, но лучше выбрать имя равным имени вашего репозитория на GitHub
* Team - надо выбрать/оставить PyNEng
* Надо выбрать Private вариант
* Choose a template - выбрать Python

После этого надо нажать кнопку создания рабочей области.

После создания, у workspace будет такой вид:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_workspace_first_screen.png)

Для примера, в workspace скопировано упражнение из книги "Learn Python the hard way".
Поэтому, надо удалить его.
Для этого надо нажать правой кнопкой мыши на папке ex50 и выбрать пункт Delete.

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_workspace_delete_default.png)


## Настройка workspace

### Аутентификация на GitHub

Для безопасной работы с GitHub, будет использоваться аутентификацию по ключам SSH.
Каждому акаунту в Cloud 9 соответствует свой ключ, поэтому его не нужно генерировать, а достаточно просто добавить в свой акаунт GitHub.


Скопировать ключ можно в настройках профиля.
Для этого нужно перейти на страницу пользователя, а затем в правом верхнем углу нажать шестеренку.

В открывшихся настройках надо выбрать пункт SSH Keys.

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_ssh_keys.png)

А затем скопировать ключ из нижнего окна, который находится под фразой:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/cloud9_copy_ssh_key.png)

После копирования, надо перейти на GitHub.

В правом верхнем углу, на любой странице GitHub, нажмите на картинку вашего профиля и в выпадающем списке выберите Settings.

В настройках, в левой панели выберите поле "SSH and GPG keys".

Нажмите "New SSH key".
И в поле "Title" напишите название ключа (например, "Cloud 9"), а в поле "Key" вставьте содержимое, которое вы скопировали с Cloud 9.

> Если GitHub запросит пароль - введите пароль своего акаунта GitHub.


### Настройка Git

Для начала, нужно проверить текущие настройки Git.

```
$ git config --list
```

> Git уже установлен.

Главное проверить, что user.name - соответствует вашему пользователю на GitHub, а в user.email прописан email, который вы использовали для регистрации на GitHub.

Если это не так, надо установить их в правильные значения таким образом:
```
$ git config --global user.name "pyneng"
$ git config --global user.email "github_email@gmail.com"
```

Для проверки настроек, надо выполнить команду:
```
$ ssh -T git@github.com
```

Вывод будет таким:
```
Hi natenka! You've successfully authenticated, but GitHub does not provide shell access.
```

Теперь вы готовы работать с Git и GitHub.

### Копирование репозитория с GitHub

Для копирования репозитория с GitHub, выполните команду git clone:

```
natenka:~/workspace $ git clone ssh://git@github.com/pyneng/online-2-natasha-samoylenko.git
Cloning into 'online-2-natasha-samoylenko'...
Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
remote: Counting objects: 279, done.
remote: Compressing objects: 100% (208/208), done.
remote: Total 279 (delta 74), reused 267 (delta 62), pack-reused 0
Receiving objects: 100% (279/279), 122.57 KiB | 0 bytes/s, done.
Resolving deltas: 100% (74/74), done.
```


В этой команде вам нужно сменить имя репозитория "online-2-natasha-samoylenko" на свой репозиторий.

В итоге, в текущем каталоге, в котором вы выполнили команду git clone, появится каталог с именем репозитория.
А слева, в дереве файлов появится каталог с аналогичным именем.


В остальном, принципы работы с Git и GitHub аналогичны тому, что описано в документе [Настройка Git и GitHub](https://pyneng.github.io/docs/git-github-setup/).


### Отображение статуса репозитория в командной строке


В Cloud 9 в приглашении командной строки включено отображение о том, что мы находимся в репозитории и в какой ветке, но не отображается информация об изменениях.

Кроме того, было бы удобней сделать многострочное приглашение, чтобы путь не съедал место в командной строке.


Для этого нужно установить [специальную утилиту](https://github.com/magicmonty/bash-git-prompt), которая будет показывать статус репозитория.

Надо скопировать репозиторий в домашний каталог пользователя, под которым вы работаете:
```
cd ~
git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1
```

А затем добавить в конец файла ```~/.bashrc``` такие строки:
```
GIT_PROMPT_ONLY_IN_REPO=1
GIT_PROMPT_START="\[\033[01;32m\]${C9_USER}\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ "
source ~/.bash-git-prompt/gitprompt.sh
```

Для того чтобы изменения применились, перезапустить bash:
```
exec bash
```

После этого, приглашение выглядит так:
```
natenka:~ $ git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1
Cloning into '.bash-git-prompt'...
remote: Counting objects: 46, done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 46 (delta 16), reused 15 (delta 7), pack-reused 0
Unpacking objects: 100% (46/46), done.

natenka:~ $ vi .bashrc 
natenka:~ $ exec bash

natenka:~ $ cd workspace/online-2-natasha-samoylenko/
natenka:~/workspace/online-2-natasha-samoylenko$  [master|✔] 
05:51 $ 
```

