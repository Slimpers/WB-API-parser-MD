# POST /api/marketplace/v3/orders/meta

**Получить метаданные сборочных заданий{{ /api/marketplace/v3/orders/meta }}**

теги: `Метаданные FBS`

**Полный путь:** `POST /api/marketplace/v3/orders/meta`

## Описание

<span>Описание метода</span>

Метод возвращает метаданные [сборочных заданий](./orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) по списку их ID.

Перечень метаданных, доступных для сборочного задания, можно получить в [списке новых сборочных заданий](./orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1new/get), поля `requiredMeta` и `optionalMeta`.

Возможные метаданные:
  - `imei` — [IMEI](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1imei/put)
  - `uin` — [УИН](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1uin/put)
  - `gtin` — [GTIN](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1gtin/put)
  - `sgtin` — [код маркировки Честного знака](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1sgtin/put)
  - `expiration` — [срок годности товара](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1expiration/put)
  - `customsDeclaration` — [номер ГТД](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1marketplace~1v3~1orders~1%7BorderId%7D~1meta~1customs-declaration/put)

Если в ответе не вернулись какие-либо из объектов метаданных, значит, у сборочного задания не может быть таких метаданных — и добавить их нельзя.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов <strong>получения и удаления метаданных FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

ID сборочных заданий
- `orders` **(required)** — array<integer>

**Пример:**

```json
{
  "orders": [
    123456,
    234567,
    345678
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<$ref: v3.OrderMetaAPI>

```json
{
  "orders": [
    {
      "metaDetails": [
        {
          "key": "uin",
          "decision": "uinMaySell"
        }
      ],
      "meta": {
        "imei": {
          "value": "123456789012345"
        },
        "uin": {
          "value": "123456789012345"
        },
        "gtin": {
          "value": "123456789012345"
        },
        "sgtin": {
          "value": [
            "123456789012345"
          ]
        },
        "expiration": {
          "value": "12.09.2030"
        },
        "customsDeclaration": {
          "value": "10704010/010624/0000302"
        }
      }
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "BadRequest",
  "message": "Неправильный запрос",
  "data": {}
}
```

#### 401

**Content-Type:** `application/json`

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

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": "Доступ запрещён",
  "data": {}
}
```

#### 404 — Не найдено

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "NotFound",
  "message": "Не найдено",
  "data": {}
}
```

#### 429

**Content-Type:** `application/json`

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
