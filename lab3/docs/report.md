# Отчёт по лабораторной работе №3. Bubble

**Студент:** Михед Мария
**Группа:** СДП-УИР-241
**Дата:** 16.10.2026
**Репозиторий:** https://github.com/mihedmasa-wq/visual-programming-labs-Mixed
**Dev-версия приложения:** https://bookfilm-list.bubbleapps.io/version-test?debug_mode=true

---

## 1. Краткое описание выполненного

В ходе лабораторной работы я освоила no-code платформу **Bubble** и создала веб-приложение **«ТВП: Михед — BookFilm List»** для ведения личного списка книг и фильмов.

Приложение позволяет пользователям:
- Регистрироваться и входить в личный кабинет.
- Добавлять книги и фильмы в свою коллекцию (Create).
- Просматривать каталог с фильтрацией по типу, жанру и статусу (Read).
- Редактировать записи (Update).
- Удалять записи (Delete).
- Искать книги и фильмы по названию, автору/режиссёру и жанру.
- Оставлять отзывы и оценки к прочитанному/просмотренному.

Работа выполнена в **6 частей** согласно заданию:
1. Промпт и генерация AI-каркаса приложения.
2. Исследование Build Guides и применение идеи (Search functionality).
3. Ручная доработка UI (заголовок, Global Variable, стиль, готовый компонент).
4. Проектирование базы данных и реализация полного CRUD (создание сущности `Отзыв` + workflows).
5. Ачивка (API Connector / Plugins).
6. Отчёт и подготовка к защите.

Все действия зафиксированы коммитами в Git-репозитории (не менее 4 коммитов — у меня их больше 15).

---

## 2. Промпт для AI-агента Bubble (Часть 1, дословно)

Промпт, который я вставила в AI-агента Bubble:
Создай приложение на тему «Список книг / фильмов». Пусть этот сайт будет требующий регистрацию. Страницу обязательно создай по структуре header + body + footer. Обязательно укажи в заготовке следующую строку: «ТВП: Михед». Добавь несколько интерактивных элементов (реализующих CRUD).


**Скриншоты:**
- `screenshots/01a-prompt-plan.png` и `screenshots/01b-prompt-plan.png`— план приложения, сгенерированный AI (Features, CRUD, ТВП: Михед).
- `screenshots/01-prompt.png` — готовое приложение после генерации (header + body + footer, строка «ТВП: Михед»).

---

## 3. AI-промпты, использованные в работе (дословно)

В ходе работы я использовала следующие ключевые промпты:

### 3.1. Промпт для генерации каркаса приложения (Часть 1)

Создай приложение на тему «Список книг / фильмов». Пусть этот сайт будет требующий регистрацию. Страницу обязательно создай по структуре header + body + footer. Обязательно укажи в заготовке следующую строку: «ТВП: Михед». Добавь несколько интерактивных элементов (реализующих CRUD).

### 3.2. Промпт для Build Guides (Часть 2)

В поле «Describe your app idea» на странице Build Guides я ввела:
Book and film tracker app where users can add, edit, delete and rate their favorite books and movies

### 3.3. Промпт для добавления Search functionality (Часть 2)

В AI-агент Bubble (поле «What should we build next?»):
Add a search bar that filters books and films by title, author/director, and genre

### 3.4. Промпт для создания новой сущности `Отзыв` (Часть 4.1)
Предложи структуру данных для сущности "Отзыв" (Review) в приложении-трекере книг и фильмов. Нужно минимум 4 поля разных типов (текст, число, дата, да/нет). Свяжи отзыв с книгой/фильмом и пользователем.


**Результат:** AI создал Data Type `Отзыв` с полями:
- `Автор` (User)
- `Дата отзыва` (date)
- `Запись` (Запись — ссылка на книгу/фильм)
- `Оценка` (number)
- `Рекомендую` (yes/no)
- `Текст отзыва` (text)

---

## 4. Освоенные элементы и workflows

### 4.1. Элементы Bubble

| Элемент | Где использован |
|---|---|
| **Header / Body / Footer** | Структура всех страниц |
| **Text** | Заголовки, тексты отзывов |
| **Button** | «Добавить отзыв», «Сохранить», «Редактировать», «Удалить» |
| **Input** | Поля формы (Текст отзыва, Оценка) |
| **Checkbox** | Флаг «Рекомендую» |
| **Repeating Group** | Список отзывов на странице `reviews` |
| **Popup** | Форма создания/редактирования отзыва |
| **Group** | Контейнеры для компоновки |

### 4.2. Data Types (сущности)

| Data Type | Поля |
|---|---|
| `User` | Встроенный (email, Name) |
| `Запись` (Book/Film) | Title, Author/Director, Genre, User |
| `Отзыв` (Review) | Автор, Дата отзыва, Запись, Оценка, Рекомендую, Текст отзыва, Creator, Created Date, Modified Date, Slug |

