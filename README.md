# Домашнее задание «Troubleshooting» — Лугинина Виктория

Исходный манифест:
https://raw.githubusercontent.com/netology-code/kuber-homeworks/main/3.5/files/task.yaml

Исправление: [web-consumer-fixed.yaml](./web-consumer-fixed.yaml)

## Проблема 1. Образ не скачивается

web-consumer использовал образ `radial/busyboxplus:curl`.
Новый containerd не поддерживает schema 1 манифесты.

Статус подов: ErrImagePull / ImagePullBackOff.

Что сделано: образ заменён на `wbitt/network-multitool`.

## Проблема 2. Не резолвится auth-db

После запуска в логах:
`curl: (6) Could not resolve host: auth-db`

web-consumer находится в namespace `web`.
Сервис `auth-db` находится в namespace `data`.
Короткое имя `auth-db` ищется только внутри своего namespace.

Что сделано: команда заменена на
`curl auth-db.data.svc.cluster.local`

## Результат

В логах web-consumer появилась страница nginx.
Приложение подключается к auth-db.

