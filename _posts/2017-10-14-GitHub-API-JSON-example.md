---
title: "Пример работы с GitHub API с помощью requests"
date: 2017-10-14
tags:
 - requests
 - json
category:
 - pyneng-3
---

На лекции был пример получения информации через GitHub API с помощью requests.
В основном он использовался как пример получения данных в формате JSON, но как базовый пример использования requests он тоже подойдет.


## Базовый пример

Для начала работы с requests, его надо установить:
```
pip install requests
```

Затем импортировать модуль:
```python
In [1]: import requests
```

И указать логин и токен для подключения на GitHub (берется тот же токен, который используется для ptest):
```python
In [2]: import os

In [3]: username = 'natenka'

In [4]: token = os.environ.get("GITHUB_TOKEN")
```

Этот запрос позволяет получить [информацию о пользователе](https://developer.github.com/v3/users/#get-the-authenticated-user):
```python
In [5]: r = requests.get('https://api.github.com/user', auth=(username, token))
```

> Все ссылки, которые используются для работы с GitHub API описаны в [документации](https://developer.github.com/v3/)

После выполнения запроса, можно просмотреть результат в формате JSON:
```python
In [6]: r.text
Out[6]: '{"login":"natenka","id":15850513,"avatar_url":"https://avatars0.githubusercontent.com/u/15850513?v=4","gravatar_id":"","url":"https://api.github.com/users/natenka","html_url":"https://github.com/natenka","followers_url":"https://api.github.com/users/natenka/followers","following_url":"https://api.github.com/users/natenka/following{/other_user}","gists_url":"https://api.github.com/users/natenka/gists{/gist_id}","starred_url":"https://api.github.com/users/natenka/starred{/owner}{/repo}","subscriptions_url":"https://api.github.com/users/natenka/subscriptions","organizations_url":"https://api.github.com/users/natenka/orgs","repos_url":"https://api.github.com/users/natenka/repos","events_url":"https://api.github.com/users/natenka/events{/privacy}","received_events_url":"https://api.github.com/users/natenka/received_events","type":"User","site_admin":false,"name":"Наташа Самойленко","company":null,"blog":"https://natenka.github.io/","location":null,"email":"natasha.samoylenko@gmail.com","hireable":null,"bio":null,"public_repos":11,"public_gists":2,"followers":49,"following":27,"created_at":"2015-11-14T20:32:44Z","updated_at":"2017-09-27T17:27:19Z","private_gists":0,"total_private_repos":0,"owned_private_repos":0,"disk_usage":53691,"collaborators":0,"two_factor_authentication":false,"plan":{"name":"free","space":976562499,"collaborators":0,"private_repos":0}}'
```

Метод json конвертирует строку в формате JSON в объекты Python:
```python
In [7]: r.json()
Out[7]:
{'avatar_url': 'https://avatars0.githubusercontent.com/u/15850513?v=4',
 'bio': None,
 'blog': 'https://natenka.github.io/',
 'collaborators': 0,
 'company': None,
 'created_at': '2015-11-14T20:32:44Z',
 'disk_usage': 53691,
 'email': 'natasha.samoylenko@gmail.com',
 'events_url': 'https://api.github.com/users/natenka/events{/privacy}',
 'followers': 49,
 'followers_url': 'https://api.github.com/users/natenka/followers',
 'following': 27,
 'following_url': 'https://api.github.com/users/natenka/following{/other_user}',
 'gists_url': 'https://api.github.com/users/natenka/gists{/gist_id}',
 'gravatar_id': '',
 'hireable': None,
 'html_url': 'https://github.com/natenka',
 'id': 15850513,
 'location': None,
 'login': 'natenka',
 'name': 'Наташа Самойленко',
 'organizations_url': 'https://api.github.com/users/natenka/orgs',
 'owned_private_repos': 0,
 'plan': {'collaborators': 0,
  'name': 'free',
  'private_repos': 0,
  'space': 976562499},
 'private_gists': 0,
 'public_gists': 2,
 'public_repos': 11,
 'received_events_url': 'https://api.github.com/users/natenka/received_events',
 'repos_url': 'https://api.github.com/users/natenka/repos',
 'site_admin': False,
 'starred_url': 'https://api.github.com/users/natenka/starred{/owner}{/repo}',
 'subscriptions_url': 'https://api.github.com/users/natenka/subscriptions',
 'total_private_repos': 0,
 'type': 'User',
 'updated_at': '2017-09-27T17:27:19Z',
 'url': 'https://api.github.com/users/natenka'}

```

## Получить все репозитории пользователя

Для получения [всех ваших репозиториев](https://developer.github.com/v3/repos/#list-your-repositories), используется ссылка `https://api.github.com/user/repos`
```python
In [8]: repos = requests.get('https://api.github.com/user/repos', auth=(username, token))
```

Пример информации о репозитории (сокращенный):
```python
In [10]: repos.json()[1]
Out[10]:
{'archive_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/{archive_format}{/ref}',
 'created_at': '2017-01-10T09:36:16Z',
 'default_branch': 'master',
 'deployments_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/deployments',
 'description': 'Репозиторий курса "Ansible для сетевых инженеров". Курс находится на GitBook: https://www.gitbook.com/book/natenka/ansible-dlya-setevih-inzhenerov',
 'downloads_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/downloads',
 'events_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/events',
 'fork': False,
 'forks': 4,
 'forks_count': 4,
 'forks_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/forks',
 'full_name': 'natenka/Ansible-for-network-engineers',
 'hooks_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/hooks',
 'html_url': 'https://github.com/natenka/Ansible-for-network-engineers',
 'id': 78518623,
 'name': 'Ansible-for-network-engineers',
 'notifications_url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers/notifications{?since,all,participating}',
 'open_issues': 0,
 'open_issues_count': 0,
 'owner': {'avatar_url': 'https://avatars0.githubusercontent.com/u/15850513?v=4',
  'events_url': 'https://api.github.com/users/natenka/events{/privacy}',
  'followers_url': 'https://api.github.com/users/natenka/followers',
  'following_url': 'https://api.github.com/users/natenka/following{/other_user}',
  'gists_url': 'https://api.github.com/users/natenka/gists{/gist_id}',
  'gravatar_id': '',
  'html_url': 'https://github.com/natenka',
  'id': 15850513,
  'login': 'natenka',
  'organizations_url': 'https://api.github.com/users/natenka/orgs',
  'received_events_url': 'https://api.github.com/users/natenka/received_events',
  'repos_url': 'https://api.github.com/users/natenka/repos',
  'site_admin': False,
  'starred_url': 'https://api.github.com/users/natenka/starred{/owner}{/repo}',
  'subscriptions_url': 'https://api.github.com/users/natenka/subscriptions',
  'type': 'User',
  'url': 'https://api.github.com/users/natenka'},
 'permissions': {'admin': True, 'pull': True, 'push': True},
 'private': False,
 'ssh_url': 'git@github.com:natenka/Ansible-for-network-engineers.git',
 'stargazers_count': 9,
 'updated_at': '2017-10-10T06:50:33Z',
 'url': 'https://api.github.com/repos/natenka/Ansible-for-network-engineers',
 'watchers': 9,
 'watchers_count': 9}
```

Таким образом можно вывести ссылку всех public репозиториев:
```
In [12]: for repo in repos.json():
    ...:     if not repo['private']:
    ...:         print(repo['html_url'])
    ...:
https://github.com/linkmeup/CCIE
https://github.com/natenka/Ansible-for-network-engineers
https://github.com/natenka/grade-system
https://github.com/natenka/Its_Clojure_Time
https://github.com/natenka/My_Coding_Challenges
https://github.com/natenka/My_Scripts
https://github.com/natenka/natenka.github.io
https://github.com/natenka/NetDay
https://github.com/natenka/PyNEng
https://github.com/natenka/pyneng-examples-exercises
https://github.com/natenka/pyneng-slides
https://github.com/natenka/python-ansible-experiments
https://github.com/pyneng/pyneng-online-jun-jul-2017
https://github.com/pyneng/pyneng.github.io

```

## Получение файла

Аналогичным образом через GitHub API [можно получить файл](https://developer.github.com/v3/repos/contents/#get-contents):
```python
In [13]: file_path = 'exercises/10_serialization/task_10_2c.py'

In [14]: github_api_file_url = 'https://api.github.com/repos/natenka/pyneng-examples-exercises/contents/'

In [15]: file_response = requests.get(github_api_file_url+file_path, auth=(username, token))
```

Результат:
```python
In [16]: file_response.json()
Out[16]:
{'_links': {'git': 'https://api.github.com/repos/natenka/pyneng-examples-exercises/git/blobs/815db87494071a883cc16d257a99cf024bdb1d0b',
  'html': 'https://github.com/natenka/pyneng-examples-exercises/blob/master/exercises/10_serialization/task_10_2c.py',
  'self': 'https://api.github.com/repos/natenka/pyneng-examples-exercises/contents/exercises/10_serialization/task_10_2c.py?ref=master'},
 'content': 'IyAtKi0gY29kaW5nOiB1dGYtOCAtKi0KCicnJwrQl9Cw0LTQsNC90LjQtSAx\nMC4yYwoK0KEg0L/QvtC80L7RidGM0Y4g0YTRg9C90LrRhtC40LggZHJhd190\nb3BvbG9neSDQuNC3INGE0LDQudC70LAgZHJhd19uZXR3b3JrX2dyYXBoLnB5\nCtGB0LPQtdC90LXRgNC40YDQvtCy0LDRgtGMINGC0L7Qv9C+0LvQvtCz0LjR\njiwg0LrQvtGC0L7RgNCw0Y8g0YHQvtC+0YLQstC10YLRgdGC0LLRg9C10YIg\n0L7Qv9C40YHQsNC90LjRjiDQsiDRhNCw0LnQu9C1IHRvcG9sb2d5LnlhbWwK\nCtCe0LHRgNCw0YLQuNGC0LUg0LLQvdC40LzQsNC90LjQtSDQvdCwINGC0L4s\nINC60LDQutC+0Lkg0YTQvtGA0LzQsNGCINC00LDQvdC90YvRhSDQvtC20LjQ\ntNCw0LXRgiDRhNGD0L3QutGG0LjRjyBkcmF3X3RvcG9sb2d5LgrQntC/0LjR\ngdCw0L3QuNC1INGC0L7Qv9C+0LvQvtCz0LjQuCDQuNC3INGE0LDQudC70LAg\ndG9wb2xvZ3kueWFtbCDQvdGD0LbQvdC+INC/0YDQtdC+0LHRgNCw0LfQvtCy\n0LDRgtGMINGB0L7QvtGC0LLQtdGC0YHRgtCy0YPRjtGJ0LjQvCDQvtCx0YDQ\nsNC30L7QvCwK0YfRgtC+0LHRiyDQuNGB0L/QvtC70YzQt9C+0LLQsNGC0Ywg\n0YTRg9C90LrRhtC40Y4gZHJhd190b3BvbG9neS4KCtCU0LvRjyDRgNC10YjQ\ntdC90LjRjyDQt9Cw0LTQsNC90LjRjyDQvNC+0LbQvdC+INGB0L7Qt9C00LDR\ngtGMINC70Y7QsdGL0LUg0LLRgdC/0L7QvNC+0LPQsNGC0LXQu9GM0L3Ri9C1\nINGE0YPQvdC60YbQuNC4LgoK0J3QtSDQutC+0L/QuNGA0L7QstCw0YLRjCDQ\nutC+0LQg0YTRg9C90LrRhtC40LggZHJhd190b3BvbG9neS4KCtCSINC40YLQ\nvtCz0LUsINC00L7Qu9C20L3QviDQsdGL0YLRjCDRgdCz0LXQvdC10YDQuNGA\n0L7QstCw0L3QviDQuNC30L7QsdGA0LDQttC10L3QuNC1INGC0L7Qv9C+0LvQ\nvtCz0LjQuC4K0KDQtdC30YPQu9GM0YLQsNGCINC00L7Qu9C20LXQvSDQstGL\n0LPQu9GP0LTQtdGC0Ywg0YLQsNC6INC20LUsINC60LDQuiDRgdGF0LXQvNCw\nINCyINGE0LDQudC70LUgdGFza18xMF8yY190b3BvbG9neS5zdmcKCtCf0YDQ\nuCDRjdGC0L7QvDoKKiDQmNC90YLQtdGA0YTQtdC50YHRiyDQvNC+0LPRg9GC\nINCx0YvRgtGMINC30LDQv9C40YHQsNC90Ysg0YEg0L/RgNC+0LHQtdC70L7Q\nvCBGYSAwLzAg0LjQu9C4INCx0LXQtyBGYTAvMC4KKiDQoNCw0YHQv9C+0LvQ\nvtC20LXQvdC40LUg0YPRgdGC0YDQvtC50YHRgtCyINC90LAg0YHRhdC10LzQ\ntSDQvNC+0LbQtdGCINCx0YvRgtGMINC00YDRg9Cz0LjQvAoqINCh0L7QtdC0\n0LjQvdC10L3QuNGPINC00L7Qu9C20L3RiyDRgdC+0L7RgtCy0LXRgtGB0YLQ\nstC+0LLQsNGC0Ywg0YHRhdC10LzQtQoKCj4g0JTQu9GPINCy0YvQv9C+0LvQ\nvdC10L3QuNGPINGN0YLQvtCz0L4g0LfQsNC00LDQvdC40Y8sINC00L7Qu9C2\n0LXQvSDQsdGL0YLRjCDRg9GB0YLQsNC90L7QstC70LXQvSBncmFwaHZpejoK\nPiBhcHQtZ2V0IGluc3RhbGwgZ3JhcGh2aXoKCj4g0Jgg0LzQvtC00YPQu9GM\nIHB5dGhvbiDQtNC70Y8g0YDQsNCx0L7RgtGLINGBIGdyYXBodml6Ogo+IHBp\ncCBpbnN0YWxsIGdyYXBodml6CgonJycK\n',
 'download_url': 'https://raw.githubusercontent.com/natenka/pyneng-examples-exercises/master/exercises/10_serialization/task_10_2c.py',
 'encoding': 'base64',
 'git_url': 'https://api.github.com/repos/natenka/pyneng-examples-exercises/git/blobs/815db87494071a883cc16d257a99cf024bdb1d0b',
 'html_url': 'https://github.com/natenka/pyneng-examples-exercises/blob/master/exercises/10_serialization/task_10_2c.py',
 'name': 'task_10_2c.py',
 'path': 'exercises/10_serialization/task_10_2c.py',
 'sha': '815db87494071a883cc16d257a99cf024bdb1d0b',
 'size': 1554,
 'type': 'file',
 'url': 'https://api.github.com/repos/natenka/pyneng-examples-exercises/contents/exercises/10_serialization/task_10_2c.py?ref=master'}

```

Обратите внимание на поле encoding:
```python
In [17]: file_response.json()['encoding']
Out[17]: 'base64'
```

Чтобы получить содержимое файла, нужно использовать [модуль base64](https://docs.python.org/3/library/base64.html):
```python
In [18]: import base64
```

Модуль позволяет декодировать строку и возвращает байты:
```
In [19]: file_bytes = base64.b64decode(file_response.json()['content'])

In [20]: file_bytes
Out[88]: b"# -*- coding: utf-8 -*-\n\n'''\n\xd0\x97\xd0\xb0\xd0\xb4\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5 10.2c\n\n\xd0\xa1 \xd0\xbf\xd0\xbe\xd0\xbc\xd0\xbe\xd1\x89\xd1\x8c\xd1\x8e \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8 draw_topology \xd0\xb8\xd0\xb7 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 draw_network_graph.py\n\xd1\x81\xd0\xb3\xd0\xb5\xd0\xbd\xd0\xb5\xd1\x80\xd0\xb8\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd1\x82\xd0\xbe\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbe\xd0\xb3\xd0\xb8\xd1\x8e, \xd0\xba\xd0\xbe\xd1\x82\xd0\xbe\xd1\x80\xd0\xb0\xd1\x8f \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd1\x83\xd0\xb5\xd1\x82 \xd0\xbe\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x8e \xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb5 topology.yaml\n\n\xd0\x9e\xd0\xb1\xd1\x80\xd0\xb0\xd1\x82\xd0\xb8\xd1\x82\xd0\xb5 \xd0\xb2\xd0\xbd\xd0\xb8\xd0\xbc\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5 \xd0\xbd\xd0\xb0 \xd1\x82\xd0\xbe, \xd0\xba\xd0\xb0\xd0\xba\xd0\xbe\xd0\xb9 \xd1\x84\xd0\xbe\xd1\x80\xd0\xbc\xd0\xb0\xd1\x82 \xd0\xb4\xd0\xb0\xd0\xbd\xd0\xbd\xd1\x8b\xd1\x85 \xd0\xbe\xd0\xb6\xd0\xb8\xd0\xb4\xd0\xb0\xd0\xb5\xd1\x82 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd1\x8f draw_topology.\n\xd0\x9e\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x82\xd0\xbe\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbe\xd0\xb3\xd0\xb8\xd0\xb8 \xd0\xb8\xd0\xb7 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb0 topology.yaml \xd0\xbd\xd1\x83\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xbf\xd1\x80\xd0\xb5\xd0\xbe\xd0\xb1\xd1\x80\xd0\xb0\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd1\x83\xd1\x8e\xd1\x89\xd0\xb8\xd0\xbc \xd0\xbe\xd0\xb1\xd1\x80\xd0\xb0\xd0\xb7\xd0\xbe\xd0\xbc,\n\xd1\x87\xd1\x82\xd0\xbe\xd0\xb1\xd1\x8b \xd0\xb8\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd1\x8c\xd0\xb7\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd1\x8e draw_topology.\n\n\xd0\x94\xd0\xbb\xd1\x8f \xd1\x80\xd0\xb5\xd1\x88\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8f \xd0\xb7\xd0\xb0\xd0\xb4\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x8f \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xbd\xd0\xbe \xd1\x81\xd0\xbe\xd0\xb7\xd0\xb4\xd0\xb0\xd1\x82\xd1\x8c \xd0\xbb\xd1\x8e\xd0\xb1\xd1\x8b\xd0\xb5 \xd0\xb2\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbc\xd0\xbe\xd0\xb3\xd0\xb0\xd1\x82\xd0\xb5\xd0\xbb\xd1\x8c\xd0\xbd\xd1\x8b\xd0\xb5 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8.\n\n\xd0\x9d\xd0\xb5 \xd0\xba\xd0\xbe\xd0\xbf\xd0\xb8\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd0\xba\xd0\xbe\xd0\xb4 \xd1\x84\xd1\x83\xd0\xbd\xd0\xba\xd1\x86\xd0\xb8\xd0\xb8 draw_topology.\n\n\xd0\x92 \xd0\xb8\xd1\x82\xd0\xbe\xd0\xb3\xd0\xb5, \xd0\xb4\xd0\xbe\xd0\xbb\xd0\xb6\xd0\xbd\xd0\xbe \xd0\xb1\xd1\x8b\xd1\x82\xd1\x8c \xd1\x81\xd0\xb3\xd0\xb5\xd0\xbd\xd0\xb5\xd1\x80\xd0\xb8\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb0\xd0\xbd\xd0\xbe \xd0\xb8\xd0\xb7\xd0\xbe\xd0\xb1\xd1\x80\xd0\xb0\xd0\xb6\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x82\xd0\xbe\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbe\xd0\xb3\xd0\xb8\xd0\xb8.\n\xd0\xa0\xd0\xb5\xd0\xb7\xd1\x83\xd0\xbb\xd1\x8c\xd1\x82\xd0\xb0\xd1\x82 \xd0\xb4\xd0\xbe\xd0\xbb\xd0\xb6\xd0\xb5\xd0\xbd \xd0\xb2\xd1\x8b\xd0\xb3\xd0\xbb\xd1\x8f\xd0\xb4\xd0\xb5\xd1\x82\xd1\x8c \xd1\x82\xd0\xb0\xd0\xba \xd0\xb6\xd0\xb5, \xd0\xba\xd0\xb0\xd0\xba \xd1\x81\xd1\x85\xd0\xb5\xd0\xbc\xd0\xb0 \xd0\xb2 \xd1\x84\xd0\xb0\xd0\xb9\xd0\xbb\xd0\xb5 task_10_2c_topology.svg\n\n\xd0\x9f\xd1\x80\xd0\xb8 \xd1\x8d\xd1\x82\xd0\xbe\xd0\xbc:\n* \xd0\x98\xd0\xbd\xd1\x82\xd0\xb5\xd1\x80\xd1\x84\xd0\xb5\xd0\xb9\xd1\x81\xd1\x8b \xd0\xbc\xd0\xbe\xd0\xb3\xd1\x83\xd1\x82 \xd0\xb1\xd1\x8b\xd1\x82\xd1\x8c \xd0\xb7\xd0\xb0\xd0\xbf\xd0\xb8\xd1\x81\xd0\xb0\xd0\xbd\xd1\x8b \xd1\x81 \xd0\xbf\xd1\x80\xd0\xbe\xd0\xb1\xd0\xb5\xd0\xbb\xd0\xbe\xd0\xbc Fa 0/0 \xd0\xb8\xd0\xbb\xd0\xb8 \xd0\xb1\xd0\xb5\xd0\xb7 Fa0/0.\n* \xd0\xa0\xd0\xb0\xd1\x81\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbe\xd0\xb6\xd0\xb5\xd0\xbd\xd0\xb8\xd0\xb5 \xd1\x83\xd1\x81\xd1\x82\xd1\x80\xd0\xbe\xd0\xb9\xd1\x81\xd1\x82\xd0\xb2 \xd0\xbd\xd0\xb0 \xd1\x81\xd1\x85\xd0\xb5\xd0\xbc\xd0\xb5 \xd0\xbc\xd0\xbe\xd0\xb6\xd0\xb5\xd1\x82 \xd0\xb1\xd1\x8b\xd1\x82\xd1\x8c \xd0\xb4\xd1\x80\xd1\x83\xd0\xb3\xd0\xb8\xd0\xbc\n* \xd0\xa1\xd0\xbe\xd0\xb5\xd0\xb4\xd0\xb8\xd0\xbd\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8f \xd0\xb4\xd0\xbe\xd0\xbb\xd0\xb6\xd0\xbd\xd1\x8b \xd1\x81\xd0\xbe\xd0\xbe\xd1\x82\xd0\xb2\xd0\xb5\xd1\x82\xd1\x81\xd1\x82\xd0\xb2\xd0\xbe\xd0\xb2\xd0\xb0\xd1\x82\xd1\x8c \xd1\x81\xd1\x85\xd0\xb5\xd0\xbc\xd0\xb5\n\n\n> \xd0\x94\xd0\xbb\xd1\x8f \xd0\xb2\xd1\x8b\xd0\xbf\xd0\xbe\xd0\xbb\xd0\xbd\xd0\xb5\xd0\xbd\xd0\xb8\xd1\x8f \xd1\x8d\xd1\x82\xd0\xbe\xd0\xb3\xd0\xbe \xd0\xb7\xd0\xb0\xd0\xb4\xd0\xb0\xd0\xbd\xd0\xb8\xd1\x8f, \xd0\xb4\xd0\xbe\xd0\xbb\xd0\xb6\xd0\xb5\xd0\xbd \xd0\xb1\xd1\x8b\xd1\x82\xd1\x8c \xd1\x83\xd1\x81\xd1\x82\xd0\xb0\xd0\xbd\xd0\xbe\xd0\xb2\xd0\xbb\xd0\xb5\xd0\xbd graphviz:\n> apt-get install graphviz\n\n> \xd0\x98 \xd0\xbc\xd0\xbe\xd0\xb4\xd1\x83\xd0\xbb\xd1\x8c python \xd0\xb4\xd0\xbb\xd1\x8f \xd1\x80\xd0\xb0\xd0\xb1\xd0\xbe\xd1\x82\xd1\x8b \xd1\x81 graphviz:\n> pip install graphviz\n\n'''\n"

```

Чтобы получить строку Python, используется decode:
```python
In [21]: file_str = file_bytes.decode('utf-8')

In [22]: print(file_str)
# -*- coding: utf-8 -*-

'''
Задание 10.2c

С помощью функции draw_topology из файла draw_network_graph.py
сгенерировать топологию, которая соответствует описанию в файле topology.yaml

Обратите внимание на то, какой формат данных ожидает функция draw_topology.
Описание топологии из файла topology.yaml нужно преобразовать соответствующим образом,
чтобы использовать функцию draw_topology.

Для решения задания можно создать любые вспомогательные функции.

Не копировать код функции draw_topology.

В итоге, должно быть сгенерировано изображение топологии.
Результат должен выглядеть так же, как схема в файле task_10_2c_topology.svg

При этом:
* Интерфейсы могут быть записаны с пробелом Fa 0/0 или без Fa0/0.
* Расположение устройств на схеме может быть другим
* Соединения должны соответствовать схеме


> Для выполнения этого задания, должен быть установлен graphviz:
> apt-get install graphviz

> И модуль python для работы с graphviz:
> pip install graphviz

'''

```


## Создание файла

Для [создания файла](https://developer.github.com/v3/repos/contents/#create-a-file) надо передать его содержимое в кодировке Base64.
При этом, сама кодировка ожидает байты и возвращает байты, а формату JSON надо передать строку, а не байты.

Поэтому надо сделать несколько конвертаций, чтобы в итоге получить нужный формат:
```python
In [25]: content = 'Проверка GitHub API'

In [26]: b_content = content.encode('utf-8')

In [27]: b_content
Out[27]: b'\xd0\x9f\xd1\x80\xd0\xbe\xd0\xb2\xd0\xb5\xd1\x80\xd0\xba\xd0\xb0 GitHub API'

In [28]: base64_content = base64.b64encode(b_content)

In [29]: base64_content
Out[29]: b'0J/RgNC+0LLQtdGA0LrQsCBHaXRIdWIgQVBJ'

In [30]: base64_content_str = base64_content.decode('utf-8')

In [31]: base64_content_str
Out[31]: '0J/RgNC+0LLQtdGA0LrQsCBHaXRIdWIgQVBJ'
```

Теперь можно составить словарь с параметрами файла:
```python
In [32]: f = {'path':'',
    ...:      'message': 'Create new file via GitHub API',
    ...:      'content': base64_content_str}
    ...:
```

И передать его как строку в параметр data:
```python
In [33]: f_resp = requests.put('https://api.github.com/repos/natenka/My_Scripts/contents/try_gh_api.md',
    ...:                       auth=(username, token),
    ...:                       headers={"Content-Type": "application/json"},
    ...:                       data=json.dumps(f))
    ...:
```

> [Итоговый файл в моем репозитории](https://github.com/natenka/My_Scripts/blob/master/try_gh_api.md)


Ответ в формате JSON:
```python
In [35]: f_resp.json()
Out[35]:
{'commit': {'author': {'date': '2017-10-14T15:19:35Z',
   'email': 'nataliya.samoylenko@gmail.com',
   'name': 'Наташа Самойленко'},
  'committer': {'date': '2017-10-14T15:19:35Z',
   'email': 'nataliya.samoylenko@gmail.com',
   'name': 'Наташа Самойленко'},
  'html_url': 'https://github.com/natenka/My_Scripts/commit/5d70c0320e344b431e09ef1a64e8e9c043000bb1',
  'message': 'Create new file via GitHub API',
  'parents': [{'html_url': 'https://github.com/natenka/My_Scripts/commit/9896e5cc60881045046bc34e4abd656b97ad2266',
    'sha': '9896e5cc60881045046bc34e4abd656b97ad2266',
    'url': 'https://api.github.com/repos/natenka/My_Scripts/git/commits/9896e5cc60881045046bc34e4abd656b97ad2266'}],
  'sha': '5d70c0320e344b431e09ef1a64e8e9c043000bb1',
  'tree': {'sha': '3dde275cf96dd1ca59f171a282df7e4fe871158f',
   'url': 'https://api.github.com/repos/natenka/My_Scripts/git/trees/3dde275cf96dd1ca59f171a282df7e4fe871158f'},
  'url': 'https://api.github.com/repos/natenka/My_Scripts/git/commits/5d70c0320e344b431e09ef1a64e8e9c043000bb1',
  'verification': {'payload': None,
   'reason': 'unsigned',
   'signature': None,
   'verified': False}},
 'content': {'_links': {'git': 'https://api.github.com/repos/natenka/My_Scripts/git/blobs/16c126f1181e013c8f72846f7b92dcff7a207ed9',
   'html': 'https://github.com/natenka/My_Scripts/blob/master/try_gh_api.md',
   'self': 'https://api.github.com/repos/natenka/My_Scripts/contents/try_gh_api.md?ref=master'},
  'download_url': 'https://raw.githubusercontent.com/natenka/My_Scripts/master/try_gh_api.md',
  'git_url': 'https://api.github.com/repos/natenka/My_Scripts/git/blobs/16c126f1181e013c8f72846f7b92dcff7a207ed9',
  'html_url': 'https://github.com/natenka/My_Scripts/blob/master/try_gh_api.md',
  'name': 'try_gh_api.md',
  'path': 'try_gh_api.md',
  'sha': '16c126f1181e013c8f72846f7b92dcff7a207ed9',
  'size': 27,
  'type': 'file',
  'url': 'https://api.github.com/repos/natenka/My_Scripts/contents/try_gh_api.md?ref=master'}}
```



## Дополнительная информация

* [Requests. Quickstart](http://docs.python-requests.org/en/master/user/quickstart/)
* [GitHub REST API v3](https://developer.github.com/v3/)

