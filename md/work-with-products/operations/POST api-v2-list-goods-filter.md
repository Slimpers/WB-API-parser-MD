# POST /api/v2/list/goods/filter

**Получить товары с ценами по артикулам{{ /api/v2/list/goods/filter }}**

теги: `Цены и скидки`

**Полный путь:** `POST /api/v2/list/goods/filter`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о товарах по их артикулам: цены, валюту, общие скидки и скидки [WB Клуба](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task~1club-discount/post).
<br><br>
В одном запросе можно указать более одного артикула.
<br><br>
Используйте отдельные методы, чтобы получить информацию:
  - обо [всех товарах продавца, не указывая артикулы](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1list~1goods~1filter/get)
  - о [размерах товара](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1list~1goods~1size~1nm/get)

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Цены и скидки</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 6 сек | 10 запросов | 600 мс | 5 запросов |

</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `nmList` **(required)** — array<integer>. Артикулы WB для поиска товара

**Пример:**

```json
{
  "nmList": [
    26613989,
    1348041
  ]
}
```

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` **(required)** — object. Данные ответа
  - `listGoods` **(required)** — array<$ref: GoodsList>. Информация о товарах
- `error` **(required)** — boolean; пример: `False`. Флаг ошибки
- `errorText` **(required)** — string; пример: ``. Текст ошибки

```json
{
  "data": {
    "listGoods": [
      {
        "nmID": 98486,
        "vendorCode": "07326060",
        "sizes": [
          {
            "sizeID": 3123515574,
            "price": 500,
            "discountedPrice": 350,
            "clubDiscountedPrice": 332.5,
            "techSizeName": "42"
          }
        ],
        "currencyIsoCode4217": "RUB",
        "discount": 30,
        "clubDiscount": 5,
        "editableSizePrice": true,
        "isBadTurnover": true
      }
    ]
  },
  "error": false,
  "errorText": ""
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*InvalidRequestParameters:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Invalid request parameters"
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

#### 403 — Доступ запрещён

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*AccessDenied:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Access denied"
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
