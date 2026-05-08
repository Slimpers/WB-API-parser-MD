# POST /api/marketplace/v3/click-collect/orders/status/prepare

**Сообщить, что сборочные задания готовы к выдаче{{ /api/marketplace/v3/click-collect/orders/status/prepare }}**

теги: `Сборочные задания Самовывоз`

**Базовый URL:** `https://marketplace-api.wildberries.ru`

**Полный путь:** `POST https://marketplace-api.wildberries.ru/api/marketplace/v3/click-collect/orders/status/prepare`

## Описание

<span>Описание метода</span>

Метод переводит [сборочные задания](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz) из [статуса](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1info/post) `confirm` — на сборке — в статус `prepare` — готово к выдаче.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий Самовывоз</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 10 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

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

- `requestId` **(required)** — пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `results` **(required)** — array<$ref: api.StatusSetResponse>

```json
{
  "requestId": "03615778-eb9e-4f55-b4O4-fd3ac0fad2сc",
  "results": [
    {
      "orderId": 123456,
      "isError": true,
      "errors": [
        {
          "code": 404,
          "detail": "NotFound"
        }
      ]
    },
    {
      "orderId": 234567,
      "isError": false
    }
  ]
}
```

#### 400

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` **(required)** — string; пример: `market-public-api`. ID внутреннего сервиса WB
- `requestId` **(required)** — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` **(required)** — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "market-public-api",
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

#### 403

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` **(required)** — string; пример: `market-public-api`. ID внутреннего сервиса WB
- `requestId` **(required)** — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` **(required)** — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "market-public-api",
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
