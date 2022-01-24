---
layout: default
title: Поддерживаемые СУБД хранилища
nav_order: 2
parent: Введение
has_children: false
has_toc: false
---

# Поддерживаемые СУБД хранилища {#supported_DBMS}

Система поддерживает работу со следующими СУБД [хранилища](../../overview/main_concepts/data_storage/data_storage.md):
*   **Arenadata DB (ADB)** — СУБД с массивно-параллельной архитектурой (Massive parallel processing, MPP), 
    построенная на основе Greenplum;
*   **Arenadata QuickMarts (ADQM)** — кластерная колоночная СУБД на основе Yandex ClickHouse;
*   **Arenadata Grid (ADG)** — система распределенных вычислений в оперативной памяти, построенная на основе 
    Tarantool;
*   **PostgreSQL (ADP)** — свободная объектно-реляционная СУБД на основе PostgreSQL.

Система позволяет работать с перечисленными СУБД одинаковым образом, используя единый синтаксис [запросов SQL+](../../reference/sql_plus_requests/sql_plus_requests.md) 
и единую [логическую схему данных](../../overview/main_concepts/logical_schema/logical_schema.md).