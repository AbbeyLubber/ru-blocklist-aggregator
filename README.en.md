# ru-blocklist-aggregator

🇬🇧 English • [🇷🇺 Русский](README.md)

![License](https://img.shields.io/github/license/AbbeyLubber/ru-blocklist-aggregator)
![Last Commit](https://img.shields.io/github/last-commit/AbbeyLubber/ru-blocklist-aggregator)

Unified Russian blocklist aggregated from multiple community sources, plus an up-to-date list of Telegram's IP ranges. Updated weekly.

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
| `blocklist.txt` | Domains, one per line, no wildcards — maximum compatibility (hosts files, MikroTik `match-subdomain=yes`, exact-match blockers) |
| `blocklist-wildcard.txt` | Same domains, with a `*.` prefix where a source indicates subdomain blocking — for AdGuard Home, sing-box, and other wildcard-aware tools |
| `telegram-ipv4.txt` | Telegram's current IPv4 subnets, from the official CIDR source |
| `telegram-ipv6.txt` | Telegram's current IPv6 subnets, from the official CIDR source |

## Update schedule

Domain lists are refreshed **weekly**: sources are re-fetched, normalized to a single format, merged, and deduplicated. The Telegram lists (`telegram-ipv4.txt`, `telegram-ipv6.txt`) are refreshed **daily**. Check the commit history for the latest update time.

## Format

**Domains** — plain text, one per line, no comments. In `blocklist-wildcard.txt`, some lines start with `*.`.

```
example.com
*.another-domain.ru
```

**IP (Telegram)** — CIDR notation, one range per line, IPv4 and IPv6 in separate files.

```
91.108.56.0/22
2001:b28:f23d::/48
```

## Usage

**AdGuard Home / Pi-hole** — add as a custom blocklist source:
```
https://raw.githubusercontent.com/AbbeyLubber/ru-blocklist-aggregator/main/blocklist-wildcard.txt
```

**hosts file** — use `blocklist.txt`, prepend each line with `0.0.0.0` or `127.0.0.1`.

**Xray / sing-box / v2ray** — use `blocklist-wildcard.txt` as a domain-matcher source, `telegram-ipv4.txt` / `telegram-ipv6.txt` for a separate IP-based rule (e.g. routing Telegram traffic directly, bypassing the proxy).

**MikroTik (RouterOS v7)** — build a DNS-based address-list from `blocklist.txt`; subdomains via `match-subdomain=yes` on the rule, no wildcard needed in the string itself.

## Disclaimer

This repository aggregates already-public data from open sources for informational and research purposes. It does not provide circumvention tools, proxies, or VPN services — only reference lists of domains and IP addresses.

This project is not affiliated with any of the listed sources and cannot guarantee the accuracy, completeness, or timeliness of their data. Materials are provided "as is," without warranties of any kind, express or implied.

How and for what purpose these lists are used is the sole decision and responsibility of the user, including compliance with the laws of their jurisdiction.

## License

Released under [AGPL-3.0](LICENSE).
