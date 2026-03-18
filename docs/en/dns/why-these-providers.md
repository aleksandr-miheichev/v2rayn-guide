---
title: Why Quad9 and Mullvad
description: DNS provider selection rationale
---

# Why Quad9 and Mullvad

| Criterion | Quad9 | Mullvad | Google (8.8.8.8) | Cloudflare (1.1.1.1) |
|---|:---:|:---:|:---:|:---:|
| No-log policy | :white_check_mark: | :white_check_mark: | :x: | :warning: partial |
| Jurisdiction | Switzerland | Sweden | USA | USA |
| DoH support | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Malware blocking | :white_check_mark: | Optional | :x: | :warning: partial |
| Not tied to ad business | :white_check_mark: | :white_check_mark: | :x: | :white_check_mark: |

---

## Why two, not one

Two DNS servers = **redundancy**. If one is down, queries automatically go to the second. Different jurisdictions (Switzerland + Sweden) = simultaneous outage is extremely unlikely.

## Why not Google or Cloudflare

- **Google DNS:** Google is an advertising company. DNS queries are valuable behavioral data.
- **Cloudflare:** Better than Google, but US jurisdiction means potential National Security Letters without user knowledge.
