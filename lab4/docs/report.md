# Отчет по лабораторной работе №4 (n8n)

## Краткое описание выполненного
В ходе работы я освоила платформу n8n как low-code инструмент для автоматизации. Я установила n8n локально через npm (так как Docker не использовался), изучила базовые ноды (Manual Trigger, Set, Code, IF, HTTP Request, Schedule Trigger) и создала 6 рабочих процессов (workflow). Также я начала изучение Redis, но из-за технических ограничений WSL на моей системе эта часть была пропущена по согласованию с преподавателем.

## Какие AI-промпты использовались
1. *«Как установить n8n без Docker на Windows?»* — помогло выбрать путь через npm.
2. *«Как написать код на JavaScript в узле Code, чтобы использовать let, const, if/else и цикл for?»* — использовалось для создания flow-02 и flow-03.
3. *«Как настроить HTTP Request для получения случайного факта о котах?»* — подсказка по URL и методу.
4. *«Как настроить Schedule Trigger на запуск каждую минуту?»* — инструкция по параметрам.
5. *«Как исправить ошибку UtilAcceptVsock при установке WSL?»* — попытка решить проблему с Redis.

## Какие ноды освоены
* **Manual Trigger** — ручной запуск.
* **Set (Edit Fields)** — создание и изменение полей данных.
* **Code** — выполнение JavaScript (работа с массивами, объектами, циклами).
* **IF** — условное ветвление.
* **HTTP Request** — отправка GET-запросов к внешним API.
* **Schedule Trigger** — запуск по расписанию.
* **NoOp** — заглушка для завершения ветки.

## Скриншоты всех workflow

### 1. Установка n8n
![Версия n8n](screenshots/01-install/01-version-n8n.png)
![Регистрация](screenshots/01-install/02-registration.png)
![Опросник](screenshots/01-install/03-setup-survey.png)

Дополнительные скриншоты процесса установки:
![Установка npm](screenshots/01-install/установка/04-npm-install.png)
![Завершение npm](screenshots/01-install/установка/05-npm-finish.png)
![Запуск в PowerShell](screenshots/01-install/установка/06-powershell-start.png)

### 2.1. Manual Trigger - Set - Code
![Схема workflow](screenshots/02-workflows/02.1-manual-set/01-workflow-canvas.png)
![Настройки Set](screenshots/02-workflows/02.1-manual-set/02-set-node-settings.png)
![Результат Code](screenshots/02-workflows/02.1-manual-set/03-code-node-result.png)

Дополнительные скриншоты добавления узлов:
![Manual Trigger](screenshots/02-workflows/02.1-manual-set/добавление узлов/04-manual-trigger-node.png)
![Set](screenshots/02-workflows/02.1-manual-set/добавление узлов/05-set-node-added.png)
![Code](screenshots/02-workflows/02.1-manual-set/добавление узлов/06-code-node-added.png)

### 2.2. Code node (JS)
![Схема workflow](screenshots/02-workflows/02.2-code/01-workflow-canvas.png)
![Настройки Code (часть 1)](screenshots/02-workflows/02.2-code/02-code-settings.png)
![Настройки Code (часть 2)](screenshots/02-workflows/02.2-code/03-code-settings.png)
![Результат NoOp](screenshots/02-workflows/02.2-code/04-noop-result.png)

### 2.3. IF node
![Схема workflow](screenshots/02-workflows/02.3-if/01-workflow-canvas.png)
![Настройки IF](screenshots/02-workflows/02.3-if/02-if-settings.png)
![Меню выбора оператора](screenshots/02-workflows/02.3-if/03-if-operator-menu.png)

### 2.4. Set node (изменение полей)
![Схема workflow](screenshots/02-workflows/02.4-set/01-workflow-canvas.png)
![Настройки Set](screenshots/02-workflows/02.4-set/02-set-settings.png)
![Результат Code](screenshots/02-workflows/02.4-set/03-code-result.png)

### 2.5. HTTP Request node
![Схема workflow](screenshots/02-workflows/02.5-http/01-workflow-canvas.png)
![Настройки HTTP Request](screenshots/02-workflows/02.5-http/02-http-settings.png)
![Результат Code](screenshots/02-workflows/02.5-http/03-code-result.png)

### 2.6. Schedule Trigger
![Схема workflow](screenshots/02-workflows/02.6-schedule/01-workflow-canvas.png)
![Настройки Schedule](screenshots/02-workflows/02.6-schedule/02-schedule-settings.png)
![Результат Code](screenshots/02-workflows/02.6-schedule/03-code-result.png)

## Выводы
В ходе выполнения лабораторной работы я научилась создавать автоматизированные сценарии в n8n. Самым интересным было работать с узлом Code, так как он позволяет использовать JavaScript для гибкой обработки данных. Узел IF показал, как строить логические ветвления. HTTP Request дал понимание, как интегрировать внешние API. Я также поняла, как работает Schedule Trigger для фоновых задач.

**Сравнение с Node-RED:**
Работа с n8n показалась мне знакомой, так как ранее я изучала Node-RED. Обе платформы используют визуальное программирование на основе потоков данных (flow-based programming). В n8n, как и в Node-RED, есть узлы (nodes), которые соединяются стрелками, и данные передаются от одного узла к другому в формате JSON. Это сделало освоение n8n интуитивно понятным и быстрым.

**Разница с Node-RED:**
1. **Визуальный стиль:** n8n выглядит более современно и минималистично, в то время как Node-RED имеет более классический "инженерный" интерфейс.
2. **Работа с данными:** В n8n узлы часто оперируют массивами объектов (items), что удобно для пакетной обработки. В Node-RED акцент сделан на передаче одного сообщения (msg) через поток.
3. **Экосистема:** n8n имеет больше встроенных интеграций с бизнес-сервисами (Google, Slack, CRM), тогда как Node-RED больше ориентирован на IoT и работу с оборудованием.

**Почему пропущена Часть 3 (Redis) и Ачивки:**
Для выполнения задания требовалось установить Redis. Так как Docker на моей машине не использовался, я попыталась установить Redis через WSL (Windows Subsystem for Linux). Однако при установке дистрибутива Ubuntu возникла критическая ошибка виртуализации (`UtilAcceptVsock: accept4 failed 110`), которая не позволила завершить установку. По согласованию с преподавателем, Часть 3 и Ачивки были пропущены ввиду невозможности выполнить их в текущих условиях.