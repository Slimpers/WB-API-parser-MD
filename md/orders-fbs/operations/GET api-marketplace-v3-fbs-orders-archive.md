# GET /api/marketplace/v3/fbs/orders/archive

**Получить список архивных сборочных заданий{{ /api/marketplace/v3/fbs/orders/archive }}**

теги: `Сборочные задания FBS`

**Полный путь:** `GET /api/marketplace/v3/fbs/orders/archive`

## Описание

<span>Описание метода</span>

Метод возвращает сборочные задания, созданные более 3 месяцев назад.

Часть сборочных заданий попадает в архив позже, чем через 3 месяца после создания, так как поставка переходит в архив только после того, как все заказы в ней будут завершены.
Например, так происходит, если продавец не доставил один из заказов в поставке и заказ был отменён автоматически через несколько дней.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `year` | query | integer | да | Год создания заказа |
| `month` | query | integer | да | Месяц создания заказа |
| `next` | query | integer (int64) | да | Параметр пагинации. Устанавливает значение, с которого надо получить следующий пакет данных. Для получения полного списка данных должен быть равен `0` в первом запросе. Для следующих запросов необходимо брать значения из одноимённого поля в ответе. |
| `limit` | query | integer (int32) | да | Количество сборочных заданий в ответе |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

Список архивных сборочных заданий
- `next` **(required)** — integer (int64). Параметр пагинации. Содержит значение, которое необходимо указать в запросе для получения следующего пакета данных
- `orders` **(required)** — array<$ref: v3.ArchiveOrder>. Архивные сборочные задания

```json
{
  "orders": [
    {
      "cargoType": "mgt",
      "colorCode": "RAL 3017",
      "createdAt": "2022-05-04",
      "crossBorder": {
        "parcel": "1Z999AA10123456784"
      },
      "crossBorderType": "crossBorder",
      "id": 1234567890,
      "isZeroOrder": false,
      "metaDetails": [
        {
          "key": "uin",
          "decision": "uinMaySell"
        }
      ],
      "options": {
        "isB2B": false
      },
      "orderUid": "165918930_629fbc924b984618a44354475ca58675",
      "priceInfo": {
        "convertedCurrencyCode": 643,
        "convertedPrice": 1020,
        "currencyCode": 643,
        "price": 1020
      },
      "product": {
        "article": "wv1702fyjh",
        "chrtId": 12345678,
        "nmId": 370870300,
        "skus": [
          "12345Ejf5",
          "12345Ejf6",
          "12345Ejf7"
        ]
      },
      "rid": "f884001e44e511edb8780242ac120002",
      "scanPrice": 5200,
      "status": {
        "supplierStatus": "complete",
        "wbStatus": "sent_to_carrier"
      },
      "stickerId": 33811984302,
      "supplyId": "WB-GI-1234588",
      "warehouseId": 55684681
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `code` — string. Код ошибки
- `detail` **(required)** — string. Детали ошибки
- `errors` — array<object>
  - *(элементы)*
    - `location` — string. Параметр, где произошла ошибка
    - `message` — string. Текст ошибки
    - `value`. Значение параметра, где произошла ошибка
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `status` — integer. HTTP статус-код ответа
- `title` **(required)** — string. Заголовок ошибки

*BadRequest:*

```json
{
  "code": "BadRequest",
  "detail": "Incorrect parameter",
  "errors": [
    {
      "location": "query.next",
      "message": "expected integer",
      "value": "1w"
    }
  ],
  "origin": "marketplace-public-api",
  "requestId": "a0b5907c-2978-4db6-9a59-00666e8b8d54",
  "status": 400,
  "title": "IncorrectParameter"
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

#### 403 — Доступ запрещён

**Content-Type:** `application/problem+json`

- `code` — string. Код ошибки
- `detail` **(required)** — string. Детали ошибки
- `errors` — array<object>
  - *(элементы)*
    - `location` — string. Параметр, где произошла ошибка
    - `message` — string. Текст ошибки
    - `value`. Значение параметра, где произошла ошибка
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `status` — integer. HTTP статус-код ответа
- `title` **(required)** — string. Заголовок ошибки

*AccessDenied:*

```json
{
  "code": "AccessDenied",
  "detail": "",
  "errors": [
    {
      "location": "",
      "message": "",
      "value": 0
    }
  ],
  "origin": "marketplace-public-api",
  "requestId": "a0b5907c-2978-4db6-9a59-00666e8b8d54",
  "status": 403,
  "title": "AccessDenied"
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
