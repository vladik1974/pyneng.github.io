---
title: "Вывод pyneng"
permalink: /docs/pyneng-output/
excerpt: "Вывод pyneng"
---

## Warning

В конце вывода теста часто написано "1 warning". Это можно игнорировать, предупреждения в основном связаны с работой
каких-то модулей и скрыты чтобы не отвлекать от заданий.


## Тесты прошли успешно

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_5.png)

## Тесты не прошли

Когда какие-то тесты не прошли, в выводе показываются отличия между тем как должен выглядеть вывод и какой
вывод был получен.

### assert x == y

В большинстве заданий проверяется равенство двух значений:

```python
correct_return_value == return_value
```

В этом случае, тест выводит Left как правильный ответ зеленого цвета, а Right как вывод задания красного цвета:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/pyneng_output_1.png)

### assert x in y

Выражение `assert x in y` проверяет находится ли нужный вывод в полученном результате задания.
Например, в тесте это может выглядеть так:

```python
assert correct_stdout in out.strip()
```

В этом случае Left (зеленый) это правильный вывод, right вывод задания:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_1.png)


### assert ...

Иногда не получается написать тест так, чтобы слева был правильный ответ, а справа неправильный.
Поэтому иногда left будет вывод из задания. 
Каждый раз при выводе отличий, перед ними есть строка вида assert:

```python
assert ...
```

В этом случае Left это вывод задания, right прправильный вывод


