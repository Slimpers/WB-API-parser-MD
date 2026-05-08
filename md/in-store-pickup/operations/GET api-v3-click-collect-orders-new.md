# GET /api/v3/click-collect/orders/new

**Получить список новых сборочных заданий{{ /api/v3/click-collect/orders/new }}**

теги: `Сборочные задания Самовывоз`

**Базовый URL:** `https://marketplace-api.wildberries.ru`

**Полный путь:** `GET https://marketplace-api.wildberries.ru/api/v3/click-collect/orders/new`

## Описание

<span>Описание метода</span>

Метод возвращает список всех новых [сборочных заданий](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz), которые есть у продавца на момент запроса.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий Самовывоз</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<$ref: api.NewOrder>. Список сборочных заданий

*NewOrderClick:*

```json
{
  "orders": [
    {
      "ddate": "29.10.2024",
      "salePrice": 14000,
      "requiredMeta": [
        "sgtin"
      ],
      "article": "wb1702fyjh",
      "rid": "1234567673554519872.0.0",
      "createdAt": "2024-10-29T10:19:30Z",
      "warehouseAddress": "Москва, район Якиманка, Софийская набережная, 4 с1",
      "orderCode": "23457822-6667",
      "payMode": "prepaid",
      "skus": [
        "2041546265353"
      ],
      "id": 1234567890,
      "warehouseId": 1234567,
      "nmId": 123456789,
      "chrtId": 987654321,
      "price": 14000,
      "finalPrice": 14000,
      "convertedPrice": 14000,
      "convertedFinalPrice": 14000,
      "currencyCode": 643,
      "convertedCurrencyCode": 643,
      "cargoType": 1,
      "isZeroOrder": false
    }
  ]
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
