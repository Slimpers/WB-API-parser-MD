# POST /api/marketplace/v3/dbs/orders/stickers

**Получить стикеры для сборочных заданий с доставкой в ПВЗ{{ /api/marketplace/v3/dbs/orders/stickers }}**

теги: `Сборочные задания DBS`

**Полный путь:** `POST /api/marketplace/v3/dbs/orders/stickers`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_token">Метод доступен по <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">типам токенов</a>:<strong> Персональный</strong>,<strong> Сервисный</strong> </div>

Метод возвращает стикеры для сборочных заданий с доставкой в ПВЗ в [статусах](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1info/post):
  - `confirm` — на сборке
  - `deliver` — в доставке

Получить стикеры можно только в размере 580x400 px в формате PDF.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий DBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `type` | query | string; enum: ["pdf"] | да | Формат стикера |
| `width` | query | integer; enum: [58] | да | Ширина стикера |
| `height` | query | integer; enum: [40] | да | Высота стикера |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` **(required)** — array<integer (int64); пример: `5346346`>. Список ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    5346346
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `stickers` — array<object>. Стикеры
  - *(элементы)*
    - `orderId` **(required)** — integer (int64); пример: `5346346`. ID сборочного задания
    - `partA` **(required)** — string; пример: `231648`. Первая часть ID стикера
    - `partB` **(required)** — string; пример: `9753`. Вторая часть ID стикера
    - `barcode` **(required)** — string; пример: `!uKEtQZVx`. Закодированное значение стикера
    - `file` **(required)** — string; пример: `JVBER...ZWYKMTM5MQolJUVPRg==`. Полное представление стикера, кодировка base64

```json
{
  "stickers": [
    {
      "orderId": 5346346,
      "partA": "231648",
      "partB": "9753",
      "barcode": "!uKEtQZVx",
      "file": "JVBER...ZWYKMTM5MQolJUVPRg=="
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

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "Передан некорректный параметр"
}
```

*StatusMismatch:*

```json
{
  "code": "StatusMismatch",
  "message": "Несоответствие статусов, проверьте их правильность"
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

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": ""
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
