# v2rayN Setup Guide — DNS & Routing

[![Deploy docs](https://github.com/aleksandr-miheichev/v2rayn-guide/actions/workflows/deploy-docs.yml/badge.svg)](https://github.com/aleksandr-miheichev/v2rayn-guide/actions/workflows/deploy-docs.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

🇷🇺 [Русский](https://aleksandr-miheichev.github.io/v2rayn-guide/) |
🇬🇧 [English](https://aleksandr-miheichev.github.io/v2rayn-guide/en/)

---

## What is this?

A **comprehensive, beginner-friendly guide** for configuring v2rayN with:

- **Split tunneling** — Russian unblocked sites go direct, blocked & foreign go
  through proxy
- **Secure DNS** (DoH via proxy) — no DNS leaks, ISP can't see your queries
- **Ad blocking** at DNS level
- **Telegram UDP** routing for voice/video calls
- **Every parameter explained** — understand what each setting does and why

**No programming knowledge required.** Screenshots, step-by-step instructions,
copy-paste configs.

---

## 📖 Read online

Just open the link — no installation needed:

> **🇷🇺 Русский:
** [aleksandr-miheichev.github.io/v2rayn-guide](https://aleksandr-miheichev.github.io/v2rayn-guide/)
>
> **🇬🇧 English:
** [aleksandr-miheichev.github.io/v2rayn-guide/en/](https://aleksandr-miheichev.github.io/v2rayn-guide/en/)

Works on any device — desktop, tablet, phone.

---

## 💻 Run locally

If you prefer to read offline or want to contribute:

**With uv (recommended):**

```bash
git clone https://github.com/aleksandr-miheichev/v2rayn-guide.git
cd v2rayn-guide
uv sync --extra docs
uv run mkdocs serve
```

**With pip:**

```bash
git clone https://github.com/aleksandr-miheichev/v2rayn-guide.git
cd v2rayn-guide
pip install -r requirements-docs.txt
mkdocs serve
```

Open **http://127.0.0.1:8000** — exact same site as the online version.

---

## Just need the configs?

| Config       | File                                                                               | Paste into                                    |
|--------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| Xray DNS     | [`configs/v2rayn/xray/dns.json`](configs/v2rayn/xray/dns.json)                     | DNS Settings → V2ray Custom DNS               |
| sing-box DNS | [`configs/v2rayn/sing-box/dns.json`](configs/v2rayn/sing-box/dns.json)             | DNS Settings → sing-box Custom DNS            |
| Xray Routing | [`configs/v2rayn/xray/routing-rules.json`](configs/v2rayn/xray/routing-rules.json) | Routing Setting → Import Rules From Clipboard |

Click file → **Raw** → copy entire JSON.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

- DNS
  lists: [runetfreedom/russia-v2ray-rules-dat](https://github.com/runetfreedom/russia-v2ray-rules-dat)
- DNS
  providers: [Quad9](https://quad9.net), [Mullvad](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls/)
- Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)

## License

[MIT](LICENSE)
