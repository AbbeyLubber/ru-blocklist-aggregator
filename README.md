# ru-blocklist-aggregator

[🇬🇧 English](README.en.md) • 🇷🇺 Русский

![License](https://img.shields.io/github/license/AbbeyLubber/ru-blocklist-aggregator)
![Last Commit](https://img.shields.io/github/last-commit/AbbeyLubber/ru-blocklist-aggregator)

Единый список заблокированных в России доменов, собранный из нескольких источников, плюс актуальный список IP-подсетей Telegram. Обновляется автоматически.

## О проекте

Несколько активно поддерживаемых проектов ведут собственные списки заблокированных в России доменов — каждый в своём формате и со своим циклом обновления. Этот репозиторий объединяет их в чистые списки без дублей — единый источник, на который можно настроить DNS-фильтр, прокси или роутер, вместо того чтобы следить за несколькими источниками по отдельности. Отдельно публикуется актуальный список IP-подсетей Telegram из официального источника.

## Источники доменов

| Источник | Что предоставляет |
|---|---|
| [Nidelon/ru-block-v2ray-rules](https://github.com/Nidelon/ru-block-v2ray-rules) | Правила блокировки доменов для маршрутизации в Xray/V2Ray |
| [savely-krasovsky/antizapret-sing-box](https://github.com/savely-krasovsky/antizapret-sing-box) | Списки доменов на основе Antizapret |
| [runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) | Объединённый список РКН + community + re:filter |
| [Noktomezo/RussiaFancyLists](https://github.com/Noktomezo/RussiaFancyLists/blob/main/lists/blacklist/domains/full.lst) (`full.lst`) | Курируемый, автообновляемый список доменов |

## Файлы

| Файл | Содержимое |
|---|---|
| `blocked/rkn-domain.txt` | Домены, по одному на строку, без wildcard-масок — максимальная совместимость (hosts-файлы, MikroTik `match-subdomain=yes`, exact-match блокировщики) |
| `blocked/rkn-with-wildcard.txt` | Те же домены, с префиксом `*.` там, где источник указывает на блокировку поддоменов — для AdGuard Home, sing-box и других инструментов с поддержкой wildcard |
| `blocked/ipv4.txt` | Заблокированные в России IPv4-подсети |
| `blocked/ipv6.txt` | Заблокированные в России IPv6-подсети (если для данного релиза есть актуальный источник — см. таблицу статуса) |
| `Telegram/telegram-ipv4.txt` | Актуальные IPv4-подсети Telegram из официального источника CIDR |
| `Telegram/telegram-ipv6.txt` | Актуальные IPv6-подсети Telegram из официального источника CIDR |
| `corp/*/…` | Домены и IP-диапазоны крупных российских сервисов (Яндекс, VK, Mail Group, Сбер, OZON, Wildberries, Avito, банковский сектор) — в разработке |

## Статус списков

Таблица ниже обновляется автоматически при каждой публикации — вручную не редактировать.

<!-- STATUS-TABLE:START -->
_Последняя проверка автоматикой: 2026-08-11 15:06 UTC_

| Файл | Обновлено | Строк | MD5 |
|---|---|---|---|
| `Telegram/telegram-ipv4.txt` | 2026-08-11 12:10 UTC | 9 | `1fd618d8fde9205840fe6be10f90d66c` |
| `Telegram/telegram-ipv6.txt` | 2026-08-11 12:10 UTC | 5 | `b40d044727025c645af8e507265b94e9` |
| `blocked/rkn-domain.txt` | 2026-08-11 13:11 UTC | 1642507 | `f9669b97b0441e1f710ae51ad440244a` |
| `blocked/rkn-with-wildcard.txt` | 2026-08-11 13:11 UTC | 3262892 | `41b4143479bfbf7045f5e90a98611bbc` |
| `blocked/ipv4.txt` | ещё не опубликован | — | — |
| `blocked/ipv6.txt` | ещё не опубликован | — | — |
| `corp/yandex/ya-domain.txt` | 2026-08-11 15:06 UTC | 133 | `5b5885132ce7770c2e25e370366ad712` |
| `corp/yandex/ya-ipv4.txt` | 2026-08-11 15:06 UTC | 122 | `6b06ba960ce6455b3b6f40f985f2a6f9` |
| `corp/yandex/ya-ipv6.txt` | 2026-08-11 15:06 UTC | 30 | `845aaeac1287d0439c6bc25fec1ff7c5` |
| `corp/vk/vk-domain.txt` | 2026-08-11 15:05 UTC | 52 | `b8618fc1530ce8d186ee7ec74809176a` |
| `corp/vk/vk-ipv4.txt` | 2026-08-11 15:05 UTC | 48 | `8a75327702e3264e1bee14d415d95f7e` |
| `corp/vk/vk-ipv6.txt` | 2026-08-11 15:06 UTC | 14 | `60cc0911e9a017c402a59920ed3152d2` |
| `corp/mailgroup/mg-domain.txt` | 2026-08-11 15:05 UTC | 300 | `38ce0639f0c742c69be23f924b657679` |
| `corp/mailgroup/mg-ipv4.txt` | 2026-08-11 15:05 UTC | 109 | `faacdf558fda28a9e9a13e7bb5a0980a` |
| `corp/mailgroup/mg-ipv6.txt` | 2026-08-11 15:05 UTC | 9 | `5c310e7e1dd8ff2026c1778e26074e5f` |
| `corp/sber/sber-domain.txt` | 2026-08-11 15:05 UTC | 101 | `c2d94bc87d09505210d10290bd64af42` |
| `corp/sber/sber-ipv4.txt` | 2026-08-11 15:05 UTC | 37 | `b0c042bc8646a77c719ede3cdc5e844e` |
| `corp/sber/sber-ipv6.txt` | 2026-08-11 15:05 UTC | 1 | `2559126dfbba4263bd5551d697137010` |
| `corp/ozon/ozon-domain.txt` | 2026-08-11 15:05 UTC | 62 | `02b73b445034a78c12872e74b46e97ed` |
| `corp/ozon/ozon-ipv4.txt` | 2026-08-11 15:05 UTC | 9 | `893e6fd94879ee0848a2a34e7639f15b` |
| `corp/ozon/ozon-ipv6.txt` | 2026-08-11 15:05 UTC | 0 | `d41d8cd98f00b204e9800998ecf8427e` |
| `corp/wildberries/wb-domain.txt` | 2026-08-11 15:06 UTC | 114 | `056a2a40b7b26ddd42af6e14a162b486` |
| `corp/wildberries/wb-ipv4.txt` | 2026-08-11 15:06 UTC | 29 | `407f18fd3ac29fb575acad8e301e06d2` |
| `corp/wildberries/wb-ipv6.txt` | 2026-08-11 15:06 UTC | 12 | `5fa643d734b3715d2326ca9315169605` |
| `corp/avito/av-domain.txt` | 2026-08-11 15:05 UTC | 3 | `b47d2fb44183ea8a676ec4f548df4014` |
| `corp/avito/av-ipv4.txt` | 2026-08-11 15:05 UTC | 17 | `c6ae2ebacb4d38a3794f33421bd9f610` |
| `corp/avito/av-ipv6.txt` | 2026-08-11 15:05 UTC | 0 | `d41d8cd98f00b204e9800998ecf8427e` |
| `corp/banks/bank-domain.txt` | ещё не опубликован | — | — |
| `corp/banks/bank-ipv4.txt` | ещё не опубликован | — | — |
| `corp/banks/bank-ipv6.txt` | ещё не опубликован | — | — |
<!-- STATUS-TABLE:END -->

## Расписание обновлений

Список Telegram (`Telegram/telegram-ipv4.txt`, `Telegram/telegram-ipv6.txt`) обновляется **каждые 12 часов** напрямую из официального источника. Списки доменов (`blocked/rkn-domain.txt`, `blocked/rkn-with-wildcard.txt`) обновляются **еженедельно**: источники скачиваются заново, приводятся к единому формату, объединяются и очищаются от дублей — из списка домены только добавляются, старые записи не удаляются даже если источник их убрал. Точное время последнего обновления каждого файла — в таблице выше.

## Формат

**Домены** — обычный текст, один домен на строку, без комментариев. В `rkn-with-wildcard.txt` часть строк начинается с `*.`.

```
example.com
*.another-domain.ru
```

**IP (Telegram, blocked/ipv4.txt, blocked/ipv6.txt)** — CIDR-нотация, один диапазон на строку, IPv4 и IPv6 в отдельных файлах.

```
91.108.56.0/22
2001:b28:f23d::/48
```

## Использование

**AdGuard Home / Pi-hole** — добавь как источник кастомного блок-листа:
```
https://raw.githubusercontent.com/AbbeyLubber/ru-blocklist-aggregator/main/blocked/rkn-with-wildcard.txt
```

**hosts-файл** — используй `blocked/rkn-domain.txt`, добавь `0.0.0.0` или `127.0.0.1` перед каждой строкой.

**Xray / sing-box / v2ray** — `blocked/rkn-with-wildcard.txt` как источник доменного правила маршрутизации, `Telegram/telegram-ipv4.txt` / `Telegram/telegram-ipv6.txt` — отдельным IP-правилом (например, чтобы направлять трафик Telegram напрямую, минуя прокси).

**MikroTik (RouterOS v7)** — DNS-based address-list из `blocked/rkn-domain.txt`; поддомены — через `match-subdomain=yes` в правиле, без wildcard в самой строке.

## Дисклеймер

Этот репозиторий агрегирует уже общедоступные данные из открытых источников в информационных и исследовательских целях. Здесь нет инструментов обхода блокировок, прокси или VPN — только справочные списки доменов и IP-адресов.

Проект не аффилирован ни с одним из перечисленных источников и не может гарантировать точность, полноту или актуальность их данных. Материалы предоставляются «как есть», без каких-либо гарантий, явных или подразумеваемых.

Как и в каких целях использовать эти списки — решение и ответственность самого пользователя, включая соблюдение законодательства своей юрисдикции.

## Лицензия

Распространяется под лицензией [AGPL-3.0](LICENSE).
