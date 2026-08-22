# ru-blocklist-aggregator

🇬🇧 English • [🇷🇺 Русский](README.md)

![License](https://img.shields.io/github/license/AbbeyLubber/ru-blocklist-aggregator)
![Last Commit](https://img.shields.io/github/last-commit/AbbeyLubber/ru-blocklist-aggregator)

Unified Russian blocklist aggregated from multiple community sources, plus an up-to-date list of Telegram's IP ranges. Updated automatically.

## About

Several actively maintained projects track domains blocked in Russia, each in its own format and on its own update cycle. This repo merges them into clean, deduplicated lists — a single source of truth you can point your DNS filter, proxy, or router at instead of juggling multiple upstreams. It also separately publishes Telegram's current IP subnets from their official source.

This repo also maintains `corp/` — a separate set of domain and IP-range lists for major Russian services (Yandex, VK, Sberbank, and others) meant for routing their traffic as RU-domestic. That's a trust list, not a blocklist — full details, methodology, and file table are in [corp/README.en.md](corp/README.en.md).

## Domain sources

| Source | What it provides |
|---|---|
| [Nidelon/ru-block-v2ray-rules](https://github.com/Nidelon/ru-block-v2ray-rules) | Blocked-domain rules for Xray/V2Ray routing |
| [savely-krasovsky/antizapret-sing-box](https://github.com/savely-krasovsky/antizapret-sing-box) | Domain lists generated from Antizapret |
| [runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) | Combined RKN + community + re:filter blocklist |
| [Noktomezo/RussiaFancyLists](https://github.com/Noktomezo/RussiaFancyLists/blob/main/lists/blacklist/domains/full.lst) (`full.lst`, `full-sld.lst`) | Curated, auto-updating domain blocklist |

## Files

| File / folder | Contents |
|---|---|
| `blocked/rkn-domain.txt` | Domains, one per line, no wildcards — maximum compatibility (hosts files, MikroTik `match-subdomain=yes`, exact-match blockers) |
| `blocked/rkn-with-wildcard.txt` | Same domains, with a `*.` prefix where a source indicates subdomain blocking — for AdGuard Home, sing-box, and other wildcard-aware tools |
| `blocked/ipv4.txt` | IPv4 subnets blocked in Russia |
| `blocked/ipv6.txt` | IPv6 subnets blocked in Russia (if a current source exists for this release - see status table) |
| `Telegram/telegram-ipv4.txt` | Telegram's current IPv4 subnets, from the official CIDR source |
| `Telegram/telegram-ipv6.txt` | Telegram's current IPv6 subnets, from the official CIDR source |
| [`corp/`](corp/README.en.md) | Domains and IP ranges for major Russian services (Yandex, VK, Mail Group, Sberbank, OZON, Wildberries, Avito, banks) — a trust list, not a blocklist. Full folder descriptions and file table: [corp/README.en.md](corp/README.en.md) |

## List status

The table below is regenerated automatically on every publish — do not edit by hand. `corp/` file status lives in its own table in [corp/README.en.md](corp/README.en.md), to keep this one short.

<!-- STATUS-TABLE:START -->
_Last checked by automation: 2026-08-22 17:39 UTC_

| File | Updated | Lines | MD5 |
|---|---|---|---|
| `Telegram/telegram-ipv4.txt` | 2026-08-11 12:10 UTC | 9 | `1fd618d8fde9205840fe6be10f90d66c` |
| `Telegram/telegram-ipv6.txt` | 2026-08-11 12:10 UTC | 5 | `b40d044727025c645af8e507265b94e9` |
| `blocked/rkn-domain.txt` | 2026-08-11 13:11 UTC | 1642507 | `f9669b97b0441e1f710ae51ad440244a` |
| `blocked/rkn-with-wildcard.txt` | 2026-08-11 13:11 UTC | 3262892 | `41b4143479bfbf7045f5e90a98611bbc` |
| `blocked/ipv4.txt` | 2026-08-21 20:58 UTC | 55918 | `cfa68f9cd3de50597a599042b4e6830a` |
| `blocked/ipv6.txt` | 2026-08-21 20:58 UTC | 3050 | `2636f2259a49b7b6fc39c19ff52c9fc7` |
<!-- STATUS-TABLE:END -->

## Update schedule

The Telegram lists (`Telegram/telegram-ipv4.txt`, `Telegram/telegram-ipv6.txt`) are refreshed **every 12 hours** straight from the official source. Domain lists (`blocked/rkn-domain.txt`, `blocked/rkn-with-wildcard.txt`) are refreshed **weekly**: sources are re-fetched, normalized to a single format, merged, and deduplicated — domains are only ever added, never removed even if a source drops them. Exact last-update time per file is in the table above. `corp/`'s schedule is documented in [corp/README.en.md](corp/README.en.md).

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
