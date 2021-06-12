---
title: "Подготовка рабочей среды"
permalink: /docs/course-vm/
---

Для выполнения заданий курса можно использовать несколько вариантов:

* взять подготовленную виртуалку vmware или vagrant (virtualbox)
* подготовить виртуалку самостоятельно
* работать без создания виртуальной машины

Любой вариант подходит и с каждым возможны нюансы.

## Выбор ОС

Для курса подходит любая ОС: Linux, Mac OS, Windows.
На каждой ОС возможны свои нюансы с установкой Python и модулей, но как правило, ничего критичного.

> Установка Python на разных [ОС](https://realpython.com/installing-python/)

## Подготовка виртуальной машины/хоста самостоятельно

* [Инструкция для подготовки Linux](/docs/pynenglinux/)
* [Инструкция для подготовки Windows](/docs/pynengwindows/)

Список модулей, которые нужно установить:

```
pip install pytest pytest-clarity==0.3.0a0 pyyaml tabulate jinja2 textfsm pexpect netmiko graphviz
```

Также надо установить graphviz принятым способом в ОС (пример для debian):

```
apt-get install graphviz
```

## Подготовленные виртуальные машины

Для курса подготовлены виртуальные машины, в которых установлены:

* Debian 9.9 ([статьи по основам Linux](https://pyneng.github.io/docs/linux/))
* Python 3.7 и 3.8 в виртуальном окружении
* IPython и другие модули, которые потребуются для выполнения заданий
* текстовые редакторы vim, Geany, Mu
* GNS3 для работы с сетевым оборудованием

Есть два варианта подготовленных виртуальных машин (по ссылкам инструкции для каждого варианта, в которых есть ссылки на образ):

* [Vagrant](https://docs.google.com/document/d/1tIb8prINPM7uhyFxIhSSIF1-jckN_OWkKaO8zHQus9g/edit?usp=sharing)
* [vmware](https://drive.google.com/open?id=1r7Si9xTphdWp79sKxDhVk2zjWGggfy5Z6h8cKCLP5Cs)

