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
_Last checked by automation: not run yet_

| File | Updated | Lines | MD5 |
|---|---|---|---|
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
