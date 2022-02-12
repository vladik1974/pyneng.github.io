---
title: "Подготовка к работе с Mu"
permalink: /docs/mu-prepare/
excerpt: "mu"
---

[Редактор Mu](https://codewith.mu/) - это редактор для начинающих изучать Python (он поддерживает только Python).


# Простой вариант для любой ОС

## vm курса (vagrant/vmware)

Все уже готово, Mu можно запускать, он будет работать в виртуальном окружении pyneng-py3-7.
В этом же окружении делаем все остальное. 
Установить Python 3.7.

## С нуля на своем хосте/vm

### Windows

Windows - можно работать без вирт окружения.

Установить Mu

```
pip install mu-editor
```

### Linux/Mac OS

Создать виртуальное окружение (для Mac OS/Linux):

```
python3.7 -m venv ~/venv/pyneng-py3-7
```

Перейти в вирт окружение (Linux/Mac OS):

```
source ~/venv/pyneng-py3-7/bin/activate
```

Установить Mu

```
pip install mu-editor
```

Дальше все время работаем в виртуальном окружении pyneng-py3-7.
Можно записать переход в вирт. окружение в ``~/.bashrc`` или аналог для ОС.

# Вариант сложнее (плюс только в том что добавится кнопка Tidy для автоформатирования кода)

[Установка последней версии Mu](https://pyneng.github.io/docs/mu-prepare-new/)
