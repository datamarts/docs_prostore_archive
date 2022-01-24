﻿---
layout: default
title: Загрузка данных
nav_order: 3
parent: Работа с системой
has_children: true
has_toc: false
---

# Загрузка данных {#data_upload}

Система позволяет параллельно загружать большие объемы данных. Данные можно загружать только 
в [логические таблицы](../../overview/main_concepts/logical_table/logical_table.md).
Загрузка данных в [логические](../../overview/main_concepts/logical_view/logical_view.md)
и [материализованные представления](../../overview/main_concepts/materialized_view/materialized_view.md)
недоступна.

Под большим объемом данных подразумевается количество записей от нескольких сотен до нескольких миллионов. 
Для загрузки небольшого объема данных можно использовать функцию [обновления данных](../data_update/data_update.md).
{: .note-wrapper}

Данные загружаются [в виде сообщений Kafka](../../reference/upload_format/upload_format.md), поэтому для их загрузки 
нужен топик Kafka. Если в брокере сообщений Kafka настроено автоматическое создание топиков, 
то дополнительные действия не требуются. Иначе топик необходимо создать, если он отсутствует. Подробнее о создании 
топиков см. в документации Kafka:
*   раздел [Quick Start](https://kafka.apache.org/documentation/#quickstart),
*   раздел [Adding and removing topics](https://kafka.apache.org/documentation/#basic_ops_add_topic).

Чтобы загрузить данные из внешней информационной системы в логическую таблицу:
1.  Загрузите данные из внешней информационной системы в топик Kafka.  
    Данные должны иметь формат, описанный в разделе [Формат загрузки данных](../../reference/upload_format/upload_format.md).
2.  [Создайте](../../reference/sql_plus_requests/CREATE_TABLE/CREATE_TABLE.md) 
    логическую таблицу, если она еще не создана.
3.  [Создайте](../../reference/sql_plus_requests/CREATE_UPLOAD_EXTERNAL_TABLE/CREATE_UPLOAD_EXTERNAL_TABLE.md) 
    [внешнюю таблицу](../../overview/main_concepts/external_table/external_table.md) 
    загрузки, если она еще не создана.
4.  Выполните запрос [BEGIN DELTA](../../reference/sql_plus_requests/BEGIN_DELTA/BEGIN_DELTA.md) 
    на открытие [дельты](../../overview/main_concepts/delta/delta.md), 
    если она еще не открыта.
5.  Выполните запрос [INSERT INTO logical_table](../../reference/sql_plus_requests/INSERT_INTO_logical_table/INSERT_INTO_logical_table.md) 
    на загрузку данных из топика в логическую таблицу. В запросе нужно указать внешнюю таблицу загрузки, 
    определяющую параметры загрузки.
6.  Если необходимо, загрузите и (или) обновите другие данные.
    <br>В открытой дельте можно выполнить произвольное количество запросов на обновление и загрузку данных,
    а также [отменить изменения](../../reference/sql_plus_requests/ROLLBACK_DELTA/ROLLBACK_DELTA.md). 
    При этом не допускается добавление информации о различных состояниях одного объекта (то есть различных записей с 
    одинаковым первичным ключом) в одной дельте.
7.  Выполните запрос [COMMIT DELTA](../../reference/sql_plus_requests/COMMIT_DELTA/COMMIT_DELTA.md) 
    для сохранения изменений и закрытия дельты.
    
При успешном выполнении действий состояние данных системы обновляется, как описано в разделе 
[Версионирование данных](data_versioning/data_versioning.md).

Пока дельта не закрыта, изменения данных этой дельты можно отменить 
с помощью запроса [ROLLBACK DELTA](../../reference/sql_plus_requests/ROLLBACK_DELTA/ROLLBACK_DELTA.md). 
Созданные внешние таблицы загрузки можно использовать повторно или удалить.
{: .note-wrapper}

## Примеры {#examples}
```sql
-- выбор логической базы данных sales в качестве базы данных по умолчанию
USE sales;

-- создание логической таблицы sales
CREATE TABLE sales (
  id INT NOT NULL,
  transaction_date TIMESTAMP NOT NULL,
  product_code VARCHAR(256) NOT NULL,
  product_units INT NOT NULL,
  store_id INT NOT NULL,
  description VARCHAR(256),
  PRIMARY KEY (id)
)
DISTRIBUTED BY (id);

-- создание внешней таблицы загрузки
CREATE UPLOAD EXTERNAL TABLE sales_ext_upload (
  id INT,
  transaction_date TIMESTAMP,
  product_code VARCHAR(256),
  product_units INT,
  store_id INT,
  description VARCHAR(256)
)
LOCATION  'kafka://zk1:2181,zk2:2181,zk3:2181/sales'
FORMAT 'AVRO'
MESSAGE_LIMIT 1000;

-- открытие новой (горячей) дельты
BEGIN DELTA;

-- запуск загрузки данных в логическую таблицу sales
INSERT INTO sales SELECT * FROM sales.sales_ext_upload;

-- закрытие дельты (фиксация изменений)
COMMIT DELTA;
```