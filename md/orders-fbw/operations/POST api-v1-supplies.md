# POST /api/v1/supplies

**Список поставок{{ /api/v1/supplies }}**

теги: `Информация о поставках`

**Полный путь:** `POST /api/v1/supplies`

## Описание

<span>Описание метода</span>

Метод возвращает список поставок, по умолчанию — последние 1000 поставок.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 30 запросов | 2 сек | 10 запросов |
| Сервисный | 1 мин | 30 запросов | 2 сек | 10 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `limit` | query | integer | нет | Количество записей в ответе |
| `offset` | query | integer | нет | После какого элемента выдавать данные |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `dates` — array<$ref: models.DateFilterRequest>. Фильтр по датам
- `statusIDs` — array<$ref: models.HandySupplyStatus>. Фильтр поставок по статусам. Возможные значения:

**Пример:**

```json
{
  "dates": [
    {
      "from": "2024-03-04",
      "till": "2025-03-24",
      "type": "factDate"
    }
  ],
  "statusIDs": [
    5,
    6
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: models.Supply

```json
[
  {
    "phone": "+7 916 *** 44 44",
    "supplyID": null,
    "preorderID": 34597755,
    "createDate": "2024-12-29T16:58:26+03:00",
    "supplyDate": null,
    "factDate": null,
    "updatedDate": null,
    "statusID": 1,
    "boxTypeID": 1
  },
  {
    "phone": "+7 916 *** 33 33",
    "supplyID": 26596368,
    "preorderID": 34601223,
    "createDate": "2024-12-29T16:57:59+03:00",
    "supplyDate": "2024-12-29T00:00:00+03:00",
    "factDate": null,
    "updatedDate": null,
    "statusID": 2,
    "boxTypeID": 5
  },
  {
    "phone": "+7 000 *** 36 76",
    "supplyID": 22677736,
    "preorderID": 27363170,
    "createDate": "2024-08-22T18:10:59+03:00",
    "supplyDate": "2024-08-22T00:00:00+03:00",
    "factDate": "2024-08-22T12:24:14+03:00",
    "updatedDate": "2024-08-22T18:33:45+03:00",
    "statusID": 6,
    "boxTypeID": 2,
    "isBoxOnPallet": false
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `status` — integer. HTTP статус-код
- `title` — string. ID ошибки
- `detail` — string. Описание ошибки
- `requestId` — string. ID запроса
- `origin` — string. Сервис, вернувший ошибку

*BadTypeFormat:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Выберите значение параметра 'Type' из списка: 'factDate createDate supplyDate updatedDate'",
  "requestId": "31aba083c7144409c3cbbb968e693f16",
  "origin": "supply-api"
}
```

*BadLimitFormat:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Неверный формат limit",
  "requestId": "a6bdc2a4d2fde51c2036fa8af2483886",
  "origin": "supply-api"
}
```

*BadOffsetFormat:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Неверный формат offset",
  "requestId": "a6bdc2a4d2fde51c2036fa8af2483886",
  "origin": "supply-api"
}
```

*BadFromOrTill:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "ошибка при считывании даты \"11-03-2019\". Дата должна быть в формате ISO Date: 2006-01-02",
  "requestId": "7916f0258e363ad2b6663e980903818d",
  "origin": "supply-api"
}
```

*BadStatusIDs:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Выберите значение параметра 'StatusIDs[0]' из списка: '1 2 3 4 5 6'",
  "requestId": "52d7410a596b40cecfeb70c41ae5ac99",
  "origin": "supply-api"
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

#### 402

**Content-Type:** `application/problem+json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки. Ошибка возвращается только сервисам из [Каталога решений для бизнеса](https://dev.wildberries.ru/business-solutions)

```json
{
  "title": "payment required",
  "detail": "wb solution for business has insufficient funds on its balance. please top up the balance in the company's personal account https://dev.wildberries.ru/company"
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
