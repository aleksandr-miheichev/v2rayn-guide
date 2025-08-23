# v2rayN DNS & Routing: sing-box 1.12 + Xray

Набор рабочих конфигов и кратких инструкций:

- **DNS sing-box 1.12** (DoH Quad9/Mullvad через прокси, защита от DNS-петли,
  блокировка рекламы NXDOMAIN)
- **DNS Xray** (эквивалентная схема для ядра Xray)
- **Маршрутизация v2rayN** (основные правила + Telegram UDP)

> Цели: приватность, маскировка рукопожатий, стабильность и совместимость.

---

## Быстрый старт

1. Обновите v2rayN до версии с поддержкой sing-box 1.12 / Xray (рекомендуется
   свежая).
2. Импортируйте нужный JSON:
    - **sing-box**: `configs/sing-box-1.12/dns+route.json`
    - **xray**: копируйте `configs/xray/dns.json` в блок DNS ядра Xray
3. Включите правила маршрутизации по образцу (см. `configs/v2rayN/routing.md`)
   и скриншоты в `docs/images`.

---

## Как это работает (коротко и простыми словами)

- **Два вида DNS (Quad9 и Mullvad) по HTTPS** идут **через прокси-туннель** →
  провайдер не видит запросы (DoH), трафик «похож» на обычный HTTPS. Для DoH
  явно задано **`server_name`** (SNI) — это унифицирует рукопожатие и проверку
  сертификата, снижая «аномалии» в TLS. См. доку по TLS полю `server_name`.
- Чтобы **не попасть в DNS-петлю**, DoH-доменные имена (например
  `dns.quad9.net`) сначала резолвятся по **DNS-over-TLS (DoT) напрямую** — поля
  `domain_resolver` указывают на `bootstrap-dot*`, а те уходят **detour: direct
  **. Это штатный паттерн sing-box 1.12. :contentReference[oaicite:1]{index=1}
- Реклама блокируется на уровне DNS правилом `action: "predefined"` +
  `rcode: "NXDOMAIN"` — сервер «как бы» отвечает, что домена не существует. Это
  быстрее и чище, чем `REFUSED`, а поведение прозрачно для приложений. См. «DNS
  Rule Action / rcode». :contentReference[oaicite:2]{index=2}
- В маршрутизации:
    - **частные сети** и **локальные домены** — в обход прокси (меньше
      задержек);
    - **заблокированные в РФ** (по доменам/по IP) — через прокси (удалённые
      ruleset’ы `*.srs` подгружаются и авто-обновляются); см. раздел про **Rule
      Set (remote)**. :contentReference[oaicite:3]{index=3}
    - **Telegram UDP** (VoIP) уводим в прокси по доменам и по официальным
      диапазонам IP Telegram (см. `core.telegram.org/resources/cidr.txt`).

---

## Почему именно Quad9 и Mullvad

- Quad9 DoH: endpoint `/dns-query`, хост `dns.quad9.net`.
- Mullvad DoH: endpoint `/dns-query`, хост `doh.mullvad.net`.

Оба поддерживают DoH, серверы стабильны и хорошо известны.

---

## Пояснения к полям sing-box (1.12)

- **`server_name` в `tls`** — задаёт SNI и имя для валидации сертификата
- (полезно для маскировки и корректного TLS-хэндшейка).
- **`domain_resolver`** у HTTPS-DNS указывает, каким резолвером получить *сам
  домен* DoH-сервера (bootstrap). В примере — DoT напрямую в обход прокси,
  чтобы не зациклиться. :contentReference[oaicite:8]{index=8}
- **`utls` с fingerprint `chrome`** имитирует TLS-клиент Chrome (меньше
  эвристик DPI). (см. TLS section)
- **Rule Set (remote)** — удобный способ тянуть `geosite/geoip` в формате
  `.srs` и обновлять по расписанию. :contentReference[oaicite:10]{index=10}

> Примечание: поля `geosite/geoip` в **самом** Route Rule считаются устаревшими
> в новых схемах — их рекомендуется использовать через **`rule_set`** (как в
> примере). :contentReference[oaicite:11]{index=11}

---

## Xray DNS: эквиваленты

- `queryStrategy: UseIPv4` — аналог `ipv4_only` в sing-box DNS.
- `disableFallbackIfMatch: true` — если совпало с хост-оверрайдом/правилом, не
  уходить в запасной резолвер.  
  Полная спецификация Xray DNS — в официальной доке. :
  contentReference[oaicite:12]{index=12}

---

## Telegram звонки (UDP)

В некоторых регионах UDP для Telegram режут. В правилах v2rayN:

- Сеть: **UDP**
- Домены: `*.telegram.org, *.t.me, *.cdn-telegram.org` → **proxy**
- IP: добавьте официальные диапазоны Telegram из
  `core.telegram.org/resources/cidr.txt` (например `91.108.4.0/22`,
  `91.108.8.0/21`, `91.108.16.0/21`, `91.108.56.0/22`, `149.154.160.0/20`, и т.
  п.) → **proxy**.

Это повышает шанс, что VoIP пойдёт поверх туннеля, минуя UDP-фильтрацию.

---

## Импорт в v2rayN (кратко)

- **DNS Xray**: *Настройки → Настройки DNS V2ray* → вставить JSON из
  `configs/xray/dns.json`.
- **DNS sing-box**: *Настройки → Настройки DNS sing-box* → импортировать
  `configs/sing-box-1.12/dns+route.json`.
- **Маршрутизация**: *Профили → Правила маршрутизации* → добавьте правила из
  `configs/v2rayN/routing.md` (или импортируйте свой набор, если собрано в
  файл).  
  См. скриншоты в `docs/images`.

---

## Тротблшут (коротко)

- **Петля DNS**: проверьте, что у DoH-серверов стоит `domain_resolver` на DoT с
  `detour: direct`. :contentReference[oaicite:14]{index=14}
- **Реклама лезет**: убедитесь, что DNS-правило с `geosite:category-ads-all`
  стоит *выше* финального и что в `dns.rules` включено `rcode: "NXDOMAIN"`. :
  contentReference[oaicite:15]{index=15}
- **Медленно**: можно увеличить `cache_capacity`, но следите за RAM; также
  проверьте, что «тяжёлые» домены не уходят в `direct` без нужды.

---

## Источники / Документация

- sing-box: DNS Rule Action (predefined/rcode) и Legacy rcode. :
  contentReference[oaicite:16]{index=16}
- sing-box: DNS Server HTTPS (1.12), TLS options (`server_name`, `utls`), Rule
  Set (remote), Route Rule. :contentReference[oaicite:17]{index=17}
- Xray: DNS configuration. :contentReference[oaicite:18]{index=18}
- Quad9 DoH.
- Mullvad DoH.
- Telegram CIDR (официально). 
