---
title: v2rayN Setup Guide
description: Split tunneling, DNS security, routing — for all skill levels
---

# :material-shield-lock-outline: v2rayN Setup Guide

> **Goal:** configure v2rayN so that blocked and foreign sites go through proxy,
> while domestic sites connect directly. Fast, secure, no DNS leaks.

---

## What you'll get after setup

| Traffic destination | Route | Why |
|---|---|---|
| :flag_ru: Russian unblocked sites (VK, Yandex, Avito…) | **Direct** (your real IP) | Max speed, sites don't think you're abroad |
| :no_entry: Blocked in Russia (YouTube, Instagram, Twitter…) | **Via proxy** | Bypass censorship |
| :earth_americas: Foreign sites (Google, GitHub, Reddit…) | **Via proxy** | Privacy, ISP tracking protection |
| :loudspeaker: Ads and trackers | **Blocked** | Cleaner, faster internet |

---

## What we'll configure

<div class="steps" markdown>

1. **Routing** — rules for directing traffic
2. **Xray DNS** — secure DNS servers for the Xray core
3. **sing-box DNS** — same for the sing-box core (if using TUN mode)
4. **Verification** — making sure everything works and no leaks

</div>

---

## Requirements

!!! info "What you need before starting"

    - [x] Installed **v2rayN** (latest version recommended)
    - [x] A working **proxy server** (already added and connected in v2rayN)
    - [x] 15 minutes of your time

!!! question "Don't know which core you're using — Xray or sing-box?"

    Open v2rayN → bottom left corner → it shows the current core.
    **Xray** is the default core. **sing-box** is used in TUN mode.

    Don't worry — we'll configure both.

---

## Guide navigation

| Section | Description | Time |
|---|---|---|
| [:material-arrow-right: Quick Start](quickstart/index.md) | Minimal setup in 5 minutes | ~5 min |
| [:material-routes: Routing](routing/index.md) | Detailed routing rules explanation | ~10 min |
| [:material-dns: DNS](dns/index.md) | Secure DNS configuration | ~5 min |
| [:material-check-circle: Verification](verification/index.md) | Testing that everything works | ~3 min |
| [:material-frequently-asked-questions: FAQ](faq/index.md) | Common questions and issues | as needed |

---

!!! tip "Tip"

    If you just need it to work — start with **Quick Start**.
    Minimum explanations, maximum action.

    If you want to **understand** what and why — follow the guide in order
    starting with **Routing**.
