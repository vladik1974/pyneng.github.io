---
title: "Python 3.6"
permalink: /docs/python-3-6/
excerpt: "Python 3.6"
---

### Install Python 3.6

Установка Python 3.6
```
sudo apt-get install libsqlite3-dev python3-dev libffi-dev libssl-dev
wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz
tar xvf Python-3.6.0.tgz
cd Python-3.6.0
./configure --enable-optimizations --enable-loadable-sqlite-extensions
make -j8
sudo make altinstall
```

После этого можно [создавать виртуальное окружение](https://pyneng.github.io/docs/venv/)