### 4.3. Workflows (CRUD)

| Операция | Workflow | Скриншот |
|---|---|---|
| **Create** | Кнопка «Сохранить» → `Create a new thing` (Отзыв) с условием `editing_review is empty` | `08-workflow-create.png` |
| **Read** | Repeating Group с Data source `Search for Отзывs` | `08a-reviews-ui.png` |
| **Update** | Кнопка «Редактировать» → `Set state (editing_review)` + `Show Popup`; кнопка «Сохранить» → `Make changes to a thing` с условием `editing_review is not empty` | `09-workflow-update.png` |
| **Delete** | Кнопка «Удалить» → `Delete a thing (Current cell's Отзыв)` | `10-workflow-delete.png` |

### 4.4. Global Variables и стили

- **Global Variable `primary-color`** (жёлтый) — используется для фона кнопок и акцентов.
- **Стиль `primary-style`** — создан для элементов Link/Text, использует переменную `primary-color`.

---

## 5. Скриншоты всех шагов

### 5.1. Часть 1 — Промпт и генерация каркаса

| Файл | Что на нём |
|---|---|
| `screenshots/01/01a-prompt-plan.png` | План приложения от AI (Features, CRUD, ТВП: Михед) |
| `screenshots/01/01b-prompt-plan.png` | Продолжение плана от AI |
| `screenshots/01/01-prompt.png` | Готовое приложение после генерации (header + body + footer) |

### 5.2. Часть 2 — Build Guides и Search functionality

| Файл | Что на нём |
|---|---|
| `screenshots/02/02-buildguide-prompt.png` | Поле «Describe your app idea» с промптом |
| `screenshots/02/02-buildguide-features.png` | Список Features (Rating, Search, CRUD и т.д.) |
| `screenshots/02/02-buildguide-search.png` | Build Guide «Search functionality» с шагами 1–5 |
| `screenshots/02-buildguide-after.png`+ `screenshots/02-buildguide-after_1.png`+ `screenshots/02-buildguide-after_2.png`+`screenshots/02-buildguide-after_3.png` | Приложение ПОСЛЕ (с полем поиска) |
| `screenshots/02/02-buildguide-AI-help.png` | Поле «Describe your app idea» с промптом |
| `screenshots/02/02-buildguide-AI-help_1.png` | Список Features (Rating, Search, CRUD и т.д.) |

### 5.3. Часть 3 — Ручная доработка UI

| Файл | Что на нём |
|---|---|
| `screenshots/03-global-variable.png` | Изменённый заголовок с фамилией и именем + Global Variable `primary-color` в редакторе |
| `screenshots/03-style.png` | Стиль `primary-style` с использованием переменной |
| `screenshots/04-style.png` | Стиль `primary-style` |
| `screenshots/03-component.png` | Готовый компонент «Отзывы читателей» на странице |

### 5.4. Часть 4.1 — Data Type и записи

| Файл | Что на нём |
|---|---|
| `screenshots/04/06-data-type.png` | Data Type `Отзыв` с полями |
| `screenshots/04/07-data-records.png` | 3 записи в App Data для `Отзыв` |
| `screenshots/04/04-data-final.png` | Финальное состояние App Data |
| `screenshots/04/04-data-after-crud.png` | App Data после CRUD-операций |

### 5.5. Часть 4.2 — UI страницы `reviews`

| Файл | Что на нём |
|---|---|
| `screenshots/04/настройки кнопок и preview/08a-reviews-ui.png` | Основной UI страницы `reviews` с Repeating Group |
| `screenshots/04/настройки кнопок и preview/08b-reviews-popup.png` | Popup с формой создания/редактирования |

### 5.6. Часть 4.2 — Workflows CRUD

| Файл | Что на нём |
|---|---|
| `screenshots/04/08-workflow-create.png` | **Workflow Create (обязательный)** |
| `screenshots/04/08-workflow-create_new.png` | Workflow Create (вариант) |
| `screenshots/04/09-workflow-update.png` | **Workflow Update (обязательный)** |
| `screenshots/04/10-workflow-delete.png` | **Workflow Delete (обязательный)** |
| `screenshots/04/настройки кнопок и preview/08c-workflow-show-popup.png` | Workflow кнопки «Добавить отзыв» (Show Popup) |
| `screenshots/04/настройки кнопок и preview/08e-workflow-add-button.png` | Workflow кнопки «Добавить отзыв» (Reset + Set state) |
| `screenshots/04/настройки кнопок и preview/08f-custom-state.png` | Создание Custom State `editing_review` |
| `screenshots/04/настройки кнопок и preview/08g-input-initial-content.png` | Initial content для Input Text |
| `screenshots/04/настройки кнопок и preview/08h-input-text-dynamic.png` | Текст отзыва = `editing_review's Текст отзыва` |
| `screenshots/04/настройки кнопок и preview/08i-input-rating-dynamic.png` | Оценка = `editing_review's Оценка` |
| `screenshots/04/настройки кнопок и preview/08j-checkbox-dynamic.png` | Dynamic status для Checkbox «Рекомендую» |
| `screenshots/04/настройки кнопок и preview/09a-workflow-edit-button.png` | Workflow кнопки «Редактировать» (Set state) |

