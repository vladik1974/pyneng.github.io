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

Отличия показываются как Left и Right, к сожалению тут нет такого что зеленым выделен правильный вариант,
а красным неправильный, надо смотреть по ситуации. Каждый раз при выводе отличий, перед ними есть строка вида:

```python
assert correct_stdout in out.strip()
```

В этом случае Left это правильный вывод, right вывод задания:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_1.png)


или так:

```python
return_value == correct_return_value
```

В этом случае Right это правильный вывод, Left вывод задания:

![passed](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/ptest_output_2.png)


