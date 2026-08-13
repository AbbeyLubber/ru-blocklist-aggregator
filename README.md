# ru-blocklist-aggregator

[🇬🇧 English](README.en.md) • 🇷🇺 Русский

![License](https://img.shields.io/github/license/AbbeyLubber/ru-blocklist-aggregator)
![Last Commit](https://img.shields.io/github/last-commit/AbbeyLubber/ru-blocklist-aggregator)

Единый список заблокированных в России доменов, собранный из нескольких источников, плюс актуальный список IP-подсетей Telegram. Обновляется автоматически.

## О проекте

Несколько активно поддерживаемых проектов ведут собственные списки заблокированных в России доменов — каждый в своём формате и со своим циклом обновления. Этот репозиторий объединяет их в чистые списки без дублей — единый источник, на который можно настроить DNS-фильтр, прокси или роутер, вместо того чтобы следить за несколькими источниками по отдельности. Отдельно публикуется актуальный список IP-подсетей Telegram из официального источника.

Репозиторий также ведёт `corp/` — отдельный набор списков доменов и IP-диапазонов крупных российских сервисов (Яндекс, VK, Сбер и другие) для маршрутизации их трафика как RU-домашнего. Это список доверия, а не блок-лист — подробности, методология и таблица файлов в [corp/README.md](corp/README.md).

## Источники доменов

| Источник | Что предоставляет |
|---|---|
| [Nidelon/ru-block-v2ray-rules](https://github.com/Nidelon/ru-block-v2ray-rules) | Правила блокировки доменов для маршрутизации в Xray/V2Ray |
| [savely-krasovsky/antizapret-sing-box](https://github.com/savely-krasovsky/antizapret-sing-box) | Списки доменов на основе Antizapret |
| [runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) | Объединённый список РКН + community + re:filter |
| [Noktomezo/RussiaFancyLists](https://github.com/Noktomezo/RussiaFancyLists/blob/main/lists/blacklist/domains/full.lst) (`full.lst`, `full-sld.lst`) | Курируемый, автообновляемый список доменов |

## Файлы

| Файл / папка | Содержимое |
|---|---|
| `blocked/rkn-domain.txt` | Домены, по одному на строку, без wildcard-масок — максимальная совместимость (hosts-файлы, MikroTik `match-subdomain=yes`, exact-match блокировщики) |
| `blocked/rkn-with-wildcard.txt` | Те же домены, с префиксом `*.` там, где источник указывает на блокировку поддоменов — для AdGuard Home, sing-box и других инструментов с поддержкой wildcard |
| `blocked/ipv4.txt` | Заблокированные в России IPv4-подсети |
| `blocked/ipv6.txt` | Заблокированные в России IPv6-подсети (если для данного релиза есть актуальный источник — см. таблицу статуса) |
| `Telegram/telegram-ipv4.txt` | Актуальные IPv4-подсети Telegram из официального источника CIDR |
| `Telegram/telegram-ipv6.txt` | Актуальные IPv6-подсети Telegram из официального источника CIDR |
| [`corp/`](corp/README.md) | Домены и IP-диапазоны крупных российских сервисов (Яндекс, VK, Mail Group, Сбер, OZON, Wildberries, Avito, банки) — список доверия, не блок-лист. Полное описание папок и таблица файлов: [corp/README.md](corp/README.md) |

## Статус списков

Таблица ниже обновляется автоматически при каждой публикации — вручную не редактировать. Статус файлов `corp/` — в [corp/README.md](corp/README.md), отдельной таблицей, чтобы не захламлять эту.

<!-- STATUS-TABLE:START -->
_Последняя проверка автоматикой: 2026-08-13 03:18 UTC_

| Файл | Обновлено | Строк | MD5 |
|---|---|---|---|
| `Telegram/telegram-ipv4.txt` | 2026-08-11 12:10 UTC | 9 | `1fd618d8fde9205840fe6be10f90d66c` |
| `Telegram/telegram-ipv6.txt` | 2026-08-11 12:10 UTC | 5 | `b40d044727025c645af8e507265b94e9` |
| `blocked/rkn-domain.txt` | 2026-08-11 13:11 UTC | 1642507 | `f9669b97b0441e1f710ae51ad440244a` |
| `blocked/rkn-with-wildcard.txt` | 2026-08-11 13:11 UTC | 3262892 | `41b4143479bfbf7045f5e90a98611bbc` |
| `blocked/ipv4.txt` | 2026-08-13 03:18 UTC | 55080 | `f10c9eced2fb0979bffbf6534d4e0ae1` |
| `blocked/ipv6.txt` | 2026-08-11 20:13 UTC | 2971 | `49556c9297c3b3cc251bc66764a90071` |
<!-- STATUS-TABLE:END -->

## Расписание обновлений

Список Telegram (`Telegram/telegram-ipv4.txt`, `Telegram/telegram-ipv6.txt`) обновляется **каждые 12 часов** напрямую из официального источника. Списки доменов (`blocked/rkn-domain.txt`, `blocked/rkn-with-wildcard.txt`) обновляются **еженедельно**: источники скачиваются заново, приводятся к единому формату, объединяются и очищаются от дублей — из списка домены только добавляются, старые записи не удаляются даже если источник их убрал. Точное время последнего обновления каждого файла — в таблице выше. Расписание `corp/` — в [corp/README.md](corp/README.md).

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
