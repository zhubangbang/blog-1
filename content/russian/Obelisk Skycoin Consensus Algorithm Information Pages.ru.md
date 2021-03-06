+++
title = "Obelisk: Алгоритм консенсуса Skycoin |Информация"
tags = [
    "Consensus",
    "Obelisk",
]
date = "2017-09-09"
author = "johnstuartmill"
aliases = [
	"/ru/overview/obelisk-skycoin-consensus-algorithm-information-pages/"
]
+++

- [Важное о консенсусах](#[Важное-о-консенсусах)
    - [Почему консенсус?](#Почему-консенсус)
    - [Высокая масштабируемость и низкое энергопотребление](#Высокая-масштабируемость-и-низкое-энергопотребление)
    - [Устойчивость к скоординированным атакам](#Устойчивость-к-скоординированным-атакам)
    - [“Атака 51 процент”](#%E2%80%9CАтака-51-процент%E2%80%9D)
    - [Скрытые IP адреса](#Скрытые-IP-адреса)
    - [Независимость в синхронизации часов](#Независимость-в-синхронизации-часов)
    - [Два типа узлов: консенсуса и создания блоков](#Два-типа-узлов-консенсуса-и-создания-блоков)
- [Как работает алгоритм консенсуса Skycoin](#Как-работает-алгоритм-консенсуса-Skycoin)
- [Ссылки](#Ссылки)

## Важное о консенсусах

### Почему консенсус?

Алгоритм консенсуса Skycoin (называемый «Obelisk») синхронизирует состояние
блокчейна Skycoin во всех узлах сети. Это приводит к согласованному учету,
то есть при вычислении баланса результат, который получает каждый из узлов
для конкретного открытого ключа (или адреса), всегда одинаков.

### Высокая масштабируемость и низкое энергопотребление

По своей конструкции алгоритм представляет собой масштабируемую и
не требующую больших вычислительных мощностей альтернативу алгоритму
proof-of-work, поэтому как работа алгоритм консенсуса, так и действия
по созданию блоков могут выполняться на бюджетном оборудовании, которое
имеет невысокую цену и низкое потребление энергии, что делает криптовалютную
сеть более надежной для возможных попыток централизации (т. е. узлы будут
доступными для широкой публики).

### Устойчивость к скоординированным атакам

Наш алгоритм консенсуса (1) сходится быстро, (2) требует минимального
сетевого трафика и (3) может противостоять крупномасштабной
скоординированной атаке хорошо организованной сети вредоносных узлов.
Алгоритм не итеративный, быстрый, может быть запущен в разреженной сети
при наличии связи только с ближайшим соседом (например, в ячеистой сети)
и хорошо работает при наличии в подключении циклических графов (то есть
подключение
[DAG-типа](https://ru.wikipedia.org/wiki/Направленный_ациклический_граф)
не требуется).

### “Атака 51 процент”

При определенных условиях базовая версия алгоритма может быть подвержена
этой атаке. В частности, когда модифицированные или злонамеренные узлы
находятся в большинстве и транслируют протокол-совместимый и UTXO-
совместимый блок-кандидат, такой блок выиграет консенсус.
Однако блок с любым видом несоответсвия отбрасывается
(не модифицированным) алгоритмом прежде, чем блок получит шанс
участвовать в консенсусном соревновании.

Узлы консенсуса могут опционально использовать концепцию «Web-of-Trust»,
при этом связанные с консенсусом сообщения, поступающие от неизвестных
узлов (т. е. подписанных ненадежными открытыми ключами), игнорируются.

Когда включен режим Web-of-Trust, запуск очень большого количества узлов
злонамеренного консенсуса для того, чтобы (a) вызвать форк блокчейна или
(б) нарушить процесс консенсуса, будет иметь незначительный эффект, если
только подавляющее большинство участников Web-of-Trust невольно
не включают эти вредоносные узлы в свои локальные списки доверенных узлов.

### Скрытые IP адреса

Узлы адресуются через их криптографический открытый ключ.
IP-адрес узла известен только тем узлам, к которым он подключен напрямую.


### Независимость в синхронизации часов

Алгоритм не использует «настенные часы» (то есть календарную дату/время).
Вместо этого для вычисления внутреннего времени узла используются номера
блоков, которые извлекаются из проверенных сообщений, связанных с
консенсусом и блокчейном.
Это можно неофициально назвать «часы блока».

### Два типа узлов: консенсуса и создания блоков

Консенсусный узел получает данные  от одного или нескольких узлов,
создающих блоки. Алгоритмы для консенсуса и создания блоков разные,
но оба они оперируют одними и теми же структурами данных.
Мы отдельно упоминаем о создании блоков, так как это поможет понять
алгоритм консенсуса и то, как он интегрируется с остальной системой.

Оба типа узлов всегда производят авторизацию и проверку фальсифиции даты.
Мошеннические или недействительные сообщения выявляются, отбрасываются и
далее не передаются; узлы одного ранга, участвующие в подозрительных
действиях, отключаются, а их открытые ключи попадают в бан.

## Как работает алгоритм консенсуса Skycoin

Для упрощения пояснений предположим:  (1) каждый узел одновременно
участвует и создании блоков, и в консенсусе,
и (2) принимаются генерируемые ненадежными узлами сообщения,
связанные с консенсусом, то есть никакая фильтрация на основе Web-of-Trust
не выполняется. Полная реализация (т. е. без этих упрощающих предположений)
будет доступна на GitHub проекта Skycoin.
Результаты моделирования и подробный, схематический пример одного
консенсусного исследования см. [\[1\]](#ссылки).
Моделирование сети с доверительными отношениями, хотя и с использованием
алгоритма, отличного от Skycoin, можно найти в [\[2\]](#ссылки).
Вот описание алгоритма консенсуса Skycoin:

1.  *Создание блоков*. Каждый блок-узел собирает новые транзакции,
    проверяет их против UTXO (Unspent Transaction Output - "список"
    непотраченных транзакций), упаковывает совместимые транзакции
    в новый блок и транслирует блок в сеть.

2.  *Сбор блоков*.  Каждый консенсусный узел собирает блоки,
    сгенерированные узлами-создателями блоков и помещает, указав
    последовательный номер блока, в контейнер (отдельно от блокчейна).

3.  *Выбор выигрышного блока*. Каждый консенсусный узел, получив
     достаточно большое количество [*1] блоков-кандидатов или при
     выполнении других критериев, находит блок, созданный наибольшим
     числом узлов-созидателей.
     Связи решаются [детерминистически](https://ru.wikipedia.org/wiki/Детерминированность).
Такой блок помечается как «локальный победитель» [*2] и добавляется
к локальному блокчейну. Пара ключ-значение, соответствующая
 номеру локального победителя, удаляется из контейнера, таким
     образом освобождается хранилище. Хеш-код местного победителя
     транслируется/объявляется.

4.  *Шаг верификации*. Каждый узел сохраняет статистику по локальным
     победителям, о которых сообщают другие узлы. Когда местные победители
     будут сообщены всеми или большинством узлов [*3], узел определяет
     глобального победителя для текущего порядкового номера. Если глобальным
победителем является локальный победитель, тогда узел продолжает
     действовать по указанной схеме. В противном случае узлы принимают решение,
     основываясь на внешних данных и локальных журналах, или
     (а) провести повторную синхронизацией с сетью
или (б) отказаться от участия в консенсусе и/или создании блока,
или (c) о сохранения блокчейна и запросе экстренной остановки.

[*1]: Это один из конфигурационных параметров алгоритма.

[*2]: В подобных идеальных условиях локальные победители (для присвоения
     текущего порядкового номера блока) одни и те же, то есть включают
     идентичный набор транзакций. Разница возникает из-за латентности сети,
     высокой частоты транзакций, доставки сообщений вне очереди, потери
     сообщения, сбоя в узле или действий вредоносных узлов и т.д.

[*3]: Это число может быть определено, например, путем запроса к доверенным
узлам рекурсивно сообщить открытые ключи их доверенных узлов.


## Ссылки

\[1\] johnstuartmill et al. A Distributed Consensus Algorithm for
Cryptocurrency Networks.
<https://github.com/skycoin/whitepapers/blob/master/whitepaper_skycoin_consensus_v01_jsm.pdf>
2016

\[2\] Houwu Chen and Jiwu Shu. Sky: an Opinion Dynamics Framework and Model
for Consensus over P2P Network.
<https://github.com/skycoin/whitepapers/blob/master/Sky-%20Opinion%20Dynamics%20Based%20Consensus%20for%20P2P%20Network%20with%20Trust%20Relationships.pdf>
201?

*Читайте для подробностей:*

* *[Skycoin Consensus Algorithm Whitepapers](https://www.skycoin.net/whitepapers)*
* *[Obelisk The Skycoin Consensus Algorithm](/statement/obelisk-the-skycoin-consensus-algorithm/)*
