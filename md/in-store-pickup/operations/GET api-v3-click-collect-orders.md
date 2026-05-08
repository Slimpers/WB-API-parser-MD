# GET /api/v3/click-collect/orders

**Получить информацию о завершённых сборочных заданиях{{ /api/v3/click-collect/orders }}**

теги: `Сборочные задания Самовывоз`

**Базовый URL:** `https://marketplace-api.wildberries.ru`

**Полный путь:** `GET https://marketplace-api.wildberries.ru/api/v3/click-collect/orders`

## Описание

<span>Описание метода</span>

Метод возвращает информацию о завершённых сборочных заданиях после продажи или отмены заказа.

Можно получить данные за заданный период, максимум 30 календарных дней одним запросом.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий Самовывоз</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `limit` | query | integer | да | Параметр пагинации. Устанавливает предельное количество возвращаемых данных. |
| `next` | query | integer | да | Параметр пагинации. Устанавливает значение, с которого необходимо получить следующий пакет данных. Для получения полного списка данных должен быть равен `0` в первом запросе. Для следующих запросов необходимо брать значения из одноимённого поля в ответе |
| `dateFrom` | query | integer | да | Дата начала периода в формате Unix timestamp |
| `dateTo` | query | integer | да | Дата конца периода в формате Unix timestamp |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `next` — integer; пример: `12345566`. Параметр пагинации. Содержит значение, которое необходимо указать в
- `orders` — array<$ref: api.Order>. Список сборочных заданий

```json
{
  "next": 12345566,
  "orders": [
    {
      "article": "wb6scpbwvp",
      "cargoType": 1,
      "chrtId": 12345676,
      "createdAt": "2025-03-21T09:53:31Z",
      "price": 5000,
      "finalPrice": 5000,
      "convertedPrice": 5000,
      "convertedFinalPrice": 5000,
      "currencyCode": 643,
      "convertedCurrencyCode": 643,
      "id": 123456789,
      "isZeroOrder": false,
      "nmId": 1234567898765,
      "orderCode": "21117866-0006",
      "payMode": "prepaid",
      "rid": "5044304527347733263.0.0",
      "skus": [
        "2043227963145"
      ],
      "warehouseAddress": "Москва, район Якиманка, Софийская набережная, 4 с1",
      "warehouseId": 1162157
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные, обогащающие ошибку
  - *(пустой object)*

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "Передан некорректный параметр"
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

#### 403

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные, обогащающие ошибку
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": "Доступ запрещён"
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
