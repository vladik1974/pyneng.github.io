---
title: "Нюансы выполнения заданий на Windows"
permalink: /docs/taskswindows/
---

Модуль pexpect не работает на Windows и так как он не нужен для выполнения заданий,
это влияет только на то, что не получится повторить примеры из лекции.

Все остальные модули работают, но с некоторыми есть нюансы.

### graphviz

Для выполнения заданий в 11 и 17 разделе будет нужен graphviz.
И нужно будет установить модуль Python:
```
pip install graphviz
```

И приложение [graphviz](https://graphviz.gitlab.io/_pages/Download/Download_windows.html)

После установки надо добавить [graphviz в PATH](https://bobswift.atlassian.net/wiki/spaces/GVIZ/pages/131924165/Graphviz+installation)

### csv

При работе с csv на Windows всегда надо указывать `newline=""` при открытии файла:
```
    with open(output, "w", newline="") as dest:
        writer = csv.writer(dest)
```

### textfsm

Часть модулей, которые использует textfsm, не доступны для Windows.
И в то же время, они не нужны для нашего использования textfsm. 
Чтобы textfsm коректно работал на Windows надо закоментировать
в файле terminal.py в каталоге textfsm некоторые строки.

Как найти каталог textfsm:

Сначала смотрим где находится каталог site-packages:
```
In [2]: import sys

In [3]: sys.path
Out[3]:
 ...
 'c:\\users\\nata\\appdata\\local\\programs\\python\\python37\\lib\\site-packages',
 ...
```

Затем переходим в этот каталог и внутри него ищем каталог textfsm.
В каталоге textfsm открываем файл terminal.py и комментируем строки таким образом:
```
# import fcntl
import getopt
import os
import re
import struct
import sys
# import termios
import time
# import tty
```

После этого код с использованием textfsm должен работать на Windows.

## Работа с сетевым оборудованием

В последней трети курса для выполнения заданий понадобится сетевое оборудование.
Можно использовать реальное или виртуальное сетевое оборудование и любую систему
управления оборудованием: GNS3, UNL или другую.

Где скачать GNS3:

* [GNS3](https://github.com/GNS3/gns3-gui/releases)

Вариант подключение к виртуальным устройствам через Loopback

* правый клик на start и выбрать Device manager
* нажать Action, выбрать Add legacy hardware
* Нажать Next
* выбрать "Install the hardware that i manually select from a list". Нажать Next
* выбрать Network adapters. Нажать Next
* выбрать Microsoft в левом столбце и Microsoft KM-TEST Loopback в правом. Нажать Next
* нажать Next
* нажать Finish
* Обязательно перезагрузить машину после этого

Потом в GNS3 выбрать этот loopback интерфейс для подключения "облака".

