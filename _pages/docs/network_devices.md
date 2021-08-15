---
title: "Сетевое оборудование"
permalink: /docs/network_devices/
excerpt: "Настройка сетевого оборудования"
---

Обратите внимание, что к 10 неделе курса, нужно подготовить виртуальное или реальное сетевое оборудование.
В виртуальных машинах, которые подготовлены для курса, уже установлен и настроен GNS3, а также настроено оборудование.
То есть, при использовании подготовленных виртуальных машин, надо только запустить GNS3 и следовать по пунктам в инструкции виртуальной машины.

Все примеры и задания, в которых встречается сетевое оборудование, используют одинаковое количество устройств: три маршрутизатора с такими базовыми настройками:

* пользователь: cisco
* пароль: cisco
* пароль на режим enable: cisco
* SSH версии 2 (обязательно именно версия 2), Telnet
* IP-адреса маршрутизаторов: 192.168.100.1, 192.168.100.2, 192.168.100.3
* IP-адреса должны быть доступны из виртуалки на которой вы выполняете задания и могут быть назначены на физических/логических/loopback интерфейсах


Если вы не будете использовать подготовленные виртуалки, лучше подготовить оборудование заранее, так как во время курса у вас будет мало времени.

## Другие параметры подключения

Если вы не используете подготовленные виртуалки и параметры подключения к оборудованию другие, надо изменить файл
devices.yaml в соответствующем разделе заданий и писать там свои параметры подключения.
При этом в файле должно быть как минимум 3 устройства.

> Тесты берут параметры подключения именно из файла devices.yaml.

## Топология

Топология может быть произвольной. Пример топологии в подготовленной VM:

![gns3](https://raw.githubusercontent.com/pyneng/pyneng.github.io/master/assets/images/gns3_network.png)

## Конфигурация

Базовый конфиг:
```
hostname R1
!
no ip domain lookup
ip domain name pyneng
!
crypto key generate rsa modulus 1024
ip ssh version 2
!
username cisco password cisco
enable secret cisco
!
line vty 0 4
 logging synchronous
 login local
 transport input telnet ssh
```

На каком-то интерфейсе надо настроить IP-адрес
```
interface ...
 ip address 192.168.100.1 255.255.255.0
```

Алиасы (по желанию)
```
!
alias configure sh do sh
alias exec ospf sh run | s ^router ospf
alias exec bri show ip int bri | exc unass
alias exec id show int desc
alias exec top sh proc cpu sorted | excl 0.00%__0.00%__0.00%
alias exec c conf t
alias exec diff sh archive config differences nvram:startup-config system:running-config
alias exec desc sh int desc | ex down
alias exec bgp sh run | s ^router bgp
```

При желании можно настроить [EEM applet](http://xgu.ru/wiki/Embedded_Event_Manager) для вывода команд, которые вводит пользователь:
```
!
event manager applet COMM_ACC
 event cli pattern ".*" sync no skip no occurs 1
 action 1 syslog msg "User $_cli_username entered $_cli_msg on device $_cli_host "
!
```
