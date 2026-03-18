---
title: V2ray Custom DNS (Xray)
description: Secure DNS configuration for the Xray core in v2rayN
---

# V2ray Custom DNS (Xray)

## Step 1. Open V2ray Custom DNS tab

<div class="steps" markdown>

1. In **DNS Settings** window click the **V2ray Custom DNS** tab
2. Enable **Enable Custom DNS** toggle (if not already on)

</div>

<figure>
  <img src="../../assets/images/dns/step2-v2ray-empty.png"
       alt="V2ray Custom DNS tab — empty" loading="lazy">
  <figcaption>V2ray Custom DNS tab with empty HTTP/SOCKS field</figcaption>
</figure>

## Step 2. Paste configuration

Copy the JSON below and paste into the **HTTP/SOCKS** field:

??? note "Xray DNS JSON — click to expand and copy"

    ```json title="xray-dns.json"
    --8<-- "configs/v2rayn/xray/dns.json"
    ```

## Step 3. Set Outbound DNS address

<div class="steps" markdown>

1. At the bottom, set **Outbound DNS address**: `dhcp://auto`
2. Click **Confirm**

</div>

<figure>
  <img src="../../assets/images/dns/step3-v2ray-filled.png"
       alt="V2ray Custom DNS — filled" loading="lazy">
  <figcaption>Configuration pasted, Outbound DNS address = dhcp://auto</figcaption>
</figure>

<div class="param-card" markdown>
**`dhcp://auto`** — for direct outbound traffic, Xray uses DNS from your router (DHCP). Direct traffic (Russian sites) resolves locally — faster, no anomalies.
</div>

!!! warning "Don't click Confirm yet!"
    First configure the sing-box Custom DNS tab (next page), then Confirm once — both settings save together.

---

## Parameter explanations

### `hosts` block

<div class="param-card" markdown>
Maps DNS server names to IPs directly — **bootstrap** that breaks the DNS loop. Without it, Xray would try to resolve `dns.quad9.net` through itself.
</div>

### `servers` block

<div class="param-card" markdown>
**`unexpectedIPs: ["geoip:private"]`** — if a DNS server returns a private IP (`192.168.x.x`) — treat it as suspicious (likely DNS poisoning by ISP) and try the next server.
</div>

### Global settings

<div class="param-card" markdown>
**`serveStale: true`** + **`serveExpiredTTL: 3600`** — if a cached DNS entry expires, still serve it (up to 1 hour) while refreshing in background. Critical for stability: a temporary DNS outage won't break your internet.
</div>

<div class="param-card" markdown>
**`useSystemHosts: false`** — don't use the system `hosts` file. It could be modified by malware.
</div>

<div class="param-card" markdown>
**`tag: "dns_inbound"`** — internal name for the DNS module, used in routing.
</div>

---

[:material-arrow-right: sing-box Custom DNS →](sing-box.md)
