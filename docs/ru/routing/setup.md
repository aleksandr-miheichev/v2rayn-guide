---
title: Настройка маршрутизации шаг за шагом
description: Пошаговая инструкция со скриншотами — куда нажимать в v2rayN
---

# Настройка маршрутизации шаг за шагом

!!! info "Время: ~5 минут"

    Ниже — пошаговая инструкция со скриншотами. Следуйте по порядку.

---

## Шаг 1. Откройте настройки маршрутизации

<div class="steps" markdown>

1. Откройте **v2rayN**
2. В верхнем меню нажмите **Settings**
3. Выберите **Routing Setting**

</div>

<figure>
  <img src="../../assets/images/routing/step1-open-routing.png"
       alt="Открытие настроек маршрутизации в v2rayN"
       loading="lazy">
  <figcaption>Settings → Routing Setting</figcaption>
</figure>

---

## Шаг 2. Нажмите «+ Add»

Откроется окно **Routing Setting** со списком существующих наборов правил.

<div class="steps" markdown>

1. Нажмите кнопку **+ Add** в левом верхнем углу

</div>

<figure>
  <img src="../../assets/images/routing/step2-routing-window.png"
       alt="Окно Routing Setting с кнопкой Add"
       loading="lazy">
  <figcaption>Нажмите «+ Add» для создания нового набора правил</figcaption>
</figure>

---

## Шаг 3. Скопируйте правила и вставьте через буфер обмена

Откроется окно **Rule Settings**. Самый быстрый способ — импорт через буфер
обмена.

<div class="steps" markdown>

1. Скопируйте JSON правил ниже (нажмите иконку :material-content-copy: в правом
   верхнем углу блока кода)
2. В окне Rule Settings нажмите вкладку **Import Rules From Clipboard**
3. Нажмите на неё

</div>

<figure>
  <img src="../../assets/images/routing/step3-import-clipboard.png"
       alt="Вкладка Import Rules From Clipboard"
       loading="lazy">
  <figcaption>Нажмите «Import Rules From Clipboard» — правила вставятся из буфера обмена</figcaption>
</figure>

??? note "JSON правил маршрутизации — нажмите чтобы развернуть и скопировать"

    ```json title="routing-rules.json"
    --8<-- "configs/v2rayn/xray/routing-rules.json"
    ```

    **Онлайн:** скопируйте JSON выше, нажав :material-content-copy:

    **Локально:** файл находится в `configs/v2rayn/xray/routing-rules.json`

---

## Шаг 4. Подтвердите импорт

Появится диалоговое окно с вопросом: «Do you want to append rules?»

<div class="steps" markdown>

1. Если создаёте **новый** набор правил — нажмите **Нет** (заменить)
2. Если хотите **добавить** к существующим — нажмите **Да** (добавить)

</div>

<figure>
  <img src="../../assets/images/routing/step4-append-dialog.png"
       alt="Диалог добавления или замены правил"
       loading="lazy">
  <figcaption>«Да» = добавить к существующим, «Нет» = заменить все правила</figcaption>
</figure>

!!! tip "Рекомендация"
    Если настраиваете с нуля — нажмите **Нет** (replace), чтобы получить
чистый набор правил без примесей.

---

## Шаг 5. Проверьте правила, заполните имя и стратегии

После импорта вы увидите все правила в списке Rule List.

<div class="steps" markdown>

1. Убедитесь, что правила отображаются в списке (15 правил)
2. В поле **Remarks** введите имя набора, например: `Rules`
3. Выберите **Domain strategy**: `IPOnDemand`
4. Выберите **sing-box domain strategy**: `ipv4_only`
5. Нажмите **Confirm** внизу справа

</div>

<figure>
  <img src="../../assets/images/routing/step5-rules-imported.png"
       alt="Импортированные правила с заполненными полями"
       loading="lazy">
  <figcaption>Заполните Remarks, выберите стратегии, нажмите Confirm</figcaption>
</figure>

<div class="param-card" markdown>

**Domain strategy: `IPOnDemand`** — Xray резолвит домен в IP **только когда это
необходимо** для проверки IP-правил. Это экономит DNS-запросы: если трафик
уже совпал по домену — IP не запрашивается. Оптимальный баланс между точностью
и скоростью.

</div>

<div class="param-card" markdown>

**sing-box domain strategy: `ipv4_only`** — при работе в TUN-режиме (ядро
sing-box)
запрашивать только IPv4-адреса. IPv6 отключён — меньше утечек, меньше
неожиданного поведения.

</div>

---

## Шаг 6. Подтвердите в окне Routing Setting

Вы вернётесь в главное окно **Routing Setting**. Ваш новый набор правил
должен появиться в списке.

<div class="steps" markdown>

1. Убедитесь, что ваш набор (`Rules`) есть в списке
2. Нажмите **Confirm** внизу справа

</div>

<figure>
  <img src="../../assets/images/routing/step6-confirm-routing.png"
       alt="Routing Setting с новым набором правил"
       loading="lazy">
  <figcaption>Набор «Rules» появился в списке → нажмите Confirm</figcaption>
</figure>

!!! success "Готово!"

    Маршрутизация настроена. Не забудьте **выбрать** этот набор правил
    в главном окне v2rayN: в нижней панели → выпадающий список **Routing** →
    выберите ваш набор `Rules`.

---

## Шаг 7. Активируйте набор правил

В главном окне v2rayN, в нижней строке статуса:

<div class="steps" markdown>

1. Найдите выпадающий список **Routing** (справа внизу)
2. Выберите ваш набор `Rules`
3. Перезапустите соединение: кнопка Reload в меню

</div>

---

## Что дальше

Маршрутизация настроена! Теперь настроим безопасные DNS:

[:material-arrow-right: Настройка DNS →](../dns/index.md)
