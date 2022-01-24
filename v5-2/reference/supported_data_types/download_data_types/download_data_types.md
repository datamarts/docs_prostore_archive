---
layout: default
title: Выгружаемые типы данных Avro
nav_order: 3
parent: Поддерживаемые типы данных
grand_parent: Справочная информация
has_children: false
has_toc: false
---

# Выгружаемые типы данных Avro {#download_data_types}

Типы данных Avro, выгружаемые из системы, зависят от СУБД хранилища, из которой выгружаются данные. 
В таблице ниже для каждого [логического типа данных](../logical_data_types/logical_data_types.md) 
указаны выгружаемые типы данных Avro.

Подробнее о типах данных Avro см. в [официальной документации](https://docs.oracle.com/database/nosql-12.1.3.0/GettingStartedGuide/avroschemas.html#avro-primitivedatatypes) 
Apache Avro.

| Логический тип данных | Тип данных Avro, выгружаемый из ADB | Тип данных Avro, выгружаемый из ADG | Тип данных Avro, выгружаемый из ADQM | Тип данных Avro, выгружаемый из ADP
|:-|:-|:-|:-|:-
| BOOLEAN | boolean | boolean | int | boolean
| VARCHAR (n) | string | string | string | string
| UUID | string | string | string | string
| INT32 | int | int | int | int
| INT | long | long | long | long
| BIGINT | long | long | long | long
| DOUBLE | double | double | double | double
| FLOAT | float | float | float  | float
| DATE | int | int | int | int
| TIME (precision) | long | long | long | long
| TIMESTAMP (precision) | long | long | long | long