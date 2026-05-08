# GET /api/v1/transit-tariffs

**Транзитные направления{{ /api/v1/transit-tariffs }}**

теги: `Информация для формирования поставок`

**Полный путь:** `GET /api/v1/transit-tariffs`

## Описание

<span>Описание метода</span>

Метод возвращает информацию о доступных транзитных направлениях.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 6 запросов | 10 сек | 10 запросов |
| Сервисный | 1 мин | 6 запросов | 10 сек | 10 запросов |
| Базовый | 12 ч | 1 запрос | 12 ч | 1 запрос |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: models.TransitTariff

*ResponseTariffs:*

```json
[
  {
    "transitWarehouseName": "Обухово",
    "destinationWarehouseName": "Краснодар",
    "activeFrom": "2024-11-03T21:01:00Z",
    "boxTariff": null,
    "palletTariff": 7500
  },
  {
    "transitWarehouseName": "СЦ Гомель 2",
    "destinationWarehouseName": "Краснодар (Тихорецкая)",
    "activeFrom": "2025-04-08T21:00:48.019Z",
    "boxTariff": [
      {
        "from": 0,
        "to": 1500,
        "value": 5.3
      },
      {
        "from": 1500,
        "to": 0,
        "value": 3.9
      }
    ],
    "palletTariff": 6500
  }
]
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
