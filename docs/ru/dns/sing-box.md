---
title: sing-box Custom DNS
description: Настройка безопасных DNS для ядра sing-box в v2rayN
---

# sing-box Custom DNS

---

## Шаг 1. Откройте вкладку sing-box Custom DNS

<div class="steps" markdown>

1. В окне **DNS Settings** нажмите вкладку **sing-box Custom DNS**
2. Включите переключатель **Enable Custom DNS** (если ещё не включён)

</div>

<figure>
  <img src="../../assets/images/dns/step4-singbox-empty.png"
       alt="Вкладка sing-box Custom DNS — пустая"
       loading="lazy">
  <figcaption>Вкладка sing-box Custom DNS с двумя пустыми полями</figcaption>
</figure>

---

## Шаг 2. Вставьте конфигурацию в ОБА поля

На вкладке два текстовых поля:

- **HTTP/SOCKS** — используется когда sing-box работает в режиме прокси
- **Tun Mode settings** — используется когда sing-box работает в TUN-режиме

!!! warning "Вставьте в оба поля"
    Одну и ту же конфигурацию нужно вставить в **оба** поля.
    Так DNS будет работать корректно в любом режиме.

Скопируйте JSON ниже и вставьте в **оба** поля:

??? note "JSON конфигурации sing-box DNS — нажмите чтобы развернуть и
скопировать"

    ```json title="sing-box-dns.json"
    --8<-- "configs/v2rayn/sing-box/dns.json"
    ```

    **Онлайн:** скопируйте JSON выше, нажав :material-content-copy:

    **Локально:** файл находится в `configs/v2rayn/sing-box/dns.json`

---

## Шаг 3. Укажите стратегию и DNS address

<div class="steps" markdown>

1. Внизу окна в поле **Default domain strategy for outbound** выберите:
   `prefer_ipv4`
2. В поле **Outbound DNS address** выберите: `dhcp://auto`
3. Нажмите **Confirm**

</div>

<figure>
  <img src="../../assets/images/dns/step5-singbox-filled.png"
       alt="sing-box Custom DNS — заполненная конфигурация"
       loading="lazy">
  <figcaption>Конфигурация вставлена в оба поля, стратегия и DNS address заполнены</figcaption>
</figure>

<div class="param-card" markdown>

**`prefer_ipv4`** — при резолве доменов для исходящего direct-трафика
предпочитать IPv4-адреса, но не отключать IPv6 полностью.

</div>

<div class="param-card" markdown>

**`dhcp://auto`** — для direct-трафика использовать DNS от роутера (DHCP).
Аналогично настройке Xray — прямой трафик резолвится локально.

</div>

---

## Объяснение каждого параметра

### DNS-сервер (Quad9 DoH)

```json
{
  "tag": "quad9-doh",
  "type": "https",
  "server": "9.9.9.9",
  "server_port": 443,
  "path": "/dns-query",
  "headers": {
    "Host": "dns.quad9.net"
  },
  "tls": {
    "enabled": true,
    "server_name": "dns.quad9.net",
    "utls": {
      "enabled": true,
      "fingerprint": "chrome"
    }
  },
  "detour": "proxy"
}
```

<div class="param-card" markdown>

**`server: "9.9.9.9"`** — подключение напрямую **по IP-адресу** Quad9.

**Зачем IP, а не домен?** Это элегантное решение проблемы DNS-петли.
Если указать домен `dns.quad9.net` — sing-box попытается его зарезолвить,
а для этого нужен DNS → петля. IP-адрес резолва не требует.

</div>

<div class="param-card" markdown>

**`headers: { "Host": "dns.quad9.net" }`** — HTTP-заголовок `Host`,
который отправляется серверу.

**Зачем:** мы подключаемся по IP (`9.9.9.9`), но серверу нужно знать,
к какому «сайту» мы обращаемся. Заголовок `Host` говорит: «я хочу
`dns.quad9.net`». Без него сервер может не понять запрос.

</div>

<div class="param-card" markdown>

**`tls.server_name: "dns.quad9.net"`** — SNI (Server Name Indication)
в TLS-хэндшейке.

**Зачем:** сервер `9.9.9.9` обслуживает несколько сервисов. SNI говорит
ему, какой сертификат использовать. Также нужен для **валидации
сертификата** — sing-box проверяет, что сертификат выдан именно для
`dns.quad9.net`.

</div>

<div class="param-card" markdown>

**`utls.fingerprint: "chrome"`** — имитировать TLS-отпечаток браузера
Chrome.

**Зачем:** делает DNS-трафик **неотличимым** от обычного просмотра веба
для систем DPI. Без этого TLS-хэндшейк выглядит как «программа, а не
браузер» — и может быть заблокирован.

</div>

<div class="param-card" markdown>

**`detour: "proxy"`** — DNS-запросы идут **через прокси-туннель**.
Провайдер не видит ни запросы, ни ответы, ни сам факт обращения к
DNS-серверу.

</div>

---

### DNS-правило: блокировка рекламы и телеметрии

```json
{
  "rule_set": [
    "geosite-category-ads-all",
    "geosite-win-spy"
  ],
  "action": "predefined",
  "rcode": "NXDOMAIN"
}
```

<div class="param-card" markdown>

**`action: "predefined"` + `rcode: "NXDOMAIN"`** — для рекламных доменов
и доменов Windows-телеметрии sing-box отвечает «домен не существует».

Приложение получает ответ **мгновенно**, без реального DNS-запроса.
Реклама не загружается, телеметрия не отправляется.

</div>

---

### Глобальные настройки

<div class="param-card" markdown>

**`final: "quad9-doh"`** — DNS-сервер по умолчанию для всех запросов,
не попавших ни в одно правило.

</div>

<div class="param-card" markdown>

**`strategy: "ipv4_only"`** — глобально: только IPv4 для DNS-запросов
через прокси.

</div>

<div class="param-card" markdown>

**`cache_capacity: 8192`** — размер DNS-кэша (количество записей).
8192 — хороший баланс между скоростью и потреблением RAM.

</div>

<div class="param-card" markdown>

**`independent_cache: false`** — общий кэш для всех DNS-серверов.
Если один сервер уже зарезолвил домен — повторный запрос не нужен.

</div>

---

## Готово!

Теперь нажмите **Confirm** в окне DNS Settings — сохранятся настройки
обеих вкладок (V2ray Custom DNS и sing-box Custom DNS).

Перезапустите соединение: кнопка Reload в меню

[:material-arrow-right: Проверка →](../verification/index.md)
