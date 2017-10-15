---
title: "Запись кириллицы и других не ASCII символов в формате JSON"
date: 2017-10-15
tags:
 - json
category:
 - pyneng-3
---

На лекции был пример записи данных, которые содержат кириллицу в файл формате JSON.
По умолчанию, вместо кириллицы, мы получили строку с кодами Unicode.

### Подготовка данных

Пример строки в формате JSON:
```python
In [20]: data ='{"login":"natenka","id":15850513,"avatar_url":"https://avatars0.githubusercontent.com/u/15850513?v=4","gravatar_id":"","url":"https://api.github.com/users/natenka","html_url":"https://github.com/natenka","followers_url":"https://api.github.com/users/natenka/followers","following_url":"https://api.github.com/users/natenka/following{/other_user}","gists_url":"https://api.github.com/users/natenka/gists{/gist_id}","starred_url":"https://api.github.com/users/natenka/starred{/owner}{/repo}","subscriptions_url":"https://api.github.com/users/natenka/subscriptions","organizations_url":"https://api.github.com/users/natenka/orgs","repos_url":"https://api.github.com/users/natenka/repos","events_url":"https://api.github.com/users/natenka/events{/privacy}","received_events_url":"https://api.github.com/users/natenka/received_events","type":"User","site_admin":false,"name":"Наташа Самойленко","company":null,"blog":"https://natenka.github.io/","location":null,"email":"natasha.samoylenko@gmail.com","hireable":null,"bio":null,"public_repos":11,"public_gists":2,"followers":49,"following":27,"created_at":"2015-11-14T20:32:44Z","updated_at":"2017-09-27T17:27:19Z","private_gists":0,"total_private_repos":0,"owned_private_repos":0,"disk_usage":53691,"collaborators":0,"two_factor_authentication":false,"plan":{"name":"free","space":976562499,"collaborators":0,"private_repos":0}}'

```

Для начала, получаем словарь Python из строки с помощью метода loads:
```python
In [21]: import json

In [22]: py_data = json.loads(data)

In [23]: py_data
Out[23]:
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
 'two_factor_authentication': False,
 'type': 'User',
 'updated_at': '2017-09-27T17:27:19Z',
 'url': 'https://api.github.com/users/natenka'}
```

### По умолчанию non-ASCII символы записываются как последовательность кодов юникод

Запись словаря в файл в формате JSON
```python
In [26]: with open('try_unicode.json', 'w') as f:
    ...:     json.dump(py_data, f, indent=2)
    ...:
```

Итоговый результат:
```python
In [27]: cat try_unicode.json
{
  "login": "natenka",
  "id": 15850513,
  "avatar_url": "https://avatars0.githubusercontent.com/u/15850513?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/natenka",
  "html_url": "https://github.com/natenka",
  "followers_url": "https://api.github.com/users/natenka/followers",
  "following_url": "https://api.github.com/users/natenka/following{/other_user}",
  "gists_url": "https://api.github.com/users/natenka/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/natenka/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/natenka/subscriptions",
  "organizations_url": "https://api.github.com/users/natenka/orgs",
  "repos_url": "https://api.github.com/users/natenka/repos",
  "events_url": "https://api.github.com/users/natenka/events{/privacy}",
  "received_events_url": "https://api.github.com/users/natenka/received_events",
  "type": "User",
  "site_admin": false,
  "name": "\u041d\u0430\u0442\u0430\u0448\u0430 \u0421\u0430\u043c\u043e\u0439\u043b\u0435\u043d\u043a\u043e",
  "company": null,
  "blog": "https://natenka.github.io/",
  "location": null,
  "email": "natasha.samoylenko@gmail.com",
  "hireable": null,
  "bio": null,
  "public_repos": 11,
  "public_gists": 2,
  "followers": 49,
  "following": 27,
  "created_at": "2015-11-14T20:32:44Z",
  "updated_at": "2017-09-27T17:27:19Z",
  "private_gists": 0,
  "total_private_repos": 0,
  "owned_private_repos": 0,
  "disk_usage": 53691,
  "collaborators": 0,
  "two_factor_authentication": false,
  "plan": {
    "name": "free",
    "space": 976562499,
    "collaborators": 0,
    "private_repos": 0
  }
}
```

Обратите внимание на ключ name:
```python
"name": "\u041d\u0430\u0442\u0430\u0448\u0430 \u0421\u0430\u043c\u043e\u0439\u043b\u0435\u043d\u043a\u043e"
```

Если этот файл будет использоваться только скриптом, никаких проблем не будет.
Мы можем считать его и получить тот же словарь в Python с кириллицей:
```python
In [36]: with open('try_unicode.json') as f:
    ...:     result = json.load(f)
    ...:

In [37]: result
Out[37]:
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
 'two_factor_authentication': False,
 'type': 'User',
 'updated_at': '2017-09-27T17:27:19Z',
 'url': 'https://api.github.com/users/natenka'}
```

### Параметр ensure_ascii

Но, если этот файл нужно будет читать и человеку, то лучше чтобы все non-ASCII символы отображались нормально.

За это отвечает параметр ensure_ascii:
```python
In [38]: with open('try_unicode.json', 'w') as f:
    ...:     json.dump(py_data, f, indent=2, ensure_ascii=False)
    ...:
```

Теперь кириллица записана нормально:
```python
In [39]: cat try_unicode.json
{
  "login": "natenka",
  "id": 15850513,
  "avatar_url": "https://avatars0.githubusercontent.com/u/15850513?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/natenka",
  "html_url": "https://github.com/natenka",
  "followers_url": "https://api.github.com/users/natenka/followers",
  "following_url": "https://api.github.com/users/natenka/following{/other_user}",
  "gists_url": "https://api.github.com/users/natenka/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/natenka/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/natenka/subscriptions",
  "organizations_url": "https://api.github.com/users/natenka/orgs",
  "repos_url": "https://api.github.com/users/natenka/repos",
  "events_url": "https://api.github.com/users/natenka/events{/privacy}",
  "received_events_url": "https://api.github.com/users/natenka/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Наташа Самойленко",
  "company": null,
  "blog": "https://natenka.github.io/",
  "location": null,
  "email": "natasha.samoylenko@gmail.com",
  "hireable": null,
  "bio": null,
  "public_repos": 11,
  "public_gists": 2,
  "followers": 49,
  "following": 27,
  "created_at": "2015-11-14T20:32:44Z",
  "updated_at": "2017-09-27T17:27:19Z",
  "private_gists": 0,
  "total_private_repos": 0,
  "owned_private_repos": 0,
  "disk_usage": 53691,
  "collaborators": 0,
  "two_factor_authentication": false,
  "plan": {
    "name": "free",
    "space": 976562499,
    "collaborators": 0,
    "private_repos": 0
  }
}
```


