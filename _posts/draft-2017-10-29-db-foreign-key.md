---
title: "SQLite foreign key"
date: 2017-10-29
tags:
 - sqlite
 - db
 - sql
category:
 - pyneng-3
---

В заданиях 11 раздела создается база данных с двумя таблицами: dhcp и switches.

Таблица dhcp (показана часть записей):

| mac | ip  | vlan  | interface | switch |
|:---:|:---:|:-----:|:---------:|:------:|
|00:07:BC:3F:A6:50 |10.1.10.6  |10  |FastEthernet0/3 |sw1|
|00:09:BC:3F:A6:50 |192.168.10 |1   |FastEthernet0/7 |sw1|
|00:A9:BB:3D:D6:58 |10.1.10.20 |10  |FastEthernet0/7 |sw2|
|00:B4:A3:3E:5B:69 |10.1.5.20  |5   |FastEthernet0/5 |sw2|
|00:E9:BC:3F:A6:50 |100.1.1.6  |3   |FastEthernet0/2 |sw3|


Таблица switches:

|hostname |   location |
|:-------:|:-------------------------:|
|sw1      | London, 21 New Globe Walk |
|sw2      | London, 21 New Globe Walk |
|sw3      | London, 21 New Globe Walk |


Столбец switch в таблице dhcp указывает на коммутатор, на котором была найдена запись.
При этом, в таблице switches указан соответствующий коммутатор и его расположение.

В SQL есть возможность создавать связь между таблицами.
Например, можно сделать так, что при удалении коммутатора из таблицы switches будут удаляться все записи таблицы dhcp, у которых в столбце switch указан этот коммутатор.

Связь между таблицами создается с помощью внешнего ключа (foreign key).

Внешний ключ указывает каким образом связаны таблицы в базе данных, а также контролирует изменение данных.

Пример создания внешнего ключа (файл dhcp_snooping_schema_ver1.sql):
```sql
create table switches (
    hostname    text not null primary key,
    location    text
);

create table dhcp (
    mac          text primary key,
    ip           text,
    vlan         text,
    interface    text,
    switch       text not null,
    FOREIGN KEY (switch) references switches(hostname)
);
```

При такой настройке столбец switch в таблице dhcp является внешним ключом.
Он указывает на столбец hostname в таблице switches.

Как правило, внешний ключ ссылается на primary key, но может также ссылаться на поле с ограничением UNIQUE.

Таблица switches, в данном случае, называется родительской по отношению к таблице dhcp.

### Подготовка

Для того чтобы посмотреть на внешний ключ в действии, надо добавить данные в таблицы.

Для начала надо создать таблицы:
```
$ sqlite3 dhcp_snooping.db

sqlite> .read dhcp_snooping_schema_ver1.sql

sqlite> .tables
dhcp      switches
```

После выполнения команд выше, надо заполнить таблицы.
Это можно сделать импортировав данные из подготовленных CSV файлов:
```
sqlite> .mode csv
sqlite> .import dhcp.csv dhcp
sqlite> .import switches.csv switches
sqlite> .mode column
```

Таблица switches:
```sql
sqlite> select * from switches;
hostname    location
----------  -------------------------
sw1         London, 21 New Globe Walk
sw2         London, 21 New Globe Walk
sw3         London, 21 New Globe Walk
```

Таблица dhcp:
```sql
sqlite> select * from dhcp;
mac                ip          vlan        interface        switch
-----------------  ----------  ----------  ---------------  ----------
00:09:BB:3D:D6:58  10.1.10.2   10          FastEthernet0/1  sw1
00:04:A3:3E:5B:69  10.1.5.2    5           FastEthernet0/1  sw1
00:05:B3:7E:9B:60  10.1.5.4    5           FastEthernet0/9  sw1
00:07:BC:3F:A6:50  10.1.10.6   10          FastEthernet0/3  sw1
00:09:BC:3F:A6:50  192.168.10  1           FastEthernet0/7  sw1
00:E9:BC:3F:A6:50  100.1.1.6   3           FastEthernet0/2  sw3
00:A9:BB:3D:D6:58  10.1.10.20  10          FastEthernet0/7  sw2
00:B4:A3:3E:5B:69  10.1.5.20   5           FastEthernet0/5  sw2
00:C5:B3:7E:9B:60  10.1.5.40   5           FastEthernet0/9  sw2
00:A9:BC:3F:A6:50  10.1.10.60  20          FastEthernet0/2  sw2
```

### Внешний ключ

В sqlite3 по умолчанию выключено соблюдение ограничений внешнего ключа.
Для включения используется такая команда:
```sql
sqlite> PRAGMA foreign_keys = ON;
```

> Команда ```PRAGMA foreign_keys = ON;``` должна указываться для каждого подключения к БД.

Теперь, если попробовать добавить в таблицу dhcp запись с коммутатором, которого нет в таблице switches, возникнет ошибка:
```
sqlite> INSERT into dhcp
   ...> values ('00:A9:0C:4F:55:50', '10.1.3.1', '10', 'FastEthernet0/19', 'sw4');
Error: FOREIGN KEY constraint failed
```

