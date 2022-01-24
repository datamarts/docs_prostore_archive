---
layout: default
title: Форматы даты и времени в запросах
nav_order: 6
parent: Справочная информация
has_children: false
has_toc: false
---

# Форматы даты и времени в запросах {#timestamp_formats}

Дату и время в запросах можно указывать в следующих форматах:
* с точностью до секунд: `YYYY-MM-DD hh:mm:ss` (например, 2021-05-25 18:00:17);
* с любой точностью от десятых секунд (`S`) до микросекунд (`SSSSSS`):
    * `YYYY-MM-DD hh:mm:ss.S`,
    * `YYYY-MM-DD hh:mm:ss.SS`,
    * `YYYY-MM-DD hh:mm:ss.SSS` (например, 2021-05-25 18:00:17.876),
    * `YYYY-MM-DD hh:mm:ss.SSSS`,
    * `YYYY-MM-DD hh:mm:ss.SSSSS`,
    * `YYYY-MM-DD hh:mm:ss.SSSSSS` (например, 2021-05-25 18:00:17.876784).