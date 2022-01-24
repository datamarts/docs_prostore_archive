---
layout: default
title: Управление схемой данных
nav_order: 2
parent: Работа с системой
has_children: true
has_toc: false
---

# Управление схемой данных {#logical_schema_update}

Система позволяет организовать структуру данных с помощью [логической схемы данных](../../overview/main_concepts/logical_schema/logical_schema.md). 
Доступны следующие действия по управлению логической схемой данных:
*   [Создание логической базы данных](create_db/create_db.md)
*   [Удаление логической базы данных](drop_db/drop_db.md)
*   [Создание логической таблицы](create_table/create_table.md)
*   [Удаление логической таблицы](drop_table/drop_table.md)
*   [Создание логического представления](create_view/create_view.md)
*   [Изменение логического представления](alter_view/alter_view.md)
*   [Удаление логического представления](drop_view/drop_view.md)
*   [Создание материализованного представления](create_materialized_view/create_materialized_view.md)
*   [Удаление материализованного представления](drop_materialized_view/drop_materialized_view.md)
*   [Создание внешней таблицы загрузки](create_upload_table/create_upload_table.md)
*   [Удаление внешней таблицы загрузки](drop_upload_table/drop_upload_table.md)
*   [Создание внешней таблицы выгрузки](create_download_table/create_download_table.md)
*   [Удаление внешней таблицы выгрузки](drop_download_table/drop_download_table.md)
*   [Проверка наличия логической сущности](entity_presence_check/entity_presence_check.md)
*   [Запрос метаданных логической схемы](request_from_schema/request_from_schema.md)

Запросы на обновление логической схемы данных обрабатываются в порядке, описанном в разделе 
[Порядок обработки запросов на обновление логической схемы](../../overview/interactions/ddl_processing/ddl_processing.md).