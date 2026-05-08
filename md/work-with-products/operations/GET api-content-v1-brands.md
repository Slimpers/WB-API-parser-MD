# GET /api/content/v1/brands

**Бренды{{ /api/content/v1/brands }}**

теги: `Категории, предметы и характеристики`

**Полный путь:** `GET /api/content/v1/brands`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список брендов по ID предмета.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Сервисный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `subjectId` | query | integer; пример: `1234` | да | ID предмета |
| `next` | query | integer; пример: `1234` | нет | Параметр пагинации. Используйте значение `next` из ответа, чтобы получить следующий пакет данных |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `brands` **(required)** — array<object>
  - *(элементы)*
    - `id` **(required)** — integer; пример: `9007199254`. ID бренда
    - `logoUrl` **(required)** — string. URL логотипа бренда
    - `name` **(required)** — string; пример: `Brand`. Название бренда
- `next` — integer; пример: `1212`. Параметр пагинации. Укажите это значение в запросе, чтобы получить следующий пакет данных. Если поле отсутствует, вы получили все данные
- `total` **(required)** — integer; пример: `344534`. Общее количество брендов предмета

```json
{
  "brands": [
    {
      "id": 9007199254,
      "name": "Brand"
    }
  ],
  "next": 1212,
  "total": 344534
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `title` **(required)** — string. Заголовок ошибки
- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `requestId` **(required)** — string. Уникальный ID запроса
- `errors` — array<object>
  - *(элементы)*
    - `message` — string. Текст ошибки
    - `location` — string. Параметр, где произошла ошибка
    - `value`. Значение параметра, где произошла ошибка

*BrandsResponseBadRequest1:*

```json
{
  "title": "Bad Request",
  "detail": "validation failed",
  "origin": "brands-api",
  "requestId": "102d2641a932d61bed60649d6c99d80a",
  "errors": [
    {
      "message": "invalid integer",
      "location": "query.next",
      "value": "MTkxOTAzMQ=="
    }
  ]
}
```

*BrandsResponseBadRequest2:*

```json
{
  "title": "Bad Request",
  "detail": "validation failed",
  "origin": "brands-api",
  "requestId": "102d2641a932d61bed60649d6c99d80a",
  "errors": [
    {
      "message": "expected number >= 0",
      "location": "query.subjectId",
      "value": "-1"
    }
  ]
}
```

#### 401

**Content-Type:** `application/problem+json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки
- `code` — string. Внутренний код ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB
- `status` — number. HTTP статус-код
- `statusText` — string. Расшифровка HTTP статус-кода
- `timestamp` — string (date-time). Дата и время запроса

```json
{
  "title": "unauthorized",
  "detail": "token problem; token is malformed: could not base64 decode signature: illegal base64 data at input byte 84",
  "code": "07e4668e--a53a3d31f8b0-[UK-oWaVDUqNrKG]; 03bce=277; 84bd353bf-75",
  "requestId": "7b80742415072fe8b6b7f7761f1d1211",
  "origin": "s2s-api-auth-catalog",
  "status": 401,
  "statusText": "Unauthorized",
  "timestamp": "2024-09-30T06:52:38Z"
}
```

#### 404 — Не найдено

**Content-Type:** `application/problem+json`

- `title` **(required)** — string. Заголовок ошибки
- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `requestId` **(required)** — string. Уникальный ID запроса
- `errors` — array<object>
  - *(элементы)*
    - `message` — string. Текст ошибки
    - `location` — string. Параметр, где произошла ошибка
    - `value`. Значение параметра, где произошла ошибка

*BrandsResponseNotFound:*

```json
{
  "title": "Not Found",
  "detail": "Brands not found",
  "origin": "brands-api",
  "requestId": "102d2641a932d61bed60649d6c99d80a"
}
```

#### 429

**Content-Type:** `application/problem+json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки
- `code` — string. Внутренний код ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB
- `status` — number. HTTP статус-код
- `statusText` — string. Расшифровка HTTP статус-кода
- `timestamp` — string (date-time). Дата и время запроса

```json
{
  "title": "too many requests",
  "detail": "limited by c122a060-a7fb-4bb4-abb0-32fd4e18d489",
  "code": "07e4668e-ac2242c5c8c5-[UK-4dx7JUdskGZ]",
  "requestId": "9d3c02cc698f8b041c661a7c28bed293",
  "origin": "s2s-api-auth-catalog",
  "status": 429,
  "statusText": "Too Many Requests",
  "timestamp": "2024-09-30T06:52:38Z"
}
```
