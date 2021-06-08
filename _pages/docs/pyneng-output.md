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
Проверка правильности вывода в тесте проверяется с помощью выражения `assert ...`. Два самых распространенных варианта (98% тестов):

```python
assert correct_return_value == return_value
assert correct_output in return_output
```

### assert x == y

В большинстве заданий проверяется равенство двух значений:

```python
assert correct_return_value == return_value
```

В этом случае, тест выводит Left как правильный ответ зеленого цвета, а Right как вывод задания красного цвета:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_2.png)

Другие примеры вывода, с разными отличиями, но тут во всех случаях left (зеленое) это правильный результат,
а rigth (красное) то что было получено при запуске задания:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/pyneng_output_1.png)

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/pyneng_output_3.png)

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/pyneng_output_2.png)

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/pyneng_output_4.png)


### assert x in y

Выражение `assert x in y` проверяет находится ли нужный вывод в полученном результате задания.
Например, в тесте это может выглядеть так:

```python
assert correct_stdout in out.strip()
```

В этом случае Left (зеленый) это правильный вывод, right вывод задания:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_1.png)

