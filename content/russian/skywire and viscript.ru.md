+++
title = "Skywire and Viscript"
tags = [
    "Development",
    "Skywire",
]
bounty = 3
date = "2017-08-15"
image = "img/old-messenger.png"
aliases = [
	"/ru/skywire/skywire-and-viscript/"
]
+++
## Введение

### Viscript

[Viscript](https://github.com/skycoin/viscript) это кроссплатформенный CLI, а также лаунчер для приложений и панель управления кластерами. Он основан на библиотеке сигналов в качестве сигнального сервера, поэтому может управлять сигнальными клиентами, такими как узел (нода) и компоненты в Skywire. Он может быть запущен либо в режиме графического интерфейса (GUI), либо в безголовом режиме (headless mode).

#### Скриншот Viscript GUI:

![screenshot](/img/viscript.jpg)

Мы можем добавить конфигурацию приложения в файл config.yaml, как meshnet-socks-server:

```
  meshnet-socks-server:
    daemon: true
    desc: DESCRIPTION GOES HERE
    path: bin/meshnet/meshnet-run-socks-server
    default_args: []
    help: |
        [1] Текстовое наименование приложения (должно быть уникальным).
        [2] Адрес узла, с которым приложение будет связываться. ex 101.202.34.56:9000
        [3] Порт, который SOCKS сервер будет использовать для соединения с целевым хостом. ex 8000

        Полный пример команды:
            start meshnet-socks-server sockssrv0 101.202.34.56:9000 8001
```

После перезапуска viscript с помощью командных приложений мы сможем проверить приложения, которые можно запустить посредством viscript.

На скриншоте видно, что мы можем запустить приложение, используя короткую команду `s` (`s apptracker 127.0.0.1:20000`) .

Затем viscript запускает его с уникальным последовательно возрастающим идентификатором (ID) последовательности: мы можем использовать ping (`ping`), проверять
испоьзование ресурсов (`ru`) и выключать (`sd`) с помощью этого ID.

### Skywire

[Skywire](https://github.com/skycoin/skywire) это одноранговая (peer-to-peer) альтернативная сеть, которая забирает контроль у интернет-провайдеров и возвращает его пользователям. Также в нём присутствует несколько компонентов: Узловой Менеджер, Узел и приложения, запущенные в mesh сети, например, VPN клиент, VPN сервер, SOCKS клиент, SOCKS сервер.

Все компоненты внутри Skywire основаны на библиотеке сигналов в качестве сигнального клиента. Таким образом, они могут запускаться, управляться и завершаться посредством viscript.

## Архитектура

#### Архитектурная схема:

------

```
                                   +-----------+-------------+
           +---------------^-----+ |     VPN   |    SOCKS    |
           |   управляемый   |     +-----------+-------------+
           |               <-----+ |          Узел           |
           v               |       +-------------------------+
                           <-----+ |     Узловой Менеджер    |
+-------------------+      |       +-------------------------+
|      viscript     |      +-----+ |        Мессенджер       |
+-------------------+--------------+-------------------------+
|                        сигнал                              |
+------------------------------------------------------------+
|                         сеть                               |
+------------------------------------------------------------+
```

------

Для каждой службы есть клиентские и серверные приложения, такие как VPN клиент и VPN сервер. Они запускаются в mesh сети Skywire.
Как мы знаем, Skycoin является валютой Skywire, и когда пользователь перенаправляет трафик или предоставляет сетевые ресурсы, то он/она получает Skycoin. Аналогично, когда пользователь потребляет сетевые ресурсы или медиа, он/она тратит Skycoin. Skywire будет генерировать монеты для работы в сети после внедрения измерений и расчетов.

Узел, Узловой Менеджер и Мессенджер являются ключевыми компонентами mesh сети Skywire. Узел представляет собой ноду одноранговой mesh сети. Сервисные приложения будут регистрироваться в Узле, и их трафик будет перенаправлен этим Узлом. Узловой Менеджер управляет маршрутами между узлами в mesh сети. Мессенджер позволяет пользователям группировать кластеры с помощью открытого ключа. Все эти компоненты являются краеугольными камнями mesh сети Skywire.

## Итог

Viscript и Skywire всё ещё находятся в интенсивной разработке. Но мы достигли прекрасных результатов в экосистеме Skycoin. Мы получаем удовольствие от разработки и собираемся раскрыть весь потенциал бесплатного интернета в будущем!