---
title: "Проверка заданий тестами"
permalink: /docs/pytest/
excerpt: "pytest"
---

Начиная с раздела "Функции" (09_functions) для проверки заданий используются автоматические тесты.
Они помогают проверить все ли соответствует поставленной задаче, а также дают обратный отклик
по тому, что не соответствует задаче.
Как правило, после первого периода адаптации к тестам, становится проще делать задания с тестами.

Помимо перечисленных выше положительных моментов, в тестах также можно посмотреть какой итоговый 
результат нужен: прояснить структуру данных и мелочи, которые могут влиять на результат.

Для запуска тестов используется pytest - фреймворк для написания тестов.

> [Запись лекции по использованию pytest для проверки заданий](https://youtu.be/R8vWoJ13MFM)

## Основы pytest

Для начала надо установить pytest:

```
pip install pytest
```

Хотя на курсе не надо будет писать тесты, чтобы их понимать, стоит посмотреть на пример теста.
Например, есть следующий код с функцией check_ip:

```python
import ipaddress


def check_ip(ip):
    try:
        ipaddress.ip_address(ip)
        return True
    except ValueError as err:
        return False


if __name__ == "__main__":
    result = check_ip('10.1.1.1')
    print('Function result:', result)
```

Функция check_ip проверяет является ли аргумент, который ей передали, IP-адресом.
Пример вызова функции с разными аргументами:

```python
In [1]: import ipaddress
   ...:
   ...:
   ...: def check_ip(ip):
   ...:     try:
   ...:         ipaddress.ip_address(ip)
   ...:         return True
   ...:     except ValueError as err:
   ...:         return False
   ...:

In [2]: check_ip('10.1.1.1')
Out[2]: True

In [3]: check_ip('10.1.')
Out[3]: False

In [4]: check_ip('a.a.a.a')
Out[4]: False

In [5]: check_ip('500.1.1.1')
Out[5]: False
```

Теперь необходимо написать тест для функции check_ip. Тест должен проверять, 
что при передаче корректного адреса, функция возвращает True, а при передаче
неправильного аргумента - False.

Чтобы упростиь задачу, тест можно написать в том же файле.
В pytest, тестом может быть обычная функция, с именем, которое начинается на test_.
Внутри функции надо написать условия, которые проверяются.
В pytest это делается с помощью assert.

### assert

assert ничего не делает, если выражение, которое написано после него истинное и
генерирует исключение, если выражение ложное:

```python
In [6]: assert 5 > 1

In [7]: a = 4

In [8]: assert a in [1,2,3,4]

In [9]: assert a not in [1,2,3,4]
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-9-1956288e2d8e> in <module>
----> 1 assert a not in [1,2,3,4]

AssertionError:

In [10]: assert 5 < 1
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-10-b224d03aab2f> in <module>
----> 1 assert 5 < 1

AssertionError:
```

После assert и выражения можно писать сообщение. Если сообщение есть, оно выводится в исключении:

```python
In [11]: assert a not in [1,2,3,4], "а нет в списке"
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-11-7a8f87272a54> in <module>
----> 1 assert a not in [1,2,3,4], "а нет в списке"

AssertionError: а нет в списке
```

### Пример теста

pytest использует assert, чтобы указать какие условия должны выполняться, чтобы тест считался пройденным.

В pytest тест можно написать как обычную функцию, но имя функции должно начинаться с test_.
Ниже написан тест test_check_ip, который проверяет работу функции check_ip, передав ей два значения: правильный адрес
и неправильный, а также после каждой проверки написано сообщение:

```python
import ipaddress


def check_ip(ip):
    try:
        ipaddress.ip_address(ip)
        return True
    except ValueError as err:
        return False


def test_check_ip():
    assert check_ip('10.1.1.1') == True, 'При правильном IP, функция должна возвращать True'
    assert check_ip('500.1.1.1') == False, 'Если адрес неправильный, функция должна возвращать False'


if __name__ == "__main__":
    result = check_ip('10.1.1.1')
    print('Function result:', result)
```

Код записан в файл check_ip_functions.py. Теперь надо разобраться как вызывать тесты.
Самый простой вариант, написать слово pytest. В этом случае, pytest автоматически обнаружит тесты в текущем каталоге.
Однако, у pytest есть определенные правила, не только по названию функцию, но и по названию файлов с тестами -
имена файлов также должны начинаться на test_.
Если правила соблюдаются, pytest автоматически найдет тесты, если нет - надо указать файл с тестами.

В случае с примером выше, надо будет вызвать такую команду:

```
$ pytest check_ip_functions.py
=================================== test session starts ====================================
platform linux -- Python 3.7.3, pytest-4.6.2, py-1.5.2, pluggy-0.12.0
rootdir: /home/vagrant/repos/general/pyneng.github.io/code_examples/pytest
collected 1 item

check_ip_functions.py .                                                              [100%]

================================= 1 passed in 0.02 seconds =================================
```

По умолчанию, если тесты проходят, каждый тест (функция test_check_ip) отмечается точкой.
Так как в данном случае тест только один - функция test_check_ip, после имени check_ip_functions.py стоит точка, а также ниже написано, что 1 тест прошел.

Теперь, допустим, что функция работает неправильно и всегда возвращает False (напишите return False в самом начале функции). В этом случае, выполнение теста будет выглядеть так:

```
$ pytest check_ip_functions.py
=================================== test session starts ====================================
platform linux -- Python 3.6.3, pytest-4.6.2, py-1.5.2, pluggy-0.12.0
rootdir: /home/vagrant/repos/general/pyneng.github.io/code_examples/pytest
collected 1 item

check_ip_functions.py F                                                              [100%]

========================================= FAILURES =========================================
______________________________________ test_check_ip _______________________________________

    def test_check_ip():
>       assert check_ip('10.1.1.1') == True, 'При правильном IP, функция должна возвращать True'
E       AssertionError: При правильном IP, функция должна возвращать True
E       assert False == True
E        +  where False = check_ip('10.1.1.1')

check_ip_functions.py:14: AssertionError
================================= 1 failed in 0.06 seconds =================================
```

Если тест не проходит, pytest выводит более подробную информацию и показывает 
в каком месте что-то пошло не так. В данном случае, при выполении строки 
`assert check_ip('10.1.1.1') == True`, выражение не дало истинный результат,
поэтому было сгенерировано исключение.

Ниже, pytest показывает, что именно он сравнивал: `assert False == True` и уточняет,
что False - это `check_ip('10.1.1.1')`.
Посмотрев на вывод, можно заподозрить, что с функцией check_ip что-то не так,
так как она возвращает False на правильном адресе.

Чаще всего, тесты пишется в отдельных файлах. Для данного примера тест всего один,
но он все равно вынесен в отдельный файл.

Файл  test_check_ip_function.py:

```python
from check_ip_functions import check_ip


def test_check_ip():
    assert check_ip('10.1.1.1') == True, 'При правильном IP, функция должна возвращать True'
    assert check_ip('500.1.1.1') == False, 'Если адрес неправильный, функция должна возвращать False'
```

Файл check_ip_functions.py:

```python
import ipaddress


def check_ip(ip):
    #return False
    try:
        ipaddress.ip_address(ip)
        return True
    except ValueError as err:
        return False


if __name__ == "__main__":
    result = check_ip('10.1.1.1')
    print('Function result:', result)
```

В таком случае, тест можно запустить не указывая файл:

```
$ pytest
=================================== test session starts ====================================
platform linux -- Python 3.6.3, pytest-4.6.2, py-1.5.2, pluggy-0.12.0
rootdir: /home/vagrant/repos/general/pyneng.github.io/code_examples/pytest
collected 1 item

test_check_ip_function.py .                                                          [100%]

================================= 1 passed in 0.02 seconds =================================
```

## Особенности использования pytest для проверки заданий

На курсе pytest используется, в первую очередь, для самопроверки заданий.
Однако, эта проверка не является опциональной - задание считается сделанным,
когда оно соблюдает все указанные пункты и проходит тесты.
Со своей стороны, я тоже сначала проверяю задания автоматическими тестами,
а затем уже смотрю код, пишу комментарии, если нужно и показываю вариант решения.

Поначалу тесты требуют усилий, но через пару разделов, они будут помогать в решении заданий.

> Очень важный момент: тесты, которые написаны для заданий курса, не являются 
> эталоном или best practice написания тестов. Тесты написаны с максимальным
> упором на понятность и многие вещи принято делать по-другому.

При решении заданий, особенно, когда есть сомнения по поводу итогового формата данных,
которые должны быть получены, лучше посмтреть в тест.
Например, если задание task_9_1.py, то соответствующий тест будет в файле 
tests/test_task_9_1.py.

Пример теста tests/test_task_9_1.py:

```python
import pytest
import task_9_1
import sys
sys.path.append('..')

from common_functions import check_function_exists, check_function_params


# Проверяет создана ли функция generate_access_config в задании task_9_1
def test_function_created():
    check_function_exists(task_9_1, 'generate_access_config')

# Проверяет параметры функции
def test_function_params():
    check_function_params(function=task_9_1.generate_access_config,
                          param_count=2, param_names=['intf_vlan_mapping', 'access_template'])


def test_function_return_value():
    access_vlans_mapping = {
        'FastEthernet0/12': 10,
        'FastEthernet0/14': 11,
        'FastEthernet0/16': 17
    }
    template_access_mode = [
        'switchport mode access', 'switchport access vlan',
        'switchport nonegotiate', 'spanning-tree portfast',
        'spanning-tree bpduguard enable'
    ]
    correct_return_value = ['interface FastEthernet0/12',
                            'switchport mode access',
                            'switchport access vlan 10',
                            'switchport nonegotiate',
                            'spanning-tree portfast',
                            'spanning-tree bpduguard enable',
                            'interface FastEthernet0/14',
                            'switchport mode access',
                            'switchport access vlan 11',
                            'switchport nonegotiate',
                            'spanning-tree portfast',
                            'spanning-tree bpduguard enable',
                            'interface FastEthernet0/16',
                            'switchport mode access',
                            'switchport access vlan 17',
                            'switchport nonegotiate',
                            'spanning-tree portfast',
                            'spanning-tree bpduguard enable']

    return_value = task_9_1.generate_access_config(access_vlans_mapping, template_access_mode)
    assert return_value != None, "Функция ничего не возвращает"
    assert type(return_value) == list, "Функция должна возвращать список"
    assert return_value == correct_return_value, "Функция возвращает неправильное значение"
```

Обратите внимание на переменную correct_return_value - в этой переменной содержится итоговый 
список, который должна возвращать функция generate_access_config.
Поэтому, если, к примеру, по мере выполнения задания, возник вопрос надо ли добавлять пробелы
перед командами или перевод строки в конце, можно посмотреть в тесте, что именно требуется в 
результате. А также сверить свой вывод, с выводом в переменной correct_return_value.


### Как запускать тесты для проверки заданий

Самое главное, это откуда надо запускать тесты: все тесты надо запускать из
каталога с заданиями раздела, а не из каталога tests.
Например, в разделе 09_functions, такая структура каталога с заданиями:

```
[~/repos/pyneng-7/pyneng-online-may-aug-2019/exercises/09_functions]
vagrant: [master|✔]
$ tree
.

├── config_r1.txt
├── config_sw1.txt
├── config_sw2.txt
├── conftest.py
├── task_9_1a.py
├── task_9_1.py
├── task_9_2a.py
├── task_9_2.py
├── task_9_3a.py
├── task_9_3.py
├── task_9_4.py
└── tests
    ├── test_task_9_1a.py
    ├── test_task_9_1.py
    ├── test_task_9_2a.py
    ├── test_task_9_2.py
    ├── test_task_9_3a.py
    ├── test_task_9_3.py
    └── test_task_9_4.py
```

Запускать тесты, в этом случае, надо из каталога 09_functions:

```
[~/repos/pyneng-7/pyneng-online-may-aug-2019/exercises/09_functions]
vagrant: [master|✔]
$ pytest tests/test_task_9_1.py
=================================== test session starts ====================================
platform linux -- Python 3.7.3, pytest-4.6.2, py-1.5.2, pluggy-0.12.0
rootdir: /home/vagrant/repos/pyneng-7/pyneng-online-may-aug-2019/exercises/09_functions
collected 3 items

tests/test_task_9_1.py ...                                                           [100%]
...
```

> При запуске тестов из каталога tests, возникнут ошибки и тесты не будут выполняться.

### conftest.py

Кроме каталога test, к тестами относится и файл conftest.py - это специальный файл,
в котором можно писать функции (а точнее фикстуры) общие для раных тестов.
Например, в этот файл вынесены функции, которые подключаются по SSH/Telnet к оборудованию.

### Полезные команды

Запуск одного теста:

```
$ pytest tests/test_task_9_1.py
```

Запуск одного теста с более подробным выводом информации (показывает diff между данными в тесте и тем, что получено из функции):

```
$ pytest tests/test_task_9_1.py -vv
```

Запуск всех тестов одного раздела:

```
[~/repos/pyneng-7/pyneng-online-may-aug-2019/exercises/09_functions]
vagrant: [master|✔]
$ pytest
=========================================== test session starts ============================================
platform linux -- Python 3.6.3, pytest-4.6.2, py-1.5.2, pluggy-0.12.0
rootdir: /home/vagrant/repos/pyneng-7/pyneng-online-may-aug-2019/exercises/09_functions
collected 21 items

tests/test_task_9_1.py ..F                                                                           [ 14%]
tests/test_task_9_1a.py FFF                                                                          [ 28%]
tests/test_task_9_2.py FFF                                                                           [ 42%]
tests/test_task_9_2a.py FFF                                                                          [ 57%]
tests/test_task_9_3.py FFF                                                                           [ 71%]
tests/test_task_9_3a.py FFF                                                                          [ 85%]
tests/test_task_9_4.py FFF                                                                           [100%]

...
```

Запуск всех тестов одного раздела с отображением сообщений об ошибках в одну строку:

```
$ pytest --tb=line
```
