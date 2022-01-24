---
layout: default
title: Загружаемые типы данных Avro
nav_order: 2
parent: Поддерживаемые типы данных
grand_parent: Справочная информация
has_children: false
has_toc: false
---

# Загружаемые типы данных Avro {#upload_data_types}

Система поддерживает загрузку типов данных Avro, перечисленных в таблице ниже. Для каждого типа данных 
Avro указан соответствующий [логический тип данных](../logical_data_types/logical_data_types.md).

Подробнее о типах данных Avro см. в [официальной документации](https://docs.oracle.com/database/nosql-12.1.3.0/GettingStartedGuide/avroschemas.html#avro-primitivedatatypes) 
Apache Avro.

| Загружаемый тип данных Avro | Логический тип данных
|:-|:-
| boolean | BOOLEAN
| string | VARCHAR (n)
| int | INT32
| long | BIGINT
| float | FLOAT
| double | DOUBLE
| (int) date | DATE
| (long) time-micros | TIME (precision)
| (long) timestamp-micros | TIMESTAMP (precision)

Значение типа данных (long) time-micros считается корректным, если лежит в интервале \[0; 86399999999\] микросекунд. 
Для значений этого типа данных, лежащих вне указанного интервала, успешная загрузка и дальнейшая корректная обработка 
не гарантируются.
{: .note-wrapper}