# POST /adv/v0/normquery/stats

**Статистика поисковых кластеров{{ /adv/v0/normquery/stats }}**

теги: `Статистика`

**Полный путь:** `POST /adv/v0/normquery/stats`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод формирует статистику по поисковым кластерам за указанный период.<br>
Можно использовать для кампаний с моделями оплаты `cpm` — за показы и `cpc` — за клики.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 10 запросов | 6 сек | 20 запросов |
| Сервисный | 1 мин | 10 запросов | 6 сек | 20 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `from` **(required)** — string (date); пример: `2025-10-07`. Дата начала периода
- `to` **(required)** — string (date); пример: `2025-10-08`. Дата окончания периода
- `items` **(required)** — array<object>
  - *(элементы)*
    - `advert_id` **(required)** — integer. ID кампании
    - `nm_id` **(required)** — integer. Артикул WB

**Пример:**

```json
{
  "from": "2025-10-07",
  "to": "2025-10-08",
  "items": [
    {
      "advert_id": 1825035,
      "nm_id": 983512347
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

Статистика по поисковым кластерам
- `stats` **(required)** — array<$ref: V0GetNormQueryStatsItem>

```json
{
  "stats": [
    {
      "advert_id": 1825035,
      "nm_id": 983512347,
      "stats": [
        {
          "atbs": 68,
          "avg_pos": 3.6,
          "clicks": 2090,
          "cpc": 471,
          "cpm": 813,
          "ctr": 107.23,
          "norm_query": "Фраза 1",
          "orders": 19,
          "views": 1949
        },
        {
          "atbs": 68,
          "avg_pos": 3.6,
          "clicks": 2090,
          "cpc": 471,
          "cpm": 813,
          "ctr": 107.23,
          "norm_query": "Фраза 2",
          "orders": 19,
          "views": 1949
        },
        {
          "atbs": 68,
          "avg_pos": 3.6,
          "clicks": 2090,
          "cpc": 471,
          "cpm": 813,
          "ctr": 107.23,
          "norm_query": "Фраза 3",
          "orders": 19,
          "views": 1949
        },
        {
          "atbs": 36,
          "avg_pos": 3.9,
          "clicks": 1847,
          "cpc": 278,
          "cpm": 445,
          "ctr": 96.4,
          "norm_query": "Фраза 4",
          "orders": 28,
          "views": 1916
        },
        {
          "atbs": 36,
          "avg_pos": 3.9,
          "clicks": 1847,
          "cpc": 278,
          "cpm": 445,
          "ctr": 96.4,
          "norm_query": "Фраза 5",
          "orders": 28,
          "views": 1916
        },
        {
          "atbs": 79,
          "avg_pos": 2.2,
          "clicks": 2468,
          "cpc": 106,
          "cpm": 819,
          "ctr": 145.01,
          "norm_query": "Фраза 6",
          "orders": 14,
          "views": 1702
        },
        {
          "atbs": 79,
          "avg_pos": 2.2,
          "clicks": 2468,
          "cpc": 106,
          "cpm": 819,
          "ctr": 145.01,
          "norm_query": "Фраза 7",
          "orders": 14,
          "views": 1702
        },
        {
          "atbs": 67,
          "avg_pos": 9.9,
          "clicks": 1166,
          "cpc": 250,
          "cpm": 837,
          "ctr": 70.33,
          "norm_query": "Фраза 8",
          "orders": 26,
          "views": 1658
        },
        {
          "atbs": 67,
          "avg_pos": 9.9,
          "clicks": 1166,
          "cpc": 250,
          "cpm": 837,
          "ctr": 70.33,
          "norm_query": "Фраза 9",
          "orders": 26,
          "views": 1658
        },
        {
          "atbs": 46,
          "avg_pos": 2,
          "clicks": 2927,
          "cpc": 122,
          "cpm": 468,
          "ctr": 186.43,
          "norm_query": "Фраза 10",
          "orders": 23,
          "views": 1570
        },
        {
          "atbs": 46,
          "avg_pos": 2,
          "clicks": 2927,
          "cpc": 122,
          "cpm": 468,
          "ctr": 186.43,
          "norm_query": "Фраза 11",
          "orders": 23,
          "views": 1570
        },
        {
          "atbs": 79,
          "avg_pos": 7.1,
          "clicks": 2447,
          "cpc": 67,
          "cpm": 426,
          "ctr": 163.9,
          "norm_query": "Фраза 12",
          "orders": 13,
          "views": 1493
        },
        {
          "atbs": 79,
          "avg_pos": 7.1,
          "clicks": 2447,
          "cpc": 67,
          "cpm": 426,
          "ctr": 163.9,
          "norm_query": "Фраза 13",
          "orders": 13,
          "views": 1493
        },
        {
          "atbs": 61,
          "avg_pos": 6,
          "clicks": 1391,
          "cpc": 370,
          "cpm": 980,
          "ctr": 99.29,
          "norm_query": "Фраза 14",
          "orders": 27,
          "views": 1401
        },
        {
          "atbs": 61,
          "avg_pos": 6,
          "clicks": 1391,
          "cpc": 370,
          "cpm": 980,
          "ctr": 99.29,
          "norm_query": "Фраза 15",
          "orders": 27,
          "views": 1401
        },
        {
          "atbs": 26,
          "avg_pos": 6.9,
          "clicks": 1029,
          "cpc": 88,
          "cpm": 459,
          "ctr": 77.43,
          "norm_query": "Фраза 16",
          "orders": 3,
          "views": 1329
        },
        {
          "atbs": 26,
          "avg_pos": 6.9,
          "clicks": 1029,
          "cpc": 88,
          "cpm": 459,
          "ctr": 77.43,
          "norm_query": "Фраза 17",
          "orders": 3,
          "views": 1329
        },
        {
          "atbs": 67,
          "avg_pos": 3.8,
          "clicks": 1371,
          "cpc": 448,
          "cpm": 534,
          "ctr": 104.18,
          "norm_query": "Фраза 18",
          "orders": 3,
          "views": 1316
        },
        {
          "atbs": 67,
          "avg_pos": 3.8,
          "clicks": 1371,
          "cpc": 448,
          "cpm": 534,
          "ctr": 104.18,
          "norm_query": "Фраза 19",
          "orders": 3,
          "views": 1316
        },
        {
          "atbs": 18,
          "avg_pos": 10,
          "clicks": 2944,
          "cpc": 472,
          "cpm": 839,
          "ctr": 256,
          "norm_query": "Фраза 20",
          "orders": 4,
          "views": 1150
        },
        {
          "atbs": 18,
          "avg_pos": 10,
          "clicks": 2944,
          "cpc": 472,
          "cpm": 839,
          "ctr": 256,
          "norm_query": "Фраза 21",
          "orders": 4,
          "views": 1150
        }
      ]
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `6023d2950af564838f9b44a279d2140c`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `invalid payload`. Заголовок ошибки

```json
{
  "detail": "invalid payment_type value",
  "origin": "camp-api-public-cache",
  "request_id": "7e5cb1f106cc6e85b5b29eb2e8815da2",
  "status": 400,
  "title": "invalid payload"
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

- `detail` **(required)** — string; пример: `some nms are not belong to advert`. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `123e4567-e89b-12d3-a456-426614174000`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `Invalid Params`. Заголовок ошибки

```json
{
  "detail": "norm_query API not available",
  "origin": "camp-api-public-cache",
  "request_id": "60aaf2bc6164e84a9399fae9565b568a",
  "status": 403,
  "title": "request forbidden"
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
