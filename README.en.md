# ru-blocklist-aggregator

🇬🇧 English • [🇷🇺 Русский](README.md)

![License](https://img.shields.io/github/license/AbbeyLubber/ru-blocklist-aggregator)
![Last Commit](https://img.shields.io/github/last-commit/AbbeyLubber/ru-blocklist-aggregator)

Unified Russian blocklist aggregated from multiple community sources, plus an up-to-date list of Telegram's IP ranges. Updated automatically.

## About

Several actively maintained projects track domains blocked in Russia, each in its own format and on its own update cycle. This repo merges them into clean, deduplicated lists — a single source of truth you can point your DNS filter, proxy, or router at instead of juggling multiple upstreams. It also separately publishes Telegram's current IP subnets from their official source.

## Domain sources

| Source | What it provides |
|---|---|
| [Nidelon/ru-block-v2ray-rules](https://github.com/Nidelon/ru-block-v2ray-rules) | Blocked-domain rules for Xray/V2Ray routing |
| [savely-krasovsky/antizapret-sing-box](https://github.com/savely-krasovsky/antizapret-sing-box) | Domain lists generated from Antizapret |
| [runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) | Combined RKN + community + re:filter blocklist |
| [Noktomezo/RussiaFancyLists](https://github.com/Noktomezo/RussiaFancyLists/blob/main/lists/blacklist/domains/full.lst) (`full.lst`) | Curated, auto-updating domain blocklist |

## Files

| File | Contents |
|---|---|
| `blocked/rkn-domain.txt` | Domains, one per line, no wildcards — maximum compatibility (hosts files, MikroTik `match-subdomain=yes`, exact-match blockers) |
| `blocked/rkn-with-wildcard.txt` | Same domains, with a `*.` prefix where a source indicates subdomain blocking — for AdGuard Home, sing-box, and other wildcard-aware tools |
| `blocked/ipv4.txt` | IPv4 subnets blocked in Russia |
| `blocked/ipv6.txt` | IPv6 subnets blocked in Russia (if a current source exists for this release - see status table) |
| `Telegram/telegram-ipv4.txt` | Telegram's current IPv4 subnets, from the official CIDR source |
| `Telegram/telegram-ipv6.txt` | Telegram's current IPv6 subnets, from the official CIDR source |
| `corp/*/…` | Domains and IP ranges for major Russian services (Yandex, VK, Mail Group, Sberbank, OZON, Wildberries, Avito, the banking sector) — in progress |

## List status

The table below is regenerated automatically on every publish — do not edit by hand.

<!-- STATUS-TABLE:START -->
_Last checked by automation: 2026-08-11 15:06 UTC_

| File | Updated | Lines | MD5 |
|---|---|---|---|
| `Telegram/telegram-ipv4.txt` | 2026-08-11 12:10 UTC | 9 | `1fd618d8fde9205840fe6be10f90d66c` |
| `Telegram/telegram-ipv6.txt` | 2026-08-11 12:10 UTC | 5 | `b40d044727025c645af8e507265b94e9` |
| `blocked/rkn-domain.txt` | 2026-08-11 13:11 UTC | 1642507 | `f9669b97b0441e1f710ae51ad440244a` |
| `blocked/rkn-with-wildcard.txt` | 2026-08-11 13:11 UTC | 3262892 | `41b4143479bfbf7045f5e90a98611bbc` |
| `blocked/ipv4.txt` | not published yet | — | — |
| `blocked/ipv6.txt` | not published yet | — | — |
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
| `corp/banks/bank-domain.txt` | not published yet | — | — |
| `corp/banks/bank-ipv4.txt` | not published yet | — | — |
| `corp/banks/bank-ipv6.txt` | not published yet | — | — |
<!-- STATUS-TABLE:END -->

## Update schedule

The Telegram lists (`Telegram/telegram-ipv4.txt`, `Telegram/telegram-ipv6.txt`) are refreshed **every 12 hours** straight from the official source. Domain lists (`blocked/rkn-domain.txt`, `blocked/rkn-with-wildcard.txt`) are refreshed **weekly**: sources are re-fetched, normalized to a single format, merged, and deduplicated — domains are only ever added, never removed even if a source drops them. Exact last-update time per file is in the table above.

## Format

**Domains** — plain text, one per line, no comments. In `rkn-with-wildcard.txt`, some lines start with `*.`.

```
example.com
*.another-domain.ru
```

**IP (Telegram, blocked/ipv4.txt, blocked/ipv6.txt)** — CIDR notation, one range per line, IPv4 and IPv6 in separate files.

```
91.108.56.0/22
2001:b28:f23d::/48
```

## Usage

**AdGuard Home / Pi-hole** — add as a custom blocklist source:
```
https://raw.githubusercontent.com/AbbeyLubber/ru-blocklist-aggregator/main/blocked/rkn-with-wildcard.txt
```

**hosts file** — use `blocked/rkn-domain.txt`, prepend each line with `0.0.0.0` or `127.0.0.1`.

**Xray / sing-box / v2ray** — use `blocked/rkn-with-wildcard.txt` as a domain-matcher source, `Telegram/telegram-ipv4.txt` / `Telegram/telegram-ipv6.txt` for a separate IP-based rule (e.g. routing Telegram traffic directly, bypassing the proxy).

**MikroTik (RouterOS v7)** — build a DNS-based address-list from `blocked/rkn-domain.txt`; subdomains via `match-subdomain=yes` on the rule, no wildcard needed in the string itself.

## Disclaimer

This repository aggregates already-public data from open sources for informational and research purposes. It does not provide circumvention tools, proxies, or VPN services — only reference lists of domains and IP addresses.

This project is not affiliated with any of the listed sources and cannot guarantee the accuracy, completeness, or timeliness of their data. Materials are provided "as is," without warranties of any kind, express or implied.

How and for what purpose these lists are used is the sole decision and responsibility of the user, including compliance with the laws of their jurisdiction.

## License

Released under [AGPL-3.0](LICENSE).
