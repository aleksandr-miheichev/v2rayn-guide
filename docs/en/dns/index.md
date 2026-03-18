---
title: DNS Configuration
description: Secure DNS servers for Xray and sing-box
---

# :material-dns: DNS Configuration

DNS is the "phone book of the internet." When you type `youtube.com`,
DNS translates that name into a server IP address.

---

## Why configure DNS separately?

!!! danger "Problem: DNS leaks"

    By default, DNS queries go **through your ISP** in plain text. This means:

    - :material-eye: Your ISP **sees** every site you visit
    - :material-close-circle: Your ISP can **spoof** DNS responses to block sites
    - :material-shield-off: Even with a proxy, DNS queries can "leak" outside the tunnel

!!! success "Solution: DoH via proxy"

    We'll configure **DNS over HTTPS (DoH)** — encrypted DNS queries
    that go **through the proxy tunnel**.

---

## How to open DNS settings

All DNS settings are in **one window** with tabs.

<div class="steps" markdown>

1. Open **v2rayN**
2. Top menu → **Settings**
3. Select **DNS Settings**

</div>

<figure>
  <img src="../../assets/images/dns/step1-open-dns.png"
       alt="Opening DNS settings in v2rayN" loading="lazy">
  <figcaption>Settings → DNS Settings</figcaption>
</figure>

The **DNS Settings** window has four tabs:

| Tab | Purpose |
|---|---|
| Basic DNS Settings | Basic settings (don't touch) |
| Advanced DNS Settings | Advanced settings (don't touch) |
| **V2ray Custom DNS** | DNS for Xray core (HTTP/SOCKS proxy mode) |
| **sing-box Custom DNS** | DNS for sing-box core (TUN mode) |

We'll configure **both** — V2ray Custom DNS and sing-box Custom DNS.

---

## Subsections

| Page | What we configure |
|---|---|
| [V2ray Custom DNS (Xray)](xray.md) | V2ray Custom DNS tab — for system proxy mode |
| [sing-box Custom DNS](sing-box.md) | sing-box Custom DNS tab — for TUN mode |
| [Why Quad9 and Mullvad](why-these-providers.md) | DNS provider selection rationale |

!!! tip "Recommendation"
    Configure **both** tabs — so DNS works correctly when switching
    between modes (HTTP/SOCKS ↔ TUN).
