---
title: Verification
description: Make sure routing and DNS work correctly
---

# :material-check-circle: Verification

After configuring routing and DNS — **always verify** everything works.

---

## Checklist

### 1. DNS Leak Test

<div class="steps" markdown>

1. Open [dnsleaktest.com](https://dnsleaktest.com)
2. Click **Extended test**
3. Wait for results (30–60 seconds)

</div>

!!! success "Correct result"
Only **Quad9** and/or **Mullvad** servers in the list. No ISP servers.

!!! danger "Something's wrong"
If you see your ISP's servers — you have a **DNS leak**. Check the QUIC block
rule (UDP:443), DNS settings, and restart v2rayN.

---

### 2. Split tunneling check

#### Russian sites — direct

Open [2ip.ru](https://2ip.ru) → should show **your Russian IP**.

#### Blocked sites — via proxy

Open [youtube.com](https://youtube.com) → should load. Check IP
at [whatismyipaddress.com](https://whatismyipaddress.com) → should show your *
*proxy server's** IP.

---

### 3. WebRTC Leak Test

Open [browserleaks.com/webrtc](https://browserleaks.com/webrtc) → your real IP
should not be exposed.

!!! warning "WebRTC can expose your IP"

- **Firefox:** `about:config` → `media.peerconnection.enabled` → `false`
- **Chrome:** install WebRTC Leak Prevent extension

---

### 4. Ad blocking test

Open [adblock.turtlecute.org](https://adblock.turtlecute.org/) → test starts
automatically → blocking percentage should be above zero.

---

## Quick reference table

| Check         | Where                                                      | Expected result      |
|---------------|------------------------------------------------------------|----------------------|
| DNS leaks     | [dnsleaktest.com](https://dnsleaktest.com)                 | Only Quad9 / Mullvad |
| Russian sites | [2ip.ru](https://2ip.ru)                                   | Russian IP           |
| Blocked sites | [youtube.com](https://youtube.com)                         | Opens                |
| Proxy IP      | [whatismyipaddress.com](https://whatismyipaddress.com)     | Proxy IP (Germany)   |
| WebRTC        | [browserleaks.com/webrtc](https://browserleaks.com/webrtc) | No real IP leak      |
| Ads           | [adblock.turtlecute.org](https://adblock.turtlecute.org/)  | Blocking > 0%        |
