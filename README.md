## Описание задачи
Необходимо собрать данные по транзакционной активности пользователей и настроить обновление таблицы с курсом валют. 

Цель — понять, как выглядит динамика оборота всей компании и что приводит к его изменениям. 

## Что сделано
1. Реализован пайплайн доставки данных из Kafka с помощью Spark Structured Streaming и пакетная загрузка во временное хранилище PostgreSQL "as is" с хранением offset.

2. Реализован пайплайн обработки и инкрементальной доставки данных чанками из промежуточного хранилища Postgres в Vertica с помощью Airflow и DAG. 

3. Реализован пайплайн инкрементальной доставки данных в cmd слой и формирования витрины с помощью Airflow и DAG. 

4. Реализован BI-дашборд в Metabase на данных из Vertica

![Архитектура проекта](https://github.com/DimitryShR/de-final-project/blob/main/%D0%90%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0%20%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0.png)

## Структура проекта
- src\py - процедура чтения данных из Kafka и загрузка в PostgreSQL
- dag и логика инкрементальной выгрузки данных из временного хранилища Postgres, обработки (парсинга) и загрузка чанками в stg слой Vertica
- src\dags\cmd - dag и логика инкрементальной загрузки данных в cmd слой
- src\dags\cmd\sql - SQL скрипт расчета витрины и импорта в целевую таблицу
- src\sql - скрипты создания таблиц (DDL)
- src\img - скрины реализованых BI-дашбордов

## PS
dds слой не реализовывался в виду объемности проекта и отсутствия требования со стороны обучающей организации
