# corp/ — trust lists for major Russian services

🇬🇧 English • [🇷🇺 Русский](README.md) · [⬅ Main README](../README.en.md)

## What this is

Unlike `blocked/` (which **blocks**), `corp/` is a **trust list**: domains and IP ranges for major Russian services that make sense to always route as RU-domestic traffic, regardless of where the client is physically located. A false negative here (a service missing from the list when it shouldn't be) breaks a service the user actually relies on — so these lists are built erring toward completeness, not minimalism.

Each company is its own folder with three files:

| File | Contents |
|---|---|
| `<prefix>-domain.txt` | Domains, one per line. No `full:` markup — suffix matching is assumed (the domain and all its subdomains), same convention as this project's internal `ru_services_domains.txt` |
| `<prefix>-ipv4.txt` | IPv4 ranges in CIDR notation, one per line |
| `<prefix>-ipv6.txt` | IPv6 ranges in CIDR notation. If a company has no announced IPv6 (it happens) the file exists and is empty — that's a confirmed fact, not an omission |

## Folders and what's in them

| Folder | Prefix | Coverage |
|---|---|---|
| `yandex/` | `ya-` | Yandex: search, mail, cloud (Yandex Cloud), Alice, Direct, Kinopoisk. **Does not include** Dzen (VK Group-owned since 2022 — see `mailgroup/`) or YooMoney/YooKassa (Sberbank-owned since 2020) |
| `vk/` | `vk-` | VKontakte specifically (vk.com/vk.ru) — the product itself |
| `mailgroup/` | `mg-` | The entire VK Group holding: Mail.ru + VKontakte + Odnoklassniki + Dzen + My.Games + RuStore + VK Play and other group brands. Overlaps with `vk/` on vk.com domains — expected, `vk/` is already part of the holding |
| `sber/` | `sber-` | Sberbank and its ecosystem: 2GIS, Okko, GigaChat, SberDevices, SberCloud, and other subsidiaries |
| `ozon/` | `ozon-` | The OZON marketplace. Ozon Bank, a separately licensed entity, lives in `banks/`, not here |
| `wildberries/` | `wb-` | Wildberries, including brands from the 2024 merger with Russ (outdoor advertising) |
| `avito/` | `av-` | Avito (classifieds) |
| `banks/` | `bank-` | Russian banks (except Sberbank — it has its own folder above) plus the Bank of Russia's website. **In progress** |

## Methodology

**Domains** — sourced from [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community), which maintains a dedicated file per company (`data/yandex`, `data/vk`, `data/mailru-group`, etc.), plus a handful of targeted additions found via dedicated research (e.g. `yadi.sk` for Yandex — Yandex Disk's short-link domain, a genuinely separate apex, not a subdomain). If a company runs a cloud platform that also hosts third-party customer traffic (Yandex Cloud, VK Cloud), its ASN is still included — completeness matters more than precision for a trust list.

**IP ranges** — not a static snapshot: every weekly build re-queries [RIPEstat](https://stat.ripe.net/) directly by ASN for each company (`https://stat.ripe.net/data/announced-prefixes/data.json?resource=AS<number>`), the same way each ASN was originally identified. The per-company ASN list was built from RIPE WHOIS (owner/maintainer) and cross-checked by resolving the company's real domains into those ranges.

Subsidiary entities in other countries (e.g. Wildberries KZ/GE/BY — same legal entity, regional nodes) are included under that same legal entity's list.

## File status

The table below is regenerated automatically on every publish — do not edit by hand.

<!-- STATUS-TABLE:START -->
_Last checked by automation: 2026-09-02 05:42 UTC_

| File | Updated | Lines | MD5 |
|---|---|---|---|
| `corp/yandex/ya-domain.txt` | 2026-08-12 23:05 UTC | 134 | `0b18069fa8aba96ec880acfa5b16dc8b` |
| `corp/yandex/ya-ipv4.txt` | 2026-08-28 08:01 UTC | 122 | `e662e168f5eacb58732568a2c460f5dc` |
| `corp/yandex/ya-ipv6.txt` | 2026-08-11 15:06 UTC | 30 | `845aaeac1287d0439c6bc25fec1ff7c5` |
| `corp/vk/vk-domain.txt` | 2026-08-11 15:05 UTC | 52 | `b8618fc1530ce8d186ee7ec74809176a` |
| `corp/vk/vk-ipv4.txt` | 2026-08-11 15:05 UTC | 48 | `8a75327702e3264e1bee14d415d95f7e` |
| `corp/vk/vk-ipv6.txt` | 2026-08-11 15:06 UTC | 14 | `60cc0911e9a017c402a59920ed3152d2` |
| `corp/mailgroup/mg-domain.txt` | 2026-08-11 15:05 UTC | 300 | `38ce0639f0c742c69be23f924b657679` |
| `corp/mailgroup/mg-ipv4.txt` | 2026-08-11 15:05 UTC | 109 | `faacdf558fda28a9e9a13e7bb5a0980a` |
| `corp/mailgroup/mg-ipv6.txt` | 2026-08-11 15:05 UTC | 9 | `5c310e7e1dd8ff2026c1778e26074e5f` |
| `corp/sber/sber-domain.txt` | 2026-08-11 15:05 UTC | 101 | `c2d94bc87d09505210d10290bd64af42` |
| `corp/sber/sber-ipv4.txt` | 2026-08-21 20:40 UTC | 36 | `6f3c133d42c71c9d249cb3c410e78601` |
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
| `corp/banks/bank-domain.txt` | 2026-08-11 21:03 UTC | 43 | `baaa9ef7a63f2f8ee9f5ca572aadaf85` |
| `corp/banks/bank-ipv4.txt` | 2026-08-28 08:01 UTC | 107 | `f1c444eb15e98ab3dd327e80218f2512` |
| `corp/banks/bank-ipv6.txt` | 2026-08-11 21:03 UTC | 1 | `47332936eb8c687efff5994e3aba06f1` |
<!-- STATUS-TABLE:END -->

## Update schedule

All `corp/` files are refreshed **weekly**, Friday 08:00 UTC — the same automation as `blocked/`. Unlike `blocked/` (additive, never shrinks), `corp/` is a trust list: if an ASN stops announcing a range or a domain drops out of the source, it correctly disappears from the file on the next build — that's not a bug.

## Usage

**sing-box / Xray / v2ray** — domains as suffix-matched entries (domain + all subdomains) in a routing rule, IP files as a separate IP-based rule. Example: route all traffic to Yandex through a direct RU egress, even when the client itself isn't physically in Russia.

**MikroTik / routers** — build a DNS-based address-list from `*-domain.txt` with `match-subdomain=yes`; `*-ipv4.txt`/`*-ipv6.txt` as static address-lists for policy routing.

## Disclaimer

These lists are built from publicly available data ([v2fly/domain-list-community](https://github.com/v2fly/domain-list-community), [RIPEstat](https://stat.ripe.net/)) for informational purposes. This project is not affiliated with any of the listed companies and cannot guarantee the completeness or accuracy of their infrastructure classification — in particular, cloud platforms (Yandex Cloud, VK Cloud) host third-party customer traffic too, not just the company's own.

## License

Released under [AGPL-3.0](../LICENSE), same as the rest of the repo.
