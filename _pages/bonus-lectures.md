---
title: "Бонусные лекции"
permalink: /bonus-lectures/
---

Тут собраны ссылки на бонусные лекции, которые проводились за все время
существования курса. Плюс, если есть предстоящие лекции, расписание и
календарь этих лекций.
Выложены только ссылки в свободном доступе, ссылки на запись лекций на Google Drive
даю в slack.

Список бонусных лекций:

* Работа с базами данных в Python
* Новые возможности в Python 3.x
* Руководство стилю кода PEP8
* Аннотация типов
* Ansible
* black
* click
* logging
* pdb
* pytest
* Python package
* Генераторы
* Декораторы
* ООП: classmethod, staticmethod, property, namedtuple
* Vim, tmux
* Rich
* Scrapli

## Расписание предстоящих бонусных лекций

| Дата       |     Время       | Тема |
|:----------:|:---------------:|------|
| 12.02.2022 | 13:00-15:00 UTC | [Аннотация типов: Generics, Protocols, TypeVar](https://github.com/pyneng/all-pyneng-slides/blob/main/bonus/adv_type_annotations.md) |
| 19.02.2022 | 13:00-15:00 UTC | Функции |
| 27.03.2022 | 7:00-9:00 UTC   | Pydantic |

## ToDo

* [Аннотация типов: Generics, Protocols, TypeVar](https://github.com/pyneng/all-pyneng-slides/blob/main/bonus/adv_type_annotations.md)
* Функции
* [pydantic](https://github.com/samuelcolvin/pydantic)
* [What's new in Python 3.11](https://docs.python.org/3.11/whatsnew/3.11.html)
* [TTP](https://github.com/dmulyalin/ttp)

## Календарь лекций

Календарь в формате [ical](https://calendar.google.com/calendar/ical/tbrecv5n6236rajk4t5bogtlo0%40group.calendar.google.com/public/basic.ics)

<iframe src="https://calendar.google.com/calendar/embed?src=tbrecv5n6236rajk4t5bogtlo0%40group.calendar.google.com&ctz=UTC" style="border: 0" width="800" height="600" frameborder="0" scrolling="no"></iframe>


## Бонусные лекции в записи

## Новые возможности в Python 3.x

В этом каталоге находятся лекции с информацией об обновлениях в Python 3.7,
Python 3.8, [Python 3.9](https://github.com/pyneng/pyneng-bonus-lectures/tree/master/examples/08_python39).

* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRlmf6BeA-7Bx-1NvmqnSIOD)
* [Примеры кода, слайды по лекции Python 3.9](https://github.com/pyneng/pyneng-bonus-lectures/tree/master/examples/08_python39)

## Работа с базами данных в Python

Лекция, которая соответствует [25 разделу в книге](https://pyneng.readthedocs.io/ru/latest/book/25_db/index.html).
Задания по этой лекции находятся в каталоге exercises/25_db в ваших репозиториях. Это
единственные задания из бонусных лекций, которые я проверяю. Их можно сдавать на
проверку так же как и основные задания курса. 


## Руководство стилю кода PEP8

Лекция в которой рассматривается PEP 8 - руководство по стилю в Python.
Рекомендуется к просмотру всем. Хотя при желании можно ограничиться прочтением
самого PEP 8, мне нравится как он оформлен на [этом сайте](https://pep8.org/).

* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

## Аннотация типов

Аннотация типов - это дополнительное описание в классах, функциях, переменных,
которое указывает какой тип данных должен быть в этом месте.

* [задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/01_type_annotations)
* [раздел в книге Advanced Python для сетевых инженеров](https://advpyneng.readthedocs.io/ru/latest/book/01_type_annotations/index.html)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/01_type_annotations)
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRlrzKmbAwxyitvmXjCN4BM9)


## Ansible

Серия лекций по основам Ansible для сетевых инженеров. Рассматриваются основы
Ansible и базовое использование Ansible для работы с сетевым оборудованием.
Этого достаточно чтобы начать работать с Ansible и делать базовые вещи, но чтобы
полноценно работать с Ansible, надо изучать его дальше, в принципе, по любой
книге/курсу по Ansible или [по документации](https://docs.ansible.com/ansible/latest/index.html).
Рассматривается версия Ansible 2.9.

* [документация](https://docs.ansible.com/ansible/latest/index.html)
* Этот же материал почти полностью продублирован в книге [Ansible для сетевых инженеров](https://ansible-for-network-engineers.readthedocs.io/ru/latest/).
* [Задания по Ansible](https://github.com/natenka/ansible-example-exercises)
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRnuI_K5-GV4FdAO9dVkRIGF)

## Python полезно знать

Это набор лекций по разным темам, которые полезно знать всем, хотя бы на уровне
того, что такие возможности есть в Python.

### black

[black](https://github.com/psf/black) - автоматически форматирует код в одном и том же стиле. Не единственный
софт такого рода в Python, другой пример - [yapf](https://github.com/google/yapf). Использовать не обязательно,
но полезно знать, что такого рода модули существуют. Также, если black не нравится,
можно посмотреть в сторону модулей типа [flake8](https://flake8.pycqa.org/en/latest/index.html#) (часто используют и black и flake8).

* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

### click

[click](https://click.palletsprojects.com/en) - модуль для создания интерфейса командной строки. Несмотря на то, что
в стандартной библиотеке Python есть модуль argparse, который делает то же самое,
модуль click использует немного другой подход и, возможно, понравится больше.

* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/03_click)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/03_click)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/03_click/index.html)
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRkrS43bjaC8hxwQjcCZhNiM)

### logging

[logging](https://docs.python.org/3/library/logging.html) - модуль, который позволяет настраивать логирование для скрипта
с огромным количеством возможностей.

* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/03_click)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/03_click)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/05_logging/index.html)
* [запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

### pdb

* [pdb](https://docs.python.org/3/library/pdb.html) - встроенный дебагер в Python
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

### pytest

* [pytest](https://docs.pytest.org/en/stable/) - фреймворк для написания тестов (тесты для заданий написаны на Pytest)
* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/04_pytest_basics)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/04_pytest_basics)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/04_pytest_basics/index.html)


### Python package

Python package - организация нескольких файлов Python в один модуль

## Python продвинутые темы

Тут собраны темы, которые немного сложнее.

### Генераторы

Генераторы - очень рекомендую всем, без исключения, послушать про генераторы.

* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/14_generators)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/14_generators)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/14_generators/index.html).
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

### Декораторы

Основы декораторов (closure) и декораторы - декораторы довольно непростая тема
и при этом, их редко нужно будет создавать самостоятельно. При этом, они довольно
часто используются в Python. Использовать декораторы очень просто, а вот разобраться
как они работают и как их создавать - нет. Лекция как раз для того чтобы
разобраться как именно работают декораторы и как создавать.

* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/08_decorators)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/08_decorators)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/Part_II.html)
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

### ООП: classmethod, staticmethod, property, namedtuple

Если ООП нормально воспринималось на курсе и вы уже начали использовать ООП в своих скриптах,
это полезная тема. Иначе, можно пропустить.

* [Задания](https://github.com/natenka/advpyneng-examples-exercises/tree/master/exercises/11_oop_method_decorators)
* [примеры](https://github.com/natenka/advpyneng-examples-exercises/tree/master/examples/11_oop_method_decorators)
* [описание в книге](https://advpyneng.readthedocs.io/ru/latest/book/11_oop_method_decorators/index.html)
* [Запись лекции (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRmiZjBaTcECszqlRM8LlahR)

## Vim, tmux

Не имеют отношения к Python напрямую, но очень рекомендую разобраться с tmux всем, кто работает на Linux/Unix.

* [Запись лекции tmux (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRkSAPJyzlk_wU7iVLzGFMAi)
* [Запись лекции vim (youtube)](https://youtube.com/playlist?list=PLah0HUih_ZRkiQXDuElo_JW9OfmbEXRpj)

