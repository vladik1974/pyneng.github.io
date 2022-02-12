---
title: "Редактор Mu"
permalink: /docs/mu/
excerpt: "mu"
---

[Редактор Mu](https://codewith.mu/) - это редактор для начинающих изучать Python (он поддерживает только Python).

С одной стороны, в нём нет ничего лишнего, что поначалу может сильно отвлекать и путать. В то же время, в нём есть такие важные функции как проверка кода на соблюдение PEP 8 и debugger. Плюс, Mu работает на разных ОС (macOS, Windows, Linux).

Запись лекций по редактору Mu:

* [Основы работы с Mu](https://youtu.be/9qH92jz0p58)
* [Использование debugger в  Mu](https://youtu.be/s9Lskg37xss)

## Установка Mu

[Установка Mu](https://pyneng.github.io/docs/mu-prepare/)

## Открыть Mu

Открыть Mu:

```
mu-editor
```

Открыть какой-то файл в Mu:
```
mu-editor task_4_1.py
```

Или нажать "Load" в графическом интерфейсе.


## Как настроить ОС, чтобы файлы .py открывались Mu (по умолчанию в моих VM - Geany)


![mu cfg](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/open_with_mu_1.png)

![mu cfg](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/open_with_mu_2.png)

## Полезные ссылки

* [Keyboard Shortcuts](https://codewith.mu/en/tutorials/1.0/shortcuts)

## Создание ярлыка

Для создания ярлыка, надо установить модуль shortcut:

```
pip3 install shortcut
```

И выполнить команду
```
shortcut mu-editor
```


## Настройка приложения в Debian

```
cd /usr/share/applications
```

Добавить в файл mu.editor.desktop:
```
[Desktop Entry]
Name=mu-editor
Comment=Simple Python editor
Exec=mu-editor
Icon=/usr/share/pixmaps/mu.png
Terminal=false
Type=Application
MimeType=text/plain
Categories=GTK;Development;TextEditor;
Keywords=Python;text;editor;
InitialPreference=6
```

Добавить иконку
```
cd /usr/share/pixmaps
sudo wget https://codewith.mu/img/brand.png
sudo mv brand.png mu.png
```

[Source](https://madewith.mu/mu/users/2019/04/11/crossing-river-feeling-stones.html).
