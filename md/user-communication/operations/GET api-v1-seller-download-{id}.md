# GET /api/v1/seller/download/{id}

**Получить файл из сообщения{{ /api/v1/seller/download/{id} }}**

теги: `Чат с покупателями`

**Полный путь:** `GET /api/v1/seller/download/{id}`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает файл или изображение из сообщения по его ID.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Сервисный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Базовый | 1 ч | 10 запросов | 6 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `id` | path | string | да | ID файла, см. значение поля `downloadID` в методе [События чатов](./user-communication#tag/Chat-s-pokupatelyami/paths/~1api~1v1~1seller~1events/get) |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/pdf`

- string (binary)
**Content-Type:** `image/jpeg`

- string (binary)
**Content-Type:** `image/png`

- string (binary)

#### 202 — Файл на модерации

**Content-Type:** `application/json`

- `moderationState` **(required)** — string; пример: `pending`. Статус модерации
- `retrySeconds` **(required)** — integer; пример: `30`. Секунд до следующей попытки запроса файла

```json
{
  "moderationState": "pending",
  "retrySeconds": 30
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `status` — number. HTTP статус-код
- `title` — string. Заголовок ошибки
- `origin` — string. ID внутреннего сервиса WB
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `error` — string. Текст ошибки

*IncorrectNextParameter:*

```json
{
  "status": 400,
  "title": "invalid fileID",
  "origin": "proxy-chats",
  "detail": "invalid fileID",
  "requestId": "62f59a4ce21064f20b1bbc28c85f38d8",
  "error": "invalid fileID"
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

#### 402

**Content-Type:** `application/problem+json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки. Ошибка возвращается только сервисам из [Каталога решений для бизнеса](https://dev.wildberries.ru/business-solutions)

```json
{
  "title": "payment required",
  "detail": "wb solution for business has insufficient funds on its balance. please top up the balance in the company's personal account https://dev.wildberries.ru/company"
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

#### 451 — Файл не прошёл модерацию

**Content-Type:** `application/problem+json`

- `status` — integer; пример: `451`. HTTP статус-код
- `title` — string; пример: `Unavailable for Legal Reasons`. Заголовок ошибки
- `origin` — string; пример: `proxy-chats`. ID внутреннего сервиса WB
- `detail` — string; пример: `moderation error`. Детали ошибки
- `requestId` — string; пример: `62f59a4ce21064f20b1bbc28c85f38d8`. ID запроса

```json
{
  "status": 451,
  "title": "Unavailable for Legal Reasons",
  "origin": "proxy-chats",
  "detail": "moderation error",
  "requestId": "62f59a4ce21064f20b1bbc28c85f38d8"
}
```
