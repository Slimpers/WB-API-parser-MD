# GET /api/v1/supplier/stocks

**Склады{{ /api/v1/supplier/stocks }}**

> ⚠️ DEPRECATED

теги: `Основные отчёты`

**Полный путь:** `GET /api/v1/supplier/stocks`

## Описание

<span>Описание метода</span>

Данный метод устарел. Он будет удалён [23 июня](https://dev.wildberries.ru/release-notes?id=494)

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 3 ч | 1 запрос | 3 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | да | Дата и время последнего изменения по товару.  Для получения полного остатка следует указывать максимально раннее значение.  Например, `2019-06-20`  Дата в формате RFC3339. Можно передать дату или дату со временем. Время можно указывать с точностью до [секунд](./api-information#tag/Vvedenie/Limity-zaprosov) или миллисекунд.  Время передаётся в часовом поясе Москва (UTC+3).  Примеры:   - `2019-06-20`   - `2019-06-20T23:59:59`   - `2019-06-20T00:00:00.12345`   - `2017-03-25T00:00:00` |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: StocksItem

```json
[
  {
    "lastChangeDate": "2023-07-05T11:13:35",
    "warehouseName": "Краснодар",
    "supplierArticle": "443284",
    "nmId": 1439871458,
    "barcode": "2037401340280",
    "quantity": 33,
    "inWayToClient": 1,
    "inWayFromClient": 0,
    "quantityFull": 34,
    "category": "Посуда и инвентарь",
    "subject": "Формы для запекания",
    "brand": "X",
    "techSize": "0",
    "Price": 185,
    "Discount": 0,
    "isSupply": true,
    "isRealization": false,
    "SCCode": "Tech"
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`


*DateFromFieldRequired:*

```json
{
  "errors": [
    "dateFrom: field required"
  ]
}
```

*DateFromValueNotValidated:*

```json
{
  "errors": "dateFrom: Value not validated"
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
