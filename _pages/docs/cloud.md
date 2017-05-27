---
title: "Cloud 9"
permalink: /docs/cloud/
excerpt: "Cloud 9"
---

## Начало работы

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


