---
title: How routing rules work
description: Key concepts — outboundTag, domain, ip, geosite
---

# How routing rules work

Before configuring — let's understand the terms. Don't worry, it's simpler
than it looks.

---

## Three traffic directions

Each rule sends traffic to one of three "directions" (`outboundTag`):

| outboundTag | What it does | Example |
|---|---|---|
| `proxy` | Sends through your proxy server | YouTube, Google, Instagram |
| `direct` | Sends directly (no proxy) | VK, Yandex, local network |
| `block` | Completely blocks the connection | Ads, telemetry |

---

## How v2rayN decides where to send

A rule can check:

### :material-web: Domain (`domain`)

Checks the **site name** in the address bar.

```
domain: ["youtube.com", "google.com"]  →  outboundTag: proxy
```

### :material-ip-network: IP address (`ip`)

Checks the **IP address** of the destination server.

```
ip: ["91.108.4.0/22"]  →  outboundTag: proxy
```

### :material-network: Port and protocol (`port`, `network`)

```
port: "53", network: "udp"  →  outboundTag: block
```

Blocks all raw DNS queries over UDP port 53 to prevent DNS leaks.

---

## What are `geosite` and `geoip`

These are **ready-made lists** of domains and IPs maintained by the community:

<div class="param-card" markdown>

**`geosite:ru-blocked`** — domains blocked by Roskomnadzor
(YouTube, Instagram, Twitter, and thousands more). Updated automatically.

</div>

<div class="param-card" markdown>

**`geosite:ru-available-only-inside`** — sites that **only work from Russia**
(some government services, regional resources).
Must go direct, otherwise they won't open through a foreign proxy.

</div>

<div class="param-card" markdown>

**`geosite:category-ads-all`** — ad network and tracker domains.
Blocking = cleaner, faster internet.

</div>

<div class="param-card" markdown>

**`geoip:private`** — private IP ranges (`192.168.x.x`, `10.x.x.x`, `127.x.x.x`).
Your local network — always direct.

</div>

!!! info "Where do these lists come from?"

    We use lists from
    [runetfreedom/russia-v2ray-rules-dat](https://github.com/runetfreedom/russia-v2ray-rules-dat) —
    maintained by the community and regularly updated.

---

## Rule checking order

```
Request → Rule 1 (match?)
              ↓ no
         Rule 2 (match?)
              ↓ no
         Rule 3 (match?)
              ↓ no
           ...
         Final rule → proxy
```

!!! tip "Principle"

    - **Narrower** rules — higher (specific ports, specific domains)
    - **Broader** rules — lower (entire `geosite` categories)
    - **Final** rule — always last (catches everything not matched)

---

Now that you understand the principles — let's [set it up in v2rayN →](setup.md)
