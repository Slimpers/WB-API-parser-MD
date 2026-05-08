# POST /adv/v1/stats

**Статистика медиакампаний{{ /adv/v1/stats }}**

теги: `Статистика`

**Полный путь:** `POST /adv/v1/stats`

## Описание

<span>Описание метода</span>

Метод формирует статистику кампаний сервиса [WB Медиа](https://cmp.wildberries.ru/cmpf/statistics). Статистику можно группировать по датам и/или интервалам.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Сервисный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- array of: any

**Пример «RequestWithDate»:**

```json
[
  {
    "id": 8960367,
    "dates": [
      "2023-10-07",
      "2023-10-06"
    ]
  },
  {
    "id": 9876543,
    "dates": [
      "2023-10-07",
      "2023-12-06"
    ]
  }
]
```

**Пример «RequestWithInterval»:**

```json
[
  {
    "id": 8960367,
    "interval": {
      "begin": "2023-10-08",
      "end": "2023-10-10"
    }
  },
  {
    "id": 78978565,
    "interval": {
      "begin": "2023-09-08",
      "end": "2023-09-11"
    }
  }
]
```

**Пример «RequestWithoutParam»:**

```json
[
  {
    "id": 107024
  }
]
```

**Пример «RequestAggregate»:**

```json
[
  {
    "id": 107024,
    "interval": {
      "begin": "2023-10-21",
      "end": "2023-10-21"
    }
  },
  {
    "id": 107024,
    "dates": [
      "2023-10-22",
      "2023-10-26"
    ]
  }
]
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: any

*RespStatMediaInterval:*

```json
[
  {
    "interval": {
      "begin": "2023-10-21",
      "end": "2023-10-25"
    },
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 11849,
        "clicks": 209,
        "cr": 0.48,
        "ctr": 1.76,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 4,
        "orders": 1,
        "price": 175000,
        "cpc": 837.32,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-21T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2017,
                    "clicks": 27,
                    "atbs": 1,
                    "ctr": 1.34
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 1.91,
        "cr2": 25
      }
    ]
  }
]
```

*RespStatMediaDates:*

```json
[
  {
    "dates": [
      "2023-10-26",
      "2023-10-22"
    ],
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 4584,
        "clicks": 74,
        "cr": 1.35,
        "ctr": 1.61,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 2,
        "orders": 1,
        "price": 175000,
        "cpc": 2364.86,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-22T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2384,
                    "clicks": 33,
                    "atbs": 2,
                    "orders": 1,
                    "cr": 3.03,
                    "ctr": 1.38
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 2.7,
        "cr2": 50
      }
    ]
  }
]
```

*RespStatMediaWithoutParam:*

```json
[
  {
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 11849,
        "clicks": 209,
        "cr": 0.48,
        "ctr": 1.76,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 4,
        "orders": 1,
        "price": 175000,
        "cpc": 837.32,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-21T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2017,
                    "clicks": 27,
                    "atbs": 1,
                    "ctr": 1.34
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 1.91,
        "cr2": 25
      }
    ]
  }
]
```

*RespStatMediaAggregate:*

```json
[
  {
    "interval": {
      "begin": "2023-10-21",
      "end": "2023-10-25"
    },
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 11849,
        "clicks": 209,
        "cr": 0.48,
        "ctr": 1.76,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 4,
        "orders": 1,
        "price": 175000,
        "cpc": 837.32,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-21T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2017,
                    "clicks": 27,
                    "atbs": 1,
                    "ctr": 1.34
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 1.91,
        "cr2": 25
      }
    ]
  },
  {
    "dates": [
      "2023-10-26",
      "2023-10-22"
    ],
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 4584,
        "clicks": 74,
        "cr": 1.35,
        "ctr": 1.61,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 2,
        "orders": 1,
        "price": 175000,
        "cpc": 2364.86,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-22T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2384,
                    "clicks": 33,
                    "atbs": 2,
                    "orders": 1,
                    "cr": 3.03,
                    "ctr": 1.38
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 2.7,
        "cr2": 50
      }
    ]
  },
  {
    "stats": [
      {
        "item_id": 62237,
        "item_name": "Gloria Jeans",
        "category_name": "Детям",
        "advert_type": 1,
        "place": 2,
        "views": 11849,
        "clicks": 209,
        "cr": 0.48,
        "ctr": 1.76,
        "date_from": "2023-10-21T00:00:00+03:00",
        "date_to": "2023-10-27T23:59:59+03:00",
        "subject_name": "Одежда",
        "atbs": 4,
        "orders": 1,
        "price": 175000,
        "cpc": 837.32,
        "status": 6,
        "daily_stats": [
          {
            "date": "2023-10-21T00:00:00+03:00",
            "app_type_stats": [
              {
                "app_type": 1,
                "stats": [
                  {
                    "views": 2017,
                    "clicks": 27,
                    "atbs": 1,
                    "ctr": 1.34
                  }
                ]
              }
            ]
          }
        ],
        "expenses": 175000,
        "cr1": 1.91,
        "cr2": 25
      }
    ]
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `error` — string

*invalidAdvert:*

```json
{
  "error": "Некорректное тело запроса"
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
