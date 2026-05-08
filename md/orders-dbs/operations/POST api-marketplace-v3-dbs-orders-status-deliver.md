# POST /api/marketplace/v3/dbs/orders/status/deliver

**Перевести сборочные задания в доставку{{ /api/marketplace/v3/dbs/orders/status/deliver }}**

теги: `Сборочные задания DBS`

**Полный путь:** `POST /api/marketplace/v3/dbs/orders/status/deliver`

## Описание

<span>Описание метода</span>

Метод переводит [сборочные задания](./orders-dbs#tag/Sborochnye-zadaniya-DBS) из [статуса](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1info/post) `confirm` в статус `deliver` — в доставке.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 10 запросов |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `ordersIds` — array<integer>. Список ID сборочных заданий

**Пример:**

```json
{
  "ordersIds": [
    123456,
    234567
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `requestId` — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `results` — array<$ref: api.StatusSetDeliverResponse>

```json
{
  "requestId": "03615778-eb9e-4f55-b4Of-fd3ac0fad2сc",
  "results": [
    {
      "orderId": 4299281547,
      "isError": true,
      "errors": [
        {
          "code": 404,
          "detail": "NotFound"
        }
      ]
    },
    {
      "orderId": 1234567890,
      "isError": true,
      "errors": [
        {
          "code": 409,
          "detail": "MetaValidationFail",
          "metaDetails": [
            {
              "key": "sgtin",
              "value": "0102900304495480215KE",
              "decision": "sgtinInvalidFormat"
            }
          ]
        }
      ]
    },
    {
      "orderId": 4279781545,
      "isError": false
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` — string; пример: `dbs-public-api`. ID внутреннего сервиса WB
- `requestId` — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "dbs-public-api",
  "requestId": "f1787bd2d1fdс35d6f537316514у4a05",
  "title": "IncorrectRequest"
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

#### 403 — Доступ запрещён

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` — string; пример: `dbs-public-api`. ID внутреннего сервиса WB
- `requestId` — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "dbs-public-api",
  "requestId": "f1787bd2d1fdс35d6f537316514у4a05",
  "title": "AccessDenied"
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
