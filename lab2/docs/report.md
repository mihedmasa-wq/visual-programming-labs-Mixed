# Отчёт по лабораторной работе №2. Node-RED

## Краткое описание выполненного

В ходе лабораторной работы я освоила Node-RED как low-code инструмент для визуального программирования. Были выполнены следующие задачи:

1. **Установка и запуск Node-RED** — через npm (Ачивка 8). Docker не подошёл из-за проблем с WSL и виртуализацией на моём компьютере.
2. **Создание 12 потоков** (flow-01 ... flow-12), демонстрирующих работу с различными нодами:
   - Flow 01: Inject → Debug
   - Flow 02: Function node
   - Flow 03: Switch node
   - Flow 04: Change/Set node
   - Flow 05: Template node
   - Flow 06: HTTP Request node
   - Flow 07: MQTT с публичным брокером
   - Flow 08: GET-эндпоинты (REST API)
   - Flow 09: Dashboard (gauge + chart)
   - Flow 10: Telegram-бот
   - Flow 11: Чтение и запись файла
   - Flow 12: Работа с контекстом (flow context)
3. **Настройка Node-RED Projects + Git** (Ачивка 7) — автоматическая синхронизация потоков с GitHub.
4. **Создание документации** — `lab2/docs/api.md` с описанием GET-эндпоинтов.

## Использованные AI-промпты

В ходе работы я использовала следующие ключевые промпты:

- «Помоги установить Node-RED на Windows 10 без Docker, через npm»
- «Сгенерируй код для function node, который использует let/const, if/else, цикл for, массив и объект»
- «Как настроить switch node в Node-RED для ветвления по значению msg.payload.sum?»
- «Как настроить change node, чтобы установить msg.topic, msg.timestamp и msg.payload?»
- «Создай Mustache-шаблон для template node с полями name, group, lab»
- «Как настроить MQTT в Node-RED с публичным брокером HiveMQ?»
- «Как создать REST API с GET-эндпоинтами в Node-RED с path-параметрами и кодами 400/404?»
- «Настрой dashboard в Node-RED: gauge для температуры и chart для истории»
- «Как создать Telegram-бота в Node-RED с командой /start и echo-ответом?»
- «Как настроить запись и чтение файла в Node-RED через write file и read file?»
- «Как работать с flow context в Node-RED? Пример со счётчиком.»
- «Как настроить Node-RED Projects для автоматической синхронизации с Git?»

## Освоенные ноды

| Нода | Назначение |
|---|---|
| `inject` | Запуск потока (вручную или по таймеру) |
| `debug` | Отладка, просмотр сообщений |
| `function` | JavaScript-код для обработки сообщений |
| `switch` | Ветвление по условию |
| `change` | Изменение свойств сообщения (Set, Change, Delete, Move) |
| `template` | Формирование текста по Mustache-шаблону |
| `http request` | Отправка HTTP-запросов к внешним API |
| `http in` / `http response` | Создание API-эндпоинтов (REST API) |
| `mqtt in` / `mqtt out` | Публикация и подписка на MQTT |
| `file` (write/read) | Запись и чтение файлов на диск |
| `gauge` / `chart` | Dashboard: виджеты для визуализации данных |
| `telegram command` / `receiver` / `sender` | Telegram-бот |
| `flow context` / `global context` | Хранение данных между сообщениями |

## Способ установки, версии

- **Способ установки:** npm (Ачивка 8)
- **Node-RED version:** v5.0.7
- **Node.js version:** v24.21.0

**Почему npm, а не Docker:**
Docker Desktop требовал WSL 2 и виртуализацию, которые не удалось настроить на моём компьютере (ошибки `Virtualization support not detected` и `Запрошенная операция требует повышения`). Установка через npm разрешена заданием и заняла меньше места на диске (~250 МБ вместо ~4 ГБ).

## Скриншоты всех flow

Все скриншоты находятся в файле **`ТВП_лаб_2.docx`** (в корне репозитория) с оглавлением и подписями. Также они продублированы в папке **`lab2/screenshots/`**.

Ниже приведён список flow и соответствующих им файлов:

| № | Flow | Файл JSON |
|---|---|---|
| 1 | Inject → Debug | `flow-01-inject-debug.json` |
| 2 | Function | `flow-02-function.json` |
| 3 | Switch | `flow-03-switch.json` |
| 4 | Change | `flow-04-change.json` |
| 5 | Template | `flow-05-template.json` |
| 6 | HTTP Request | `flow-06-http-request.json` |
| 7 | MQTT | `flow-07-mqtt.json` |
| 8 | GET-эндпоинты | `flow-08-endpoints.json` |
| 9 | Dashboard | `flow-09-dashboard.json` |
| 10 | Telegram-бот | `flow-10-telegram.json` |
| 11 | Файлы | `flow-11-files.json` |
| 12 | Контекст | `flow-12-context.json` |

## Выводы

В ходе выполнения лабораторной работы я:
1. Освоила Node-RED как инструмент визуального программирования — научилась собирать потоки из нод, соединять их «проводами» и разворачивать (Deploy).
2. Научилась работать с базовыми нодами: `inject`, `debug`, `function`, `switch`, `change`, `template`.
3. Освоила продвинутые ноды: `http request`, `http in`/`http response` (REST API), `mqtt in`/`mqtt out`, `file` (write/read), `gauge`/`chart` (Dashboard), `telegram command`/`receiver`/`sender`.
4. Поняла, как создавать REST API с path-параметрами и обработкой ошибок (400, 404).
5. Научилась работать с контекстом (`flow context`) для хранения данных между сообщениями.
6. Настроила автоматическую синхронизацию Node-RED с Git через **Node-RED Projects** (Ачивка 7) — теперь все изменения в потоках коммитятся и пушатся на GitHub автоматически.
7. Поняла, как установить Node-RED через npm (Ачивка 8), когда Docker не подходит.

**Самым сложным** было настроить Docker Desktop и WSL — пришлось разбираться с виртуализацией и компонентами Windows. В итоге я выбрала npm, что оказалось проще и надёжнее.

**Самым интересным** было создание Telegram-бота и Dashboard с визуализацией данных в реальном времени (gauge + chart).

**Самым полезным** — настройка Node-RED Projects + Git, потому что теперь все потоки версионируются автоматически, и я могу видеть историю изменений.
