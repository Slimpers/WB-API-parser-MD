# GET /api/v3/dbw/orders/new

**Получить список новых сборочных заданий{{ /api/v3/dbw/orders/new }}**

теги: `Сборочные задания DBW`

**Полный путь:** `GET /api/v3/dbw/orders/new`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список всех новых [сборочных заданий](./orders-dbw#tag/Sborochnye-zadaniya-DBW), которые есть у продавца на момент запроса.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для следующих методов DBW:
<ul>
    <li>получение и обновление списка контактов</li>
    <li>получение и удаление метаданных</li>
    <li>методы сборочных заданий</li>
</ul> 

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<$ref: OrderNewDBW>. Список новых сборочных заданий

```json
{
  "orders": [
    {
      "address": {
        "fullAddress": "Челябинская область, г. Челябинск, 51-я улица Арабкира, д. 10А, кв. 42",
        "longitude": 44.519068,
        "latitude": 40.20192
      },
      "salePrice": 504658,
      "requiredMeta": [
        "uin"
      ],
      "comment": "Упакуйте в пленку, пожалуйста",
      "orderUid": "165918930_629fbc924b984618a44354475ca58675",
      "groupId": "7a2c8810-1db2-4011-9682-5c7fa33afd83",
      "article": "one-ring-7548",
      "colorCode": "RAL 3017",
      "rid": "f884001e44e511edb8780242ac120002",
      "createdAt": "2022-05-04T07:56:29Z",
      "skus": [
        "6665956397512"
      ],
      "id": 13833711,
      "warehouseId": 658434,
      "nmId": 123456789,
      "chrtId": 987654321,
      "price": 1014,
      "convertedPrice": 1014,
      "currencyCode": 933,
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
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": ""
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
