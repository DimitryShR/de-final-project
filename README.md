## Описание задачи
Необходимо собрать данные по транзакционной активности пользователей и настроить обновление таблицы с курсом валют. 
Цель — понять, как выглядит динамика оборота всей компании и что приводит к его изменениям. 

## Что сделать
Реализовать пайплайн обработки данных, поступающих из Kafka, с помощью Spark Streaming и полноценное хранилище
Хранилище должно быть реализовано на Vertica. 
После построения пайплайна обработки данных необходимо отдельно реализовать пайплайн формирования витрины с помощью Airflow и DAG. 
Необходимо также реализовать BI-аналитику для компании: подключиться из Metabase к Vertica и реализовать дашборд.

![Архитектура проекта](https://github.com/DimitryShR/de-final-project/blob/main/%D0%90%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0%20%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0.png)

## Структура проекта
- src\py - процедура чтения данных из Kafka с помощью Spark Streaming и пакетная загрузка во временное хранилище Postgres "as is" с хранением offset.
- src\dags\to_stg - dag и логика инкрементальной выгрузки данных из временного хранилища Postgres, обработки (парсинга) и загрузка чанками в stg слой Vertica
- src\dags\cmd - dag и логика инкрементальной загрузки данных в cmd слой
- src\dags\cmd\sql - SQL скрипт расчета витрины и импорта в целевую таблицу
- src\sql - скрипты создания таблиц (DDL)
- src\img - скрины реализованых BI-дашбордов

## PS
dds слой не реализовывался в виду объемности проекта и отсутствия требования со стороны обучающей организации
