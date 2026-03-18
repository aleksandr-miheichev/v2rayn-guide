---
title: FAQ
description: Common questions and solutions
---

# :material-frequently-asked-questions: FAQ

---

## General

??? question "Which v2rayN version should I use?"
    Latest stable from [github.com/2dust/v2rayN/releases](https://github.com/2dust/v2rayN/releases).

??? question "Xray or sing-box — which to choose?"
    **Xray** — default core, system proxy mode. Works for most tasks.
    **sing-box** — used in TUN mode to capture all system traffic.
    Recommended to configure DNS for both.

??? question "What is TUN mode?"
    TUN creates a virtual network interface at OS level. All system traffic goes through it — even apps that don't support proxy settings (games, some messengers). Requires admin rights.

---

## Routing issues

??? question "Site opens but thinks I'm abroad"
    The site goes through proxy instead of direct. It should already be covered
    by rule 13 (`geosite:category-ru`). If the specific site still doesn't work,
    add its domain as a separate rule with `outboundTag: direct`.

??? question "Blocked site doesn't open"
    1. Check proxy is working (green icon in v2rayN tray)
    2. Check the site is in `geosite:ru-blocked`
    3. If not — add the domain manually to rule 11
    4. Make sure the final rule (`0-65535 → proxy`) is in place

??? question "Everything goes through proxy, nothing direct"
    Check **rule order**. Direct rules (private networks, Russian sites) must be **above** proxy rules and the final rule.

---

## DNS issues

??? question "DNS Leak Test shows ISP servers"
    1. QUIC block rule (UDP:443) must be **first** in routing
    2. DNS settings must be filled (Quad9 + Mullvad)
    3. Fully restart v2rayN
    4. Check Windows DNS isn't manually overridden

??? question "Sites load slowly after DNS setup"
    DoH via proxy adds latency on first request. After caching (8192 entries) — repeat queries are fast. Check latency to your proxy: `ping your-server.example.com` (normal: < 100ms).

---

## Telegram

??? question "Telegram works but calls don't connect"
    Check Telegram UDP rule exists in routing with `network: udp` and current IP ranges from [core.telegram.org/resources/cidr.txt](https://core.telegram.org/resources/cidr.txt).

---

## Other

??? question "Torrents are slow"
    Enable **sniffing** in v2rayN: Settings → Basic settings → Sniffing → enable. Without it, v2rayN can't detect BitTorrent protocol and sends traffic through proxy.

??? question "How to update geosite/geoip lists?"
    - **Xray:** v2rayN menu → Update → Update Geo files
    - **sing-box:** rule_sets update automatically every 6 hours (`update_interval`)

??? question "Can I use other DNS instead of Quad9/Mullvad?"
    Yes. Requirements: DoH support, no-log policy, stability. Alternatives: AdGuard DNS, NextDNS. Don't use Google DNS or ISP DNS.
