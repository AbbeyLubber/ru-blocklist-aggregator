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
| `Telegram/telegram-ipv4.txt` | Telegram IPv4 subnets: the official CIDR list **plus** the CDN networks Telegram's media is hosted on (see the note below the table) |
| `Telegram/telegram-ipv6.txt` | Telegram IPv6 subnets: the official CIDR list **plus** the CDN networks Telegram's media is hosted on (see the note below the table) |
| [`corp/`](corp/README.en.md) | Domains and IP ranges for major Russian services (Yandex, VK, Mail Group, Sberbank, OZON, Wildberries, Avito, banks) — a trust list, not a blocklist. Full folder descriptions and file table: [corp/README.en.md](corp/README.en.md) |


> ⚠️ **About the Telegram lists.** They contain more than the ranges Telegram publishes officially: they also include the CDN addresses where the media actually lives — photos, videos, stickers, files. That means Google, Amazon CloudFront, Cloudflare, Hetzner and others.
>
> Without those networks the list covers Telegram's signalling but not its content delivery. With them coverage is complete — **but the same networks serve thousands of unrelated sites**, and any rule built on this list will catch those too. Choose deliberately: for "route all Telegram one way" this is what you want; for targeted blocking it is far too broad.
>
> Ranges belonging to Russian networks are stripped from the additional sources. Telegram's own list is never filtered.

## List status

The table below is regenerated automatically on every publish — do not edit by hand. `corp/` file status lives in its own table in [corp/README.en.md](corp/README.en.md), to keep this one short.

**How to read this table.** The "Updated" column shows when a file's contents **actually changed** — not when it was last checked. The "Last checked by automation" line above the table is when the sources were last compared against.

A gap between the two is normal, not a sign of neglect. If a file was "updated" two weeks ago but checked today, the source simply hasn't changed and the list is still current. Files are rewritten only when the data really changes: otherwise the date would move on every run and stop meaning anything, and the commit history would fill up with empty updates.

<!-- STATUS-TABLE:START -->
_Last checked by automation: 2026-08-26 17:41 UTC_

| File | Updated | Lines | MD5 |
|---|---|---|---|
| `Telegram/telegram-ipv4.txt` | 2026-08-26 17:41 UTC | 148 | `6a2eb8beeed3f297b3d6a354e980d29b` |
| `Telegram/telegram-ipv6.txt` | 2026-08-26 17:41 UTC | 41 | `ca34027fef80a9e65146cb6e5943ea97` |
| `blocked/rkn-domain.txt` | 2026-08-11 13:11 UTC | 1642507 | `f9669b97b0441e1f710ae51ad440244a` |
| `blocked/rkn-with-wildcard.txt` | 2026-08-11 13:11 UTC | 3262892 | `41b4143479bfbf7045f5e90a98611bbc` |
| `blocked/ipv4.txt` | 2026-08-21 20:58 UTC | 55918 | `cfa68f9cd3de50597a599042b4e6830a` |
| `blocked/ipv6.txt` | 2026-08-21 20:58 UTC | 3050 | `2636f2259a49b7b6fc39c19ff52c9fc7` |
<!-- STATUS-TABLE:END -->

## How the lists are updated

The lists here follow two different principles — which determines what to expect from them.

**Mirror of the sources — the `Telegram/` folder.** These files are rebuilt from the sources rather than appended to: if a range disappears from every source, it disappears here too.

There are three sources. Telegram's own published list is authoritative — it goes in whole and is never filtered. Alongside it are two lists from [iplist.opencck.org](https://iplist.opencck.org), which are broader and include the CDN networks Telegram serves media through (Google, CloudFront, Cloudflare, Hetzner). That gives fuller coverage, but those same networks carry plenty of unrelated sites — worth knowing if you route traffic based on these lists.

One filter is applied, and only to the additional sources: ranges belonging to Russian networks are removed. The reason is practical — these files feed a routing rule that sends everything listed abroad, while Russian services are meant to be reached from a Russian address. The filter is noted in each file's header.

**Accumulator — the `blocked/` and `corp/` folders.** Entries are only ever added; nothing is removed automatically. If a domain or subnet disappears from a source, it stays in the list.

Why accumulate: an entry vanishing from one source does not mean the block was lifted. Sources are incomplete, maintained by different teams, and periodically lose entries or change scope. Accumulating favours completeness — at the cost of some entries growing stale over time.

| List | Source | Checked against source | Published | Principle |
|---|---|---|---|---|
| `Telegram/telegram-ipv4.txt`, `Telegram/telegram-ipv6.txt` | Telegram's official CIDR list + two [iplist.opencck.org](https://iplist.opencck.org) lists | every 12 hours | only when the data changes | mirror of sources |
| `blocked/rkn-domain.txt`, `blocked/rkn-with-wildcard.txt` | four projects (see "Domain sources" above) | Noktomezo every 12 hours; full merge of all four weekly | weekly, Friday 08:00 UTC | accumulator |
| `blocked/ipv4.txt` | Noktomezo, `ipsets/full.lst` | every 12 hours | weekly, Friday 08:00 UTC | accumulator |
| `blocked/ipv6.txt` | [bol-van/rulist](https://github.com/bol-van/rulist), `reestr_smart6.txt` | weekly | weekly, Friday 08:00 UTC | accumulator |
| [`corp/`](corp/README.en.md) | see [corp/README.en.md](corp/README.en.md) | weekly | weekly, Friday 08:00 UTC | accumulator |

Everything updates automatically on a schedule, with no manual step. The exact last-change time per file is in the status table above.

**Guard against corrupting a list.** Every download is sanity-checked for size. If a source temporarily returns an empty or suspiciously short response, the update is skipped and the previous version of the file is kept — a slightly stale working list beats one overwritten with incomplete data.

The `corp/` schedule is documented in detail in [corp/README.en.md](corp/README.en.md).

## Format

**Domains** — plain text, one per line, no comments. In `rkn-with-wildcard.txt`, some lines start with `*.`.

```
example.com
*.another-domain.ru
```

**IP (`blocked/ipv4.txt`, `blocked/ipv6.txt`)** — CIDR notation, one range per line, no comments. IPv4 and IPv6 live in separate files.

**IP (`Telegram/`)** — the same CIDR notation, plus a header of lines starting with `#`: the source, the date it last changed, and the number of ranges. Tools that skip `#` lines (most do) read the file with no configuration change.

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
