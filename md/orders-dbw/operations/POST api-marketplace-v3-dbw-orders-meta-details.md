# POST /api/marketplace/v3/dbw/orders/meta/details

**Получить метаданные сборочных заданий{{ /api/marketplace/v3/dbw/orders/meta/details }}**

теги: `Метаданные DBW`

**Полный путь:** `POST /api/marketplace/v3/dbw/orders/meta/details`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает метаданные [сборочных заданий](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders/get) и статусы их валидации.
<br><br>
Перечень метаданных, доступных для сборочного задания, можно получить в [списке новых сборочных заданий](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1new/get), поле `requiredMeta`.
<br><br>
Возможные метаданные:
  - `imei` — [IMEI](./orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1imei/put)
  - `uin` — [УИН](./orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1uin/put)
  - `gtin` — [GTIN](./orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1gtin/put)
  - `sgtin` — [код маркировки Честного знака](./orders-dbw#tag/Metadannye-DBW/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1sgtin/post)

  <div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для следующих методов DBW:
<ul>
    <li>получение и обновление списка контактов</li>
    <li>получение и удаление метаданных</li>
    <li>методы сборочных заданий</li>
</ul> 

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

</div>

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
    1234678898
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `requestId` **(required)** — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `orders` — array<object>. Метаданные сборочных заданий и статусы их валидации
  - *(элементы)*
    - `orderId` — integer; пример: `123456`. ID сборочного задания
    - `isError` **(required)** — boolean; пример: `False`. Есть ли ошибки
    - `errors` — array<object>. Информация об ошибке
      - *(элементы)*
        - `code` — integer; пример: `404`. Код ошибки
        - `detail` — string; пример: `NotFound`. Дополнительная информация об ошибке
    - `metaDetails` — array<object>. Метаданные и статусы их валидации
      - *(элементы)*
        - `key` — string; пример: `sgtin`. Метаданные
        - `value` — string; пример: `123456789012345`. Значение метаданных
        - `decision` — string; пример: `sgtinIntroduced`. Статус проверки:

```json
{
  "requestId": "f1787bd2d1fdс35d6f537316514у4a05",
  "orders": [
    {
      "orderId": 123456,
      "isError": false,
      "errors": [],
      "metaDetails": [
        {
          "key": "sgtin",
          "value": "123456789012345",
          "decision": "sgtinIntroduced"
        }
      ]
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
