---
title: "Python 3.6"
permalink: /docs/python-3-6/
excerpt: "Python 3.6"
---

### Install Python 3.6

Установка Python 3.6
```
sudo apt-get install libsqlite3-dev
wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz
tar xvf Python-3.6.0.tgz
cd Python-3.6.0
./configure --enable-optimizations --enable-loadable-sqlite-extensions
make -j8
sudo make altinstall
```

### Виртуальные окружения

virtualenv - это инструмент, который позволяет создавать виртуальные окружения.

Виртуальные окружения:
* позволяют изолировать различные проекты
* зависимости, которых требуют разные проекты, находятся в разных местах
* Например, если в проекте 1 требуется пакет версии 1.0, а в проекте 2 требуется тот же пакет, но версии 3.1 пакеты, которые установлены в виртуальных окружениях, не перебивают глобальные пакеты

В курсе используется virtualenvwrapper: он позволяет немного проще работать с virtualenv.

Установка virtualenvwrapper с помощью pip:
```
pip install virtualenvwrapper
```

После установки, в .bashrc нужно добавить несколько строк
```
export WORKON_HOME=~/venv

. /usr/local/bin/virtualenvwrapper.sh
```

Для того чтобы скрипт virtualenvwrapper.sh выполнился и можно было работать с виртуальными окружениями, надо перезапустить bash. Например, таким образом:
```
exec bash
```

Создание виртуального окружения, в котором используется Python 3.6:
```
mkvirtualenv --python=/usr/local/bin/python3.6 pyneng-py3
```

Установка IPython:
```
pip install ipython
ipython
```
