---
layout: default
title: Настройка JSON-логов
nav_order: 4
parent: Эксплуатация
has_children: false
---

# Настройка JSON-логов {#json_logs_configuration}

Система поддерживает конфигурацию и отображение JSON-логов проекта [Logback](http://logback.qos.ch/index.html). 
Помимо [стандартных параметров](http://logback.qos.ch/manual/configuration.html), таких как время 
сообщения, уровень логирования и т.д., система позволяет отображать в логах уникальные идентификаторы запросов.

Если отображение идентификаторов настроено, для каждого [запроса SQL+](../../reference/sql_plus_requests/sql_plus_requests.md) 
отображается уникальный идентификатор, для внутреннего запроса системы — значение `no_id`.

Чтобы настроить отображение идентификаторов запросов в логах, отредактируйте файл _logback.xml_ (полный пример файла 
см. [ниже](#ex_logback)):

1. Перед объявлением `appender` добавьте строки:

    ```xml
    <conversionRule conversionWord="vcl"
                converterClass="io.reactiverse.contextual.logging.LogbackConverter"/>
    ```

2. В секцию `appender.providers.pattern` добавьте строку:

    ```xml
    "requestId": "%vcl{requestId:-no_id}"
    ```

<a id="ex_logback"></a>
Ниже показан пример файла _logback.xml_ с включенным отображением идентификаторов запросов:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <conversionRule conversionWord="vcl"
                    converterClass="io.reactiverse.contextual.logging.LogbackConverter"/>

    <appender name="rollingFile" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>logs/application.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- daily rollover -->
            <fileNamePattern>logs/application.%d{yyyy-MM-dd}.log.gz</fileNamePattern>
            <!-- keep 30 days' worth of history capped at 3GB total size -->
            <maxHistory>7</maxHistory>
            <totalSizeCap>3GB</totalSizeCap>
        </rollingPolicy>
        <encoder class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">
            <providers>
                <pattern>
                    <omitEmptyFields>true</omitEmptyFields>
                    <pattern>
                        {
                        "timestamp": "%date{ISO8601}",
                        "logger": "%logger",
                        "level": "%level",
                        "thread": "%thread",
                        "requestId": "%vcl{requestId:-no_id}",
                        "message": "%message"
                        }
                    </pattern>
                </pattern>
                <stackTrace>
                    <throwableConverter class="net.logstash.logback.stacktrace.ShortenedThrowableConverter">
                        <maxDepthPerThrowable>30</maxDepthPerThrowable>
                        <maxLength>2048</maxLength>
                        <shortenedClassNameLength>20</shortenedClassNameLength>
                        <exclude>^sun\.reflect\..*\.invoke</exclude>
                        <exclude>^net\.sf\.cglib\.proxy\.MethodProxy\.invoke</exclude>
                        <rootCauseFirst>true</rootCauseFirst>
                    </throwableConverter>
                </stackTrace>
            </providers>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="rollingFile" />
    </root>
</configuration>
```
