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

В заданиях 11 раздела создает БД в которой есть две таблицы: dhcp и switches.

Таблица dhcp (показана часть записей):

| mac | ip  | vlan  | interface | switch |
|:---:|:---:|:-----:|:---------:|:------:|
|00:07:BC:3F:A6:50 |10.1.10.6  |10  |FastEthernet0/3 |sw1|
|00:09:BC:3F:A6:50 |192.168.10 |1   |FastEthernet0/7 |sw1|
|00:A9:BB:3D:D6:58 |10.1.10.20 |10  |FastEthernet0/7 |sw2|
|00:B4:A3:3E:5B:69 |10.1.5.20  |5   |FastEthernet0/5 |sw2|
|00:E9:BC:3F:A6:50 |100.1.1.6  |3   |FastEthernet0/2 |sw3|


Таблица switch:

|hostname |   location |
|:-------:|:-------------------------:|
|sw1     | London, 21 New Globe Walk|
|sw2     | London, 21 New Globe Walk|
|sw3     | London, 21 New Globe Walk|


В заданиях к 11 разделу в определении таблицы встречается такая строка:
```
    switch       text not null references switches(hostname)
```

Полная версия команд создания таблиц:
```
create table switches (
    hostname    text primary key,
    location    text
);

create table dhcp (
    mac          text primary key,
    ip           text,
    vlan         text,
    interface    text,
    switch       text not null references switches(hostname)
);
```

Эта запись создает внешний ключ (foreign key) - 

Файл dhcp_snooping_schema.sql:
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


```sql
sqlite> select * from switches;
hostname    location
----------  -------------------------
sw1         London, 21 New Globe Walk
sw2         London, 21 New Globe Walk
sw3         London, 21 New Globe Walk
```


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


```sql
sqlite> PRAGMA foreign_keys = ON;

sqlite> INSERT into dhcp
   ...> values ('0010.A1AA.C1CC', '10.1.3.1', '10', 'FastEthernet0/19', 'sw4');
Error: FOREIGN KEY constraint failed
```



```sql
sqlite> PRAGMA foreign_keys = OFF;

sqlite> INSERT into dhcp
   ...> values ('0010.A1AA.C1CC', '10.1.3.1', '10', 'FastEthernet0/19', 'sw4');

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
0010.A1AA.C1CC     10.1.3.1    10          FastEthernet0/1  sw4
```


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
0010.A1AA.C1CC     10.1.3.1    10          FastEthernet0/1  sw4
```


Но достаточно легко найти такие строки:
```sql
sqlite> select * from dhcp where switch not in (select hostname from switches);
mac             ip          vlan        interface         switch
--------------  ----------  ----------  ----------------  ----------
0010.A1AA.C1CC  10.1.3.1    10          FastEthernet0/19  sw4
```

А затем удалить:
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


