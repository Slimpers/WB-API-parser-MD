# POST /api/v1/seller/message

**Отправить сообщение{{ /api/v1/seller/message }}**

теги: `Чат с покупателями`

**Полный путь:** `POST /api/v1/seller/message`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод отправляет сообщения в [чат с покупателем](./user-communication#tag/Chat-s-pokupatelyami/paths/~1api~1v1~1seller~1chats/get).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Сервисный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `multipart/form-data`

- `replySign` **(required)** — string. Подпись чата. Можно получить из [информации по чату](./user-communication#tag/Chat-s-pokupatelyami/paths/~1api~1v1~1seller~1chats/get) или [данных события](./user-communication#tag/Chat-s-pokupatelyami/paths/~1api~1v1~1seller~1events/get), если в событии есть поле `"isNewChat": true`.
- `message` — string. Текст сообщения. Максимум 1000 символов.
- `file` — array<string (binary)>. Файлы, формат JPEG, PDF или PNG, максимальный размер — 5 Мб каждый. Максимальный суммарный размер файлов — 30 Мб.

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `errors` — array<string>. Ошибки загрузки файлов, если есть
- `result` — object
  - `addTime` — integer (Unix Timestamp в миллисекундах). Дата и время создания чата
  - `chatID` — string. ID чата
  - `sign` — string. Подпись чата

```json
{
  "result": {
    "addTime": 1712848270018,
    "chatID": "1:641b623c-5c0e-295b-db03-3d5b4d484c32"
  },
  "errors": []
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `status` — number. HTTP статус-код
- `title` — string. Заголовок ошибки
- `origin` — string. ID внутреннего сервиса WB
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `error` — string. Текст ошибки

*InvalidSignature:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "Invalid signature",
  "requestId": "1b21cad4833a0c9244dc294a000f6149",
  "error": "Invalid signature"
}
```

*InvalidFileSize:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "A24FA09844E: attachment too big. Max size: 5MiB",
  "requestId": "1b21cad4833a0c9244dc294a000f6149",
  "error": "A24FA09844E: attachment too big. Max size: 5MiB"
}
```

*UnsupportedFilesType:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "4A9F2544E29: \"video_2023-07-25_10-54-09.mp4\" has unsupported mime type",
  "requestId": "1b21cad4833a0c9244dc294a000f6149",
  "error": "4A9F2544E29: \"video_2023-07-25_10-54-09.mp4\" has unsupported mime type"
}
```

*InvalidMessage:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "Invalid value for \"message\"",
  "requestId": "1b21cad4833a0c9244dc294a000f6149",
  "error": "Invalid value for \"message\""
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
