---
title: "Python 3.6"
permalink: /docs/python-3-6/
excerpt: "Python 3.6"
---

### Install Python 3.6
pip install libsqlite3-dev
wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz
tar xvf Python-3.6.0.tgz
cd Python-3.6.0
./configure --enable-optimizations --enable-loadable-sqlite-extensions
make -j8
sudo make altinstall

pip install virtualenvwrapper
После установки, в .bashrc нужно добавить несколько строк
export WORKON_HOME=~/venv

. /usr/local/bin/virtualenvwrapper.sh

exec bash

mkvirtualenv --python=/usr/local/bin/python3.6 py3_convert
pip install ipython
ipython