Внешний ключ не дает добавлять данные в таблицу dhcp из-за того, что в таблице switches не существует коммутатора sw4.
Если добавить коммутатор и повторить команду, она отработает.

Кроме того, нельзя удалить коммутатор из таблицы switches, если в таблице dhcp есть записи, которые указывают на него:
```
sqlite> delete from switches where hostname = 'sw2';
Error: FOREIGN KEY constraint failed
```

Очень важно не забывать включать ограничение.
Иначе, несмотря на наличие внешнего ключа, он не будет работать.


Например, можно отключить поддержку внешнего ключа и попытаться выполнить команду еще раз:
```sql
sqlite> PRAGMA foreign_keys = OFF;

sqlite> INSERT into dhcp
   ...> values ('00:A9:0C:4F:55:50', '10.1.3.1', '10', 'FastEthernet0/19', 'sw4');

sqlite> select * from dhcp;
mac                ip          vlan        interface        switch
-----------------  ----------  ----------  ---------------  ----------
00:09:BB:3D:D6:58  10.1.10.2   10          FastEthernet0/1  sw1
00:04:A3:3E:5B:69  10.1.5.2    5           FastEthernet0/1  sw1
00:05:B3:7E:9B:60  10.1.5.4    5           FastEthernet0/9  sw1
00:07:BC:3F:A6:50  10.1.10.6   10          FastEthernet0/3  sw1
00:09:BC:3F:A6:50  192.168.10  1           FastEthernet0/7  sw1
00:E9:BC:3F:A6:50  100.1.1.6   3           FastEthernet0/2  sw3
00:A9:BB:3D:D6:58  10.1.10.20  10          FastEthernet0/7  sw2
00:B4:A3:3E:5B:69  10.1.5.20   5           FastEthernet0/5  sw2
00:C5:B3:7E:9B:60  10.1.5.40   5           FastEthernet0/9  sw2
00:A9:BC:3F:A6:50  10.1.10.60  20          FastEthernet0/2  sw2
00:A9:0C:4F:55:50  10.1.3.1    10          FastEthernet0/1  sw4
```

Теперь данные добавились без ошибки.

Проблема в том, что при включении PRAGMA foreign_keys строки нарушающие условие не удаляются:
```sql
sqlite> PRAGMA foreign_keys = ON;

sqlite> select * from dhcp;
mac                ip          vlan        interface        switch
-----------------  ----------  ----------  ---------------  ----------
00:09:BB:3D:D6:58  10.1.10.2   10          FastEthernet0/1  sw1
00:04:A3:3E:5B:69  10.1.5.2    5           FastEthernet0/1  sw1
00:05:B3:7E:9B:60  10.1.5.4    5           FastEthernet0/9  sw1
00:07:BC:3F:A6:50  10.1.10.6   10          FastEthernet0/3  sw1
00:09:BC:3F:A6:50  192.168.10  1           FastEthernet0/7  sw1
00:E9:BC:3F:A6:50  100.1.1.6   3           FastEthernet0/2  sw3
00:A9:BB:3D:D6:58  10.1.10.20  10          FastEthernet0/7  sw2
00:B4:A3:3E:5B:69  10.1.5.20   5           FastEthernet0/5  sw2
00:C5:B3:7E:9B:60  10.1.5.40   5           FastEthernet0/9  sw2
00:A9:BC:3F:A6:50  10.1.10.60  20          FastEthernet0/2  sw2
00:A9:0C:4F:55:50  10.1.3.1    10          FastEthernet0/1  sw4
```

Но достаточно легко найти такие строки:
```sql
sqlite> select * from dhcp where switch not in (select hostname from switches);
mac             ip          vlan        interface         switch
--------------  ----------  ----------  ----------------  ----------
00:A9:0C:4F:55:50  10.1.3.1    10          FastEthernet0/1  sw4
```

А затем, если необходимо, удалить:
```sql
sqlite> delete from dhcp where switch not in (select hostname from switches);
sqlite> select * from dhcp;
mac                ip          vlan        interface        switch
-----------------  ----------  ----------  ---------------  ----------
00:09:BB:3D:D6:58  10.1.10.2   10          FastEthernet0/1  sw1
00:04:A3:3E:5B:69  10.1.5.2    5           FastEthernet0/1  sw1
00:05:B3:7E:9B:60  10.1.5.4    5           FastEthernet0/9  sw1
00:07:BC:3F:A6:50  10.1.10.6   10          FastEthernet0/3  sw1
00:09:BC:3F:A6:50  192.168.10  1           FastEthernet0/7  sw1
00:E9:BC:3F:A6:50  100.1.1.6   3           FastEthernet0/2  sw3
00:A9:BB:3D:D6:58  10.1.10.20  10          FastEthernet0/7  sw2
00:B4:A3:3E:5B:69  10.1.5.20   5           FastEthernet0/5  sw2
00:C5:B3:7E:9B:60  10.1.5.40   5           FastEthernet0/9  sw2
00:A9:BC:3F:A6:50  10.1.10.60  20          FastEthernet0/2  sw2
```

### ON DELETE, ON UPDATE