### 5.7. Preview (Read/Update/Delete)

| Файл | Что на нём |
|---|---|
| `screenshots/04/настройки кнопок и preview/04-preview-read-1.png` | Preview — 1-я карточка |
| `screenshots/04/настройки кнопок и preview/04-preview-read-2.png` | Preview — 2-я карточка |
| `screenshots/04/настройки кнопок и preview/04-preview-read-3.png` | Preview — 3-я карточка |
| `screenshots/04/настройки кнопок и preview/09b-preview-before-edit.png` | Preview ДО редактирования |
| `screenshots/04/настройки кнопок и preview/09c-preview-popup-filled.png` | Popup с заполненными данными |
| `screenshots/04/настройки кнопок и preview/09d-preview-after-edit.png` | Preview ПОСЛЕ редактирования |
| `screenshots/04/настройки кнопок и preview/10a-preview-after-delete.png` | Preview ПОСЛЕ удаления |


## 5. Выводы

В ходе выполнения лабораторной работы я:

1. **Освоила Bubble как no-code платформу** — научилась создавать веб-приложения без написания кода, используя визуальный редактор.

2. **Научилась использовать AI-агента Bubble** для генерации каркаса приложения по промпту. AI создал структуру header + body + footer, страницу с CRUD-элементами и базой данных.

3. **Изучила Build Guides** и применила одну из идей (Search functionality) в своём приложении. Это показало, как Bubble помогает с персонализированными рекомендациями.

4. **Освоила ручную доработку UI:**
   - Изменение заголовка.
   - Создание Global Variable для цвета (`primary-color`).
   - Создание стиля (`primary-style`), использующего переменную.
   - Использование готовых компонентов (Testimonials).

5. **Спроектировала базу данных** — создала Data Type `Отзыв` с 6 полями разных типов (User, date, link, number, yes/no, text) и 3 записи.

6. **Реализовала полный CRUD** для сущности `Отзыв`:
   - **Create** — форма в Popup, кнопка «Сохранить» создаёт запись.
   - **Read** — Repeating Group показывает список отзывов.
   - **Update** — кнопка «Редактировать» открывает Popup с данными; кнопка «Сохранить» обновляет запись через Custom State `editing_review`.
   - **Delete** — кнопка «Удалить» удаляет запись.

7. **Настроила Privacy Rules** для Data Type `Отзыв` — чтобы записи были видны всем пользователям (Find in searches + View).

8. **Освоила Custom States** — использовала `editing_review` для передачи данных между кнопкой «Редактировать» и Popup.

9. **Научилась работать с Git** — делала осмысленные коммиты после каждого шага (всего более 15 коммитов).

**Самым сложным** было:
- Настройка Custom State для передачи данных в Popup (Display data не работал, потому что у Popup нет Data Type).
- Настройка Privacy Rules — без них записи не отображались в Repeating Group.

**Самым интересным** было:
- Использование AI-агента Bubble — он сгенерировал каркас приложения за 10 минут.
- Реализация полного CRUD через визуальный редактор workflows.

**Самым полезным** стало понимание того, как no-code платформы позволяют быстро создавать полноценные веб-приложения с базой данных, аутентификацией и CRUD-операциями — без написания классического кода.

---

## 6. Список коммитов в репозитории

Все действия фиксировались коммитами с осмысленными сообщениями. Всего в репозитории более 13 коммитов по лабораторной работе №3.

**История коммитов:**

![История коммитов](screenshots/11-git-history.png)

*Рис. 11. История коммитов в репозитории (команда `git log --oneline --decorate`)*

Основные коммиты:
- `Lab3: create folder structure` — создание структуры папок
- `Lab3: add AI prompt plan screenshot` — план от AI
- `Lab3: AI prompt screenshot` — скриншот промпта в лучшем качестве
- `Lab3: add prompt_1 screen` — добавление скриншотов промптов
- `Lab3: add prompt_2 and _3 screen` — Build Guides скриншоты
- `Lab3: Build Guides research and Search functionality applied` — Часть 2
- `Lab3: Part 2 - распределила скрины по папкам` — организация скриншотов
- `Lab3: Part 3 - добавлены все скрины` — Часть 3 (UI доработки)
- `Lab3: Part 4 - all screens добавлены` — Часть 4
- `Lab3: Part 4 - screen's names изменены` — переименование скриншотов
- `Lab3: Part 4 - внесла изменения в папку 04` — правки
- `Lab3: create folder structure` — финальная структура
- `Lab3: Part 3 - добавила скрин по style` — последний коммит по стилю
- `Lab3: Part 3 - добавилен report` 
