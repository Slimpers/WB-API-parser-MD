# POST /api/advert/v1/bids/min

**Минимальные ставки для карточек товаров{{ /api/advert/v1/bids/min }}**

теги: `Создание кампаний`

**Полный путь:** `POST /api/advert/v1/bids/min`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает минимальные ставки для карточек товаров в копейках по типу оплаты и местам размещения.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 20 запросов | 3 сек | 5 запросов |
| Сервисный | 1 мин | 20 запросов | 3 сек | 5 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `advert_id` **(required)** — integer (int64). ID кампании
- `nm_ids` **(required)** — array<integer (int64)>. Список артикулов WB
- `payment_type` **(required)** — string; enum: ["cpm", "cpc"]. Тип оплаты:
- `placement_types` **(required)** — array<string; enum: ["combined", "search", "recommendation"]>. Места размещения:

**Пример:**

```json
{
  "advert_id": 98765432,
  "nm_ids": [
    12345678,
    87654321
  ],
  "payment_type": "cpm",
  "placement_types": [
    "combined",
    "search",
    "recommendation"
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `bids` **(required)** — array<object>. Список карточек товаров со ставками
  - *(элементы)*
    - `bids` **(required)** — array<object>. Список ставок по местам размещения
      - *(элементы)*
        - `type` **(required)** — $ref: PlacementType
        - `value` **(required)** — integer. Минимальная ставка, копейки
    - `nm_id` **(required)** — integer (int64). Артикул WB

```json
{
  "bids": [
    {
      "bids": [
        {
          "type": "combined",
          "value": 155
        },
        {
          "type": "search",
          "value": 250
        },
        {
          "type": "recommendation",
          "value": 250
        }
      ],
      "nm_id": 12345678
    },
    {
      "bids": [
        {
          "type": "combined",
          "value": 155
        },
        {
          "type": "search",
          "value": 250
        },
        {
          "type": "recommendation",
          "value": 250
        }
      ],
      "nm_id": 87654321
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string; пример: `some nms are not belong to advert`. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `123e4567-e89b-12d3-a456-426614174000`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `Invalid Params`. Заголовок ошибки

```json
{
  "detail": "some nms are not belong to advert",
  "origin": "camp-api-public-cache",
  "request_id": "123e4567-e89b-12d3-a456-426614174000",
  "status": 400,
  "title": "Invalid Params"
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
