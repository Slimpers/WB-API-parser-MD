# POST /adv/v1/normquery/stats

**Статистика по поисковым кластерам с детализацией по дням{{ /adv/v1/normquery/stats }}**

теги: `Статистика`

**Полный путь:** `POST /adv/v1/normquery/stats`

## Описание

<span>Описание метода</span>

Метод формирует статистику по поисковым кластерам за указанный период с детализацией по дням.
Можно использовать для кампаний с моделями оплаты `cpm` — за показы и `cpc` — за клики.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 10 запросов | 6 сек | 20 запросов |
| Сервисный | 1 мин | 10 запросов | 6 сек | 20 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `from` **(required)** — string (date); пример: `2025-01-01`. Дата начала периода
- `to` **(required)** — string (date); пример: `2025-01-31`. Дата окончания периода периода
- `items` **(required)** — array<object>
  - *(элементы)*
    - `advertId` **(required)** — integer (int64). ID кампании
    - `nmId` **(required)** — integer (int64). Артикул WB

**Пример:**

```json
{
  "from": "2026-01-01",
  "to": "2026-01-30",
  "items": [
    {
      "advertId": 123456789,
      "nmId": 987654321
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `items` **(required)** — array<$ref: V1GetNormQueryStatsResponseItem>

```json
{
  "items": [
    {
      "advertId": 123456789,
      "dailyStats": [
        {
          "date": "2026-01-27",
          "stat": {
            "atbs": 39,
            "avgPos": 3.3,
            "clicks": 75,
            "cpc": 1.44,
            "cpm": 562.5,
            "ctr": 39.06,
            "normQuery": "Поисковый кластер 0",
            "orders": 9,
            "shks": 5,
            "spend": 108,
            "views": 192
          }
        },
        {
          "date": "2026-01-27",
          "stat": {
            "atbs": 71,
            "avgPos": 7.9,
            "clicks": 56,
            "cpc": 4.38,
            "cpm": 1290.95,
            "ctr": 29.47,
            "normQuery": "румяна для лица vivienne sabo",
            "orders": 2,
            "shks": 44,
            "spend": 245.28,
            "views": 190
          }
        },
        {
          "date": "2026-01-27",
          "stat": {
            "atbs": 39,
            "avgPos": 3.3,
            "clicks": 75,
            "cpc": 1.44,
            "cpm": 562.5,
            "ctr": 39.06,
            "normQuery": "Поисковый кластер 2",
            "orders": 9,
            "shks": 345345,
            "spend": 108,
            "views": 192
          }
        }
      ],
      "nmId": 987654321
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
  "detail": "incorrect request body, please check API documentation",
  "origin": "camp-api-public-cache",
  "request_id": "33e7d9f3fc221648cdf096bf8e62e482",
  "status": 400,
  "title": "invalid request body"
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
