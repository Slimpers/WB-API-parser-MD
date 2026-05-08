# GET /api/advert/v0/bids/recommendations

**Рекомендуемые ставки для карточек товаров и поисковых кластеров{{ /api/advert/v0/bids/recommendations }}**

теги: `Управление кампаниями`

**Полный путь:** `GET /api/advert/v0/bids/recommendations`

## Описание

<span>Описание метода</span>

Метод возвращает рекомендуемые ставки для карточек товаров и поисковых кластеров кампании.
Только для кампаний с типом оплаты `cpm` — за показы.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 5 запросов | 12 сек | 5 запросов |
| Сервисный | 1 мин | 5 запросов | 12 сек | 5 запросов |
| Базовый | 1 ч | 20 запросов | 3 мин | 1 запрос |

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `nmId` | query | integer (int64) | да | Артикул WB |
| `advertId` | query | integer (int64) | да | ID кампании |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `advertId` — integer (int64). ID кампании
- `base` — $ref: V0BidRecommendationBase
- `nmId` — integer (int64). Артикул WB
- `normQueries` — array<$ref: V0BidRecommendationNormQuery>. Рекомендуемые ставки для поисковых кластеров

```json
{
  "advertId": 987654321,
  "base": {
    "competitiveBid": {
      "bidKopecks": 39500
    },
    "leadersBid": {
      "bidKopecks": 66900
    },
    "top2": {
      "bidKopecks": 0
    }
  },
  "nmId": 123456789,
  "normQueries": [
    {
      "normQuery": "футболка",
      "reachMax": {
        "bidKopecks": 50500,
        "bidKopecksMin": 49500
      },
      "reachMedium": {
        "bidKopecks": 32000
      },
      "reachMin": {
        "bidKopecks": 32000
      }
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `text/plain`

- string

*IncorrectTypeAdv:*

```json
"Некорректное значение параметра type"
```

*IncorrectSupplierIdAdv:*

```json
"Некорректный ID продавца"
```

*IncorrectUsingMethods:*

```json
"Для получения информации передайте или список кампаний, или набор фильтров"
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
