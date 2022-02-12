---
title: "Установка последней версии Mu"
permalink: /docs/mu-prepare-new/
excerpt: "mu"
---


## Windows

Лучше НЕ устанавливать Python отдельно, а если он был установлен, удалить (только для использования Mu).

### Установка

[Ставим Mu используя installer](https://github.com/mu-editor/mu/releases/download/1.1.0-beta.7/Signed-Mu-Editor-1.1.0b7.msi), [подробнее о процессе установки](https://codewith.mu/en/howto/1.1/install_windows)

### Определяем виртуальное окружение Mu

Надо открыть Mu и в любой новый файл вставить такой код

```python
import sys
from pprint import pprint


pprint(sys.path)
```

Нажимаем Run. Вывод будет примерно таким:

```
['c:\\users\\nata\\mu_code',
 'C:\\Users\\nata\\AppData\\Local\\Programs\\Mu Editor\\Python\\python38.zip',
 'C:\\Users\\nata\\AppData\\Local\\Programs\\Mu Editor\\Python\\DLLs',
 'C:\\Users\\nata\\AppData\\Local\\Programs\\Mu Editor\\Python\\lib',
 'C:\\Users\\nata\\AppData\\Local\\Programs\\Mu Editor\\Python',
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054',
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054\\lib\\site-packages',
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054\\lib\\site-packages\\win32',
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054\\lib\\site-packages\\win32\\lib',
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054\\lib\\site-packages\\Pythonwin']
>>> 
```

Нам надо узнать правильный путь к виртуальному окружению Mu. Оно будет называться ``mu_venv-38-...``.
В данном случае, такой путь:

```
 'C:\\Users\\nata\\AppData\\Local\\python\\mu\\mu_venv-38-20220212-131054',
```

Теперь, для работы в терминале Cmder с Python, надо сначала переходить в это виртуальное окружение так:

```
C:\Users\nata\AppData\Local\python\mu\mu_venv-38-20220212-131054\Scripts\activate.bat
```

Приглашение изменится на

```
C:\Users\nata\cmder
(mu_venv-38-20220212-131054) λ
```

После этого можно переходить в каталог где находится репозиторий и устанавливать pyneng:

```
C:\Users\nata\cmder
(mu_venv-38-20220212-131054) λ ..\Desktop\pyneng-12\online-12-natasha-samoylenko\

C:\Users\nata\Desktop\pyneng-12\online-12-natasha-samoylenko(main -> origin)
(mu_venv-38-20220212-131054) λ pip install .
```

Установить остальные модули, которые нужны для курса:

```
pip install -U pytest pytest-clarity pyyaml tabulate jinja2 textfsm netmiko
```


### Работа с терминалом

Дальше запускаем код в Cmder всегда из виртуального окружения.

## Mac OS

Так же как на windows устанавливаем инсталятор, запускаем и смотрим пути (у меня нет Mac поэтому не могу показать пример вывода).


## Linux

Устанавливаем mu через pip в Python 3.8.

```
python3.8 -m pip install mu-editor==1.1.0b7
```

Запуск mu

```
mu-editor
```

### Определяем виртуальное окружение Mu

Надо открыть Mu и в любой новый файл вставить такой код

```python
import sys
from pprint import pprint


pprint(sys.path)
```

Нажимаем Run. Вывод будет примерно таким:

```
['/home/vagrant/mu_code',
 '/home/vagrant/mu_code',
 '/home/vagrant/.local/bin',
 '/usr/local/lib/python38.zip',
 '/usr/local/lib/python3.8',
 '/usr/local/lib/python3.8/lib-dynload',
 '/home/vagrant/.local/share/mu/mu_venv-38-20220212-113653/lib/python3.8/site-packages']
>>> 
```

Нам надо узнать правильный путь к виртуальному окружению Mu. Оно будет называться ``mu_venv-38-...``.
В данном случае, такой путь:

```
 '/home/vagrant/.local/share/mu/mu_venv-38-20220212-113653/lib/python3.8/'
```

Теперь, для работы в терминале Cmder с Python, надо сначала переходить в это виртуальное окружение так:

```
source /home/vagrant/.local/share/mu/mu_venv-38-20220212-113653/bin/activate
```

Приглашение изменится на

```
(mu_venv-38-20220212-113653)
$
```

После этого можно переходить в каталог где находится репозиторий и устанавливать pyneng:

```
cd ~/repos/online-12-natasha-samoylenko
pip install .
```

Установить остальные модули, которые нужны для курса:

```
pip install -U pytest pytest-clarity pyyaml tabulate jinja2 textfsm netmiko
```


## Обновление Mu на vm курса

> Обновляться не обязательно, кроме кнопки Tidy - автоформатирования кода в красивый вид, все остальное работает
> так же, а из-за обновление многое надо переделывать.


Если хочется обновить Mu, чтобы стала доступна фича "Tidy" - запуск автоформатирования кода в красивый вид.

Удаляем старый Mu в вирт окружении pyneng-py3-7 (чтобы потом не было путанницы какой Mu запустился):

```
pip uninstall mu-editor
```

Переходим в вирт окружение 3.8

```
workon pyneng-py3-8
```

Ставим новый Mu:

```
pip install mu-editor==1.1.0b7
```

Будет продолжение ...

> Делаем так, чтобы терминал всегда переходил в вирт окружение 3.8. Меняем в файле ~/.bashrc строку workon 

