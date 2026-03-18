# Гайд по настройке v2rayN — DNS и маршрутизация

[![Deploy docs](https://github.com/aleksandr-miheichev/v2rayn-guide/actions/workflows/deploy-docs.yml/badge.svg)](https://github.com/aleksandr-miheichev/v2rayn-guide/actions/workflows/deploy-docs.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**🇷🇺 Русский** | 🇬🇧 [English](README.md)

---

## Что это?

**Подробный гайд для новичков** по настройке v2rayN:

- **Раздельное туннелирование** — российские незаблокированные сайты напрямую, заблокированные и зарубежные — через прокси
- **Безопасный DNS** (DoH через прокси) — нет утечек DNS, провайдер не видит ваши запросы
- **Блокировка рекламы** на уровне DNS
- **Блокировка телеметрии Windows** на сетевом уровне
- **Маршрутизация Telegram** для голосовых/видеозвонков
- **Каждый параметр объяснён** — понимание что делает каждая настройка и зачем

**Знания программирования не нужны.** Скриншоты, пошаговые инструкции, готовые конфигурации для копирования.

---

## 📖 Читать онлайн

Просто откройте ссылку — ничего устанавливать не нужно:

> **🇷🇺 Русский:** [aleksandr-miheichev.github.io/v2rayn-guide](https://aleksandr-miheichev.github.io/v2rayn-guide/)
>
> **🇬🇧 English:** [aleksandr-miheichev.github.io/v2rayn-guide/en/](https://aleksandr-miheichev.github.io/v2rayn-guide/en/)

Работает на любом устройстве — компьютер, планшет, телефон.

---

## 💻 Запустить локально

Если предпочитаете читать офлайн или хотите внести вклад:

**С uv (рекомендуется):**
```bash
git clone https://github.com/aleksandr-miheichev/v2rayn-guide.git
cd v2rayn-guide
uv sync --extra docs
uv run mkdocs serve
```

**С pip:**
```bash
git clone https://github.com/aleksandr-miheichev/v2rayn-guide.git
cd v2rayn-guide
pip install -r requirements-docs.txt
mkdocs serve
```

Откройте **http://127.0.0.1:8000** — тот же сайт, что и онлайн-версия.

---

## Нужны только конфиги?

| Конфигурация | Файл | Куда вставить |
|---|---|---|
| Xray DNS | [`configs/v2rayn/xray/dns.json`](configs/v2rayn/xray/dns.json) | DNS Settings → V2ray Custom DNS |
| sing-box DNS | [`configs/v2rayn/sing-box/dns.json`](configs/v2rayn/sing-box/dns.json) | DNS Settings → sing-box Custom DNS |
| Правила маршрутизации | [`configs/v2rayn/xray/routing-rules.json`](configs/v2rayn/xray/routing-rules.json) | Routing Setting → Import Rules From Clipboard |

Нажмите на файл → **Raw** → скопируйте весь JSON.

---

## Участие в проекте

Смотрите [CONTRIBUTING.md](CONTRIBUTING.md).

## Благодарности

- Списки DNS: [runetfreedom/russia-v2ray-rules-dat](https://github.com/runetfreedom/russia-v2ray-rules-dat)
- DNS-провайдеры: [Quad9](https://quad9.net), [Mullvad](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls/)
- Собрано с помощью [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)

## Лицензия

[MIT](LICENSE)
