# GET /adv/v3/fullstats

**Статистика кампаний{{ /adv/v3/fullstats }}**

теги: `Статистика`

**Полный путь:** `GET /adv/v3/fullstats`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод формирует статистику для кампаний независимо от типа.
<br><br>
Максимальный период в запросе — 31 день.
<br><br>
Для кампаний в статусах `7`, `9` и `11`.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 1 запрос |
| Сервисный | 1 мин | 3 запроса | 20 сек | 1 запрос |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `ids` | query | string; пример: `22161678,28449281,28155229` | да | ID кампаний, максимум 50 значений |
| `beginDate` | query | string (date) | да | Дата начала интервала |
| `endDate` | query | string (date) | да | Дата окончания интервала |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

Статистика по кампаниям за период, указанный в запросе. По всем артикулам WB и платформам
- array of: $ref: FullStatsItem

```json
[
  {
    "advertId": 22161678,
    "atbs": 9,
    "boosterStats": [
      {
        "avg_position": 24,
        "date": "2025-09-07",
        "nm": 221725278
      },
      {
        "avg_position": 35,
        "date": "2025-09-08",
        "nm": 221725278
      }
    ],
    "canceled": 0,
    "clicks": 139,
    "cpc": 4.76,
    "cr": 0,
    "ctr": 10.12,
    "days": [
      {
        "apps": [
          {
            "appType": 1,
            "atbs": 0,
            "canceled": 0,
            "clicks": 1,
            "cpc": 10.19,
            "cr": 0,
            "ctr": 4.76,
            "nms": [
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 1,
                "cpc": 10.19,
                "cr": 0,
                "ctr": 4.76,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 10.19,
                "sum_price": 0,
                "views": 21
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 10.19,
            "sum_price": 0,
            "views": 21
          },
          {
            "appType": 32,
            "atbs": 1,
            "canceled": 0,
            "clicks": 54,
            "cpc": 4.26,
            "cr": 0,
            "ctr": 11.37,
            "nms": [
              {
                "atbs": 1,
                "canceled": 0,
                "clicks": 54,
                "cpc": 4.26,
                "cr": 0,
                "ctr": 11.37,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 230.08,
                "sum_price": 0,
                "views": 475
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 230.08,
            "sum_price": 0,
            "views": 475
          },
          {
            "appType": 64,
            "atbs": 1,
            "canceled": 0,
            "clicks": 20,
            "cpc": 6.91,
            "cr": 0,
            "ctr": 6.94,
            "nms": [
              {
                "atbs": 1,
                "canceled": 0,
                "clicks": 20,
                "cpc": 6.91,
                "cr": 0,
                "ctr": 6.94,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 138.23,
                "sum_price": 0,
                "views": 288
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 138.23,
            "sum_price": 0,
            "views": 288
          }
        ],
        "atbs": 2,
        "canceled": 0,
        "clicks": 75,
        "cpc": 5.05,
        "cr": 0,
        "ctr": 9.57,
        "date": "2025-09-07T00:00:00Z",
        "orders": 0,
        "shks": 0,
        "sum": 378.49,
        "sum_price": 0,
        "views": 784
      },
      {
        "apps": [
          {
            "appType": 32,
            "atbs": 5,
            "canceled": 0,
            "clicks": 45,
            "cpc": 3.58,
            "cr": 0,
            "ctr": 13.43,
            "nms": [
              {
                "atbs": 5,
                "canceled": 0,
                "clicks": 45,
                "cpc": 3.58,
                "cr": 0,
                "ctr": 13.43,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 161.02,
                "sum_price": 0,
                "views": 335
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 161.02,
            "sum_price": 0,
            "views": 335
          },
          {
            "appType": 64,
            "atbs": 2,
            "canceled": 0,
            "clicks": 19,
            "cpc": 6.05,
            "cr": 0,
            "ctr": 8.02,
            "nms": [
              {
                "atbs": 2,
                "canceled": 0,
                "clicks": 19,
                "cpc": 6.05,
                "cr": 0,
                "ctr": 8.02,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 114.95,
                "sum_price": 0,
                "views": 237
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 114.95,
            "sum_price": 0,
            "views": 237
          },
          {
            "appType": 1,
            "atbs": 0,
            "canceled": 0,
            "clicks": 0,
            "cpc": 0,
            "cr": 0,
            "ctr": 0,
            "nms": [
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 0,
                "cpc": 0,
                "cr": 0,
                "ctr": 0,
                "name": "постер 2",
                "nmId": 221725278,
                "orders": 0,
                "shks": 0,
                "sum": 6.79,
                "sum_price": 0,
                "views": 17
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 6.79,
            "sum_price": 0,
            "views": 17
          }
        ],
        "atbs": 7,
        "canceled": 0,
        "clicks": 64,
        "cpc": 4.42,
        "cr": 0,
        "ctr": 10.87,
        "date": "2025-09-08T00:00:00Z",
        "orders": 0,
        "shks": 0,
        "sum": 282.76,
        "sum_price": 0,
        "views": 589
      }
    ],
    "orders": 0,
    "shks": 0,
    "sum": 661.25,
    "sum_price": 0,
    "views": 1373
  },
  {
    "advertId": 28449281,
    "atbs": 1,
    "canceled": 0,
    "clicks": 9,
    "cpc": 35.94,
    "cr": 11.11,
    "ctr": 1.76,
    "days": [
      {
        "apps": [
          {
            "appType": 32,
            "atbs": 1,
            "canceled": 0,
            "clicks": 7,
            "cpc": 26.31,
            "cr": 14.29,
            "ctr": 2.41,
            "nms": [
              {
                "atbs": 1,
                "canceled": 0,
                "clicks": 5,
                "cpc": 33.02,
                "cr": 20,
                "ctr": 1.92,
                "name": "Футболка желтая",
                "nmId": 398309059,
                "orders": 1,
                "shks": 1,
                "sum": 165.1,
                "sum_price": 500,
                "views": 260
              },
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 2,
                "cpc": 9.53,
                "cr": 0,
                "ctr": 6.67,
                "name": "Футболка салатовая",
                "nmId": 301957154,
                "orders": 0,
                "shks": 0,
                "sum": 19.05,
                "sum_price": 0,
                "views": 30
              }
            ],
            "orders": 1,
            "shks": 1,
            "sum": 184.15,
            "sum_price": 500,
            "views": 290
          },
          {
            "appType": 64,
            "atbs": 0,
            "canceled": 0,
            "clicks": 2,
            "cpc": 62.87,
            "cr": 0,
            "ctr": 1.01,
            "nms": [
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 1,
                "cpc": 12.7,
                "cr": 0,
                "ctr": 5,
                "name": "Футболка салатовая",
                "nmId": 301957154,
                "orders": 0,
                "shks": 0,
                "sum": 12.7,
                "sum_price": 0,
                "views": 20
              },
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 1,
                "cpc": 113.03,
                "cr": 0,
                "ctr": 0.56,
                "name": "Футболка желтая",
                "nmId": 398309059,
                "orders": 0,
                "shks": 0,
                "sum": 113.03,
                "sum_price": 0,
                "views": 178
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 125.73,
            "sum_price": 0,
            "views": 198
          },
          {
            "appType": 1,
            "atbs": 0,
            "canceled": 0,
            "clicks": 0,
            "cpc": 0,
            "cr": 0,
            "ctr": 0,
            "nms": [
              {
                "atbs": 0,
                "canceled": 0,
                "clicks": 0,
                "cpc": 0,
                "cr": 0,
                "ctr": 0,
                "name": "Футболка желтая",
                "nmId": 398309059,
                "orders": 0,
                "shks": 0,
                "sum": 13.59,
                "sum_price": 0,
                "views": 22
              }
            ],
            "orders": 0,
            "shks": 0,
            "sum": 13.59,
            "sum_price": 0,
            "views": 22
          }
        ],
        "atbs": 1,
        "canceled": 0,
        "clicks": 9,
        "cpc": 35.94,
        "cr": 11.11,
        "ctr": 1.76,
        "date": "2025-09-08T00:00:00Z",
        "orders": 1,
        "shks": 1,
        "sum": 323.47,
        "sum_price": 500,
        "views": 510
      }
    ],
    "orders": 1,
    "shks": 1,
    "sum": 323.47,
    "sum_price": 500,
    "views": 510
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

Ошибка
- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `request_id` **(required)** — string. ID запроса
- `status` **(required)** — integer. HTTP статус-код
- `title` **(required)** — string. Заголовок ошибки

```json
{
  "detail": "invalid ids",
  "origin": "camp-api-public-cache",
  "request_id": "40a229f3775b03585b65420c787aaebe",
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
