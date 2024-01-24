# Установка и настройка Prometheus, использование exporters

## Создание docker-compose

Создаем файл docker-compose.yml, который инициализирует запуск следующий контейнеров и объединяем их в одну сеть:

- wordpress
- postgres
- prometheus
- node_exporter
- blackbox
- grafana

## Создание файла настройки blackbox_exporter

Создаем файл настроек blackbox.yml, которым указываем по какому протоколу происходит проверка сторонних сервисов.

## Создание файлов настроек postgre_exporter

Создаем 2 файла настроек для конфигурирования exporter:
- postgres_exporter.env
- postgres_exporter.service

## Создание файлов настроек prometheus

Создаем файл настроек prometheus.yml, в котором указываем, какие job будут выполняться, периодичность опроса, path для сбора метрик.

## Развертывание окружения

Дополняем файл docker-compose.yml копированием в контейнеры созданных ранее файлов настроек для prometheus, blackbox_exporter, postgre_exporter и разворачиваем окружение.

## Настройка postgre_exporter

Заходим в контейнер postgres и выполняем следующие команды:

> apt-get update \
apt-get install wget -y \
apt-get install systemctl -y \
wget https://github.com/prometheus-community/postgres_exporter/releases/download/v0.15.0/postgres_exporter-0.15.0.linux-amd64.tar.gz \
tar -xf postgres_exporter-0.15.0.linux-*.tar.gz \
cp postgres_exporter-0.15.0.linux-*/postgres_exporter /usr/local/bin \
adduser --system postgres_exporter \
chown -R postgres_exporter /opt/postgres_exporter \
systemctl daemon-reload \
systemctl enable --now postgres_exporter

## Настройка grafana

Скачиваем шаблоны dashboards для exporters с [сайта](https://grafana.com/grafana/dashboards/), после чего:

- открываем grafana;
- в качестве источника данных указываем prometheus
- создаем dashboards, через импорт скаченных шаблонов.