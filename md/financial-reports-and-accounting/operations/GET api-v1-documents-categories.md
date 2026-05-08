# GET /api/v1/documents/categories

**Категории документов{{ /api/v1/documents/categories }}**

теги: `Документы`

**Полный путь:** `GET /api/v1/documents/categories`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает категории документов для получения [списка документов продавца](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1list/get).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 1 запрос | 10 сек | 5 запросов |
| Сервисный | 10 сек | 1 запрос | 10 сек | 5 запросов |
| Базовый | 24 ч | 1 запрос | 24 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `categories` — array<object>. Категории документов
    - *(элементы)*
      - `name` — string; пример: `redeem-notification`. ID категории документа из параметра [запроса](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1list/get) `category`
      - `title` — string; пример: `Уведомление о выкупе`. Название категории документа из поля [ответа](./financial-reports-and-accounting#tag/Dokumenty/~1api~1v1~1documents~1list/get) `category`

```json
{
  "data": {
    "categories": [
      {
        "name": "redeem-notification",
        "title": "Уведомление о выкупе"
      }
    ]
  }
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
