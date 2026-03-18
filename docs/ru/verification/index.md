---
title: Проверка настроек
description: Убедитесь, что маршрутизация и DNS работают правильно
---

# :material-check-circle: Проверка настроек

После настройки маршрутизации и DNS — **обязательно** проверьте, что всё
работает как задумано. Без проверки вы не узнаете об утечках.

---

## Чек-лист проверки

### 1. DNS Leak Test

<div class="steps" markdown>

1. Откройте [dnsleaktest.com](https://dnsleaktest.com)
2. Нажмите **Extended test** (расширенный тест)
3. Дождитесь результатов (30–60 секунд)

</div>

!!! success "Правильный результат"

    В списке серверов должны быть **только**:

    - **Quad9** (Швейцария / Германия / другие страны)
    - **Mullvad** (Швеция / Германия / другие страны)

    Никаких серверов вашего российского провайдера.

!!! danger "Что-то не так"

    Если видите серверы вашего провайдера (Ростелеком, Билайн, МТС и т.д.) —
    у вас **DNS-утечка**. Проверьте:

    - Правило блокировки QUIC (UDP:443) — первое в списке маршрутизации
    - Настройки DNS (должны быть Quad9/Mullvad по DoH)
    - Перезапустите v2rayN полностью

---

### 2. Проверка разделения трафика

#### Российские сайты — напрямую

<div class="steps" markdown>

1. Откройте [2ip.ru](https://2ip.ru)
2. Должен показать **ваш российский IP-адрес**
3. Откройте [yandex.ru](https://yandex.ru) — должен работать быстро

</div>

!!! success "Правильно"
    `2ip.ru` показывает ваш **российский** IP → трафик идёт напрямую ✅

!!! danger "Не так"
    Если `2ip.ru` показывает немецкий/иностранный IP — правило
    `geosite:ru-available-only-inside` не работает или `2ip.ru` попал
    в список заблокированных. Проверьте порядок правил.

---

#### Заблокированные сайты — через прокси

<div class="steps" markdown>

1. Откройте [youtube.com](https://youtube.com) — должен открыться
2. Откройте [instagram.com](https://instagram.com) — должен открыться
3. Проверьте IP: откройте [whatismyipaddress.com](https://whatismyipaddress.com) —
   должен показать IP вашего **прокси-сервера** (Германия)

</div>

!!! success "Правильно"
    Заблокированные сайты открываются, IP — иностранный ✅

---

### 3. WebRTC Leak Test

<div class="steps" markdown>

1. Откройте [browserleaks.com/webrtc](https://browserleaks.com/webrtc)
2. Проверьте, что ваш **реальный IP** не раскрывается

</div>

!!! warning "WebRTC может раскрыть IP"

    Даже с правильно настроенным прокси, WebRTC в браузере может
    показать ваш настоящий IP. Если это критично:

    - **Firefox:** `about:config` → `media.peerconnection.enabled` → `false`
    - **Chrome:** установите расширение WebRTC Leak Prevent

---

### 4. Проверка блокировки рекламы

<div class="steps" markdown>

1. Откройте [d3ward.github.io/toolz/adblock](https://d3ward.github.io/toolz/adblock)
2. Нажмите **Run test**
3. Процент блокировки должен быть значительно выше нуля

</div>

!!! info "100% не будет"

    Блокировка на уровне DNS не ловит всю рекламу (встроенная реклама
    на YouTube, например, идёт с тех же доменов, что и видео).
    Но баннеры, трекеры и всплывающие окна — значительно уменьшатся.

---

### 5. Telegram звонки

<div class="steps" markdown>

1. Откройте **Telegram Desktop**
2. Позвоните кому-нибудь (или в Saved Messages → голосовое сообщение)
3. Звонок должен установиться

</div>

Если звонки не проходят — проверьте правило Telegram UDP в маршрутизации.

---

## Быстрая таблица проверки

| Что проверяем | Где | Ожидаемый результат |
|---|---|---|
| DNS-утечки | [dnsleaktest.com](https://dnsleaktest.com) | Только Quad9 / Mullvad |
| Российские сайты | [2ip.ru](https://2ip.ru) | Российский IP |
| Заблокированные | [youtube.com](https://youtube.com) | Открывается |
| IP через прокси | [whatismyipaddress.com](https://whatismyipaddress.com) | IP прокси (Германия) |
| WebRTC | [browserleaks.com/webrtc](https://browserleaks.com/webrtc) | Нет утечки реального IP |
| Реклама | [d3ward.github.io/toolz/adblock](https://d3ward.github.io/toolz/adblock) | Блокировка > 0% |

---

!!! success "Всё работает?"

    :tada: Поздравляю! Ваш v2rayN настроен правильно.

    Если возникли проблемы — загляните в [FAQ →](../faq/index.md)
