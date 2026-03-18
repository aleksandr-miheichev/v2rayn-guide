---
title: Quick Start
description: Minimal setup in 5 minutes — no extra explanations
---

# :material-rocket-launch: Quick Start

!!! tip "This page is for those who want it fast"

    Minimum explanations, maximum action. For the **why** —
    read [Routing](../routing/index.md) and [DNS](../dns/index.md).

---

## 1. Routing

**Settings → Routing settings** → add rules or import the ready JSON:

??? note "Routing rules JSON (click to expand and copy)"

    ```json
    --8<-- "configs/v2rayn/xray/routing-rules.json"
    ```

---

## 2. Xray DNS

**Settings → DNS settings V2ray** → paste:

??? note "Xray DNS JSON (click to expand and copy)"

    ```json
    --8<-- "configs/v2rayn/xray/dns.json"
    ```

---

## 3. sing-box DNS (if using TUN mode)

**Settings → DNS settings sing-box** → paste:

??? note "sing-box DNS JSON (click to expand and copy)"

    ```json
    --8<-- "configs/v2rayn/sing-box/dns.json"
    ```

---

## 4. Verification

<div class="steps" markdown>

1. Restart connection: ++ctrl+r++
2. Open [dnsleaktest.com](https://dnsleaktest.com) → Extended test
3. Results should show **only** Quad9 and/or Mullvad
4. Open [2ip.ru](https://2ip.ru) → should show **your Russian IP**
5. Open [youtube.com](https://youtube.com) → should load via proxy

</div>

If everything works — :tada: congratulations! If not — see
[detailed verification](../verification/index.md) and [FAQ](../faq/index.md).
