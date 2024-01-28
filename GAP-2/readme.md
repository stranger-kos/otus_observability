# Отказоустойчивость Prometheus, хранилища метрик для Prometheus

## Создание docker-compose

для развертывания Thanos берем файл docker-compose.yml из предыдущего задания и добавляем дополнительные компоненты:

- thanos-sidecar
- thanos-query
- thanos-query-frontend
- thanos-store-gateway
- thanos-compactor
- minio.

После развертывания контенйеров переходим по ссылке http://localhost:9091, и получаем UI-Thanos для выборки данных по необходимым метрикам. 