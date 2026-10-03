# API Documentation — Lab 2

## 1. GET /api/text

Возвращает простой текст.

**Пример запроса:**
GET http://localhost:1880/api/text

**Пример ответа:**
Привет! Это простой текстовый ответ из Node-RED. Студент: Михед.

---

## 2. GET /api/info

Возвращает JSON с информацией о студенте и лабораторной.

**Пример запроса:**
GET http://localhost:1880/api/info

**Пример ответа:**
{
    "student": "Михед",
    "lab": 2,
    "status": "OK"
}

---

## 3. GET /api/items/:id

Возвращает информацию о предмете по его ID.

**Path-параметры:**
- `id` (обязательный) — числовой ID предмета.

**Query-параметры:**
- `limit` (опциональный) — количество элементов. По умолчанию 10.

**Успешный запрос:**
GET http://localhost:1880/api/items/42?limit=5

**Успешный ответ (200):**
{
    "status": "success",
    "itemId": 42,
    "limit": 5,
    "items": [
        {"id": 42, "name": "Item 42"}
    ]
}

**Ошибка 400 (Bad Request):**
GET http://localhost:1880/api/items/abc

{
    "status": "error",
    "message": "ID must be a number",
    "code": 400
}

**Ошибка 404 (Not Found):**
GET http://localhost:1880/api/items/999

{
    "status": "error",
    "message": "Item not found",
    "code": 404
}