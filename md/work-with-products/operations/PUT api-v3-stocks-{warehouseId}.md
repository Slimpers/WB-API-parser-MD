# PUT /api/v3/stocks/{warehouseId}

**Обновить остатки товаров{{ /api/v3/stocks/{warehouseId} }}**

теги: `Остатки на складах продавца`

**Полный путь:** `PUT /api/v3/stocks/{warehouseId}`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод обновляет количество остатков товаров продавца [в списке](./work-with-products#tag/Ostatki-na-skladah-prodavca/paths/~1api~1v3~1stocks~1%7BwarehouseId%7D/post).

<div class="description_important">
  Названия параметров запроса не валидируются. При отправке некорректных названий вы получите успешный ответ (<code>204</code>), но остатки не обновятся.
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов <strong>остатков на складах продавца</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `stocks` **(required)** — array<object>. Массив ID размеров товаров и их остатков
  - *(элементы)*
    - `chrtId` — integer; пример: `12345678`. ID размера товара
    - `amount` — integer; пример: `10`. Остаток

**Пример:**

```json
{
  "stocks": [
    {
      "chrtId": 12345678,
      "amount": 10
    }
  ]
}
```

## Ответы


#### 204 — Обновлено


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": "Incorrect required body"
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": "Переданы некорректные данные"
}
```

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "IncorrectParameter"
}
```

*SKUUploadDisabled:*

```json
{
  "code": "SKUUploadDisabled",
  "message": "Uploading stock is not allowed by 'sku'. Please use the 'chrtId' key"
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

#### 404

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "NotFound",
  "message": ""
}
```

#### 406

**Content-Type:** `application/json`

- `code` — string; пример: `StatusNotAcceptable`. Код ошибки
- `message` — string; пример: `Обновление остатков заблокировано в связи с баном поставщика`. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "StatusNotAcceptable",
  "message": "Обновление остатков заблокировано в связи с баном поставщика"
}
```

#### 409 — Ошибка обновления остатков

**Content-Type:** `application/json`

- array of: object
  - `data` — array<object>. Дополнительная информация об ошибке
    - *(элементы)*
      - `sku` — string. Баркод
      - `chrtId` — integer. ID размера товара
      - `amount` — integer. Остаток
  - `code` — string. Код ошибки
  - `message` — string. Описание ошибки

*UploadDataLimit:*

```json
[
  {
    "code": "UploadDataLimit",
    "message": "Upload limit exceeded.",
    "data": [
      {
        "sku": "skuTest2",
        "amount": 100001
      }
    ]
  }
]
```

*CargoWarehouseRestrictionMGT:*

```json
[
  {
    "code": "CargoWarehouseRestrictionMGT",
    "message": "The selected warehouse is not suitable for goods with the type \"LCL (Less than Container Load)\". Upload the balances to the warehouse without the ODC or CD+ mark",
    "data": [
      {
        "sku": "skuTest3",
        "amount": 10
      }
    ]
  }
]
```

*CargoWarehouseRestrictionSGT:*

```json
[
  {
    "code": "CargoWarehouseRestrictionSGT",
    "message": "The selected warehouse is not suitable for goods with the type \"ODC\". Upload the balances to the warehouse marked - ODC",
    "data": [
      {
        "sku": "2042688657617",
        "amount": 0
      }
    ]
  }
]
```

*CargoWarehouseRestrictionSGTKGTPlus:*

```json
[
  {
    "code": "CargoWarehouseRestrictionSGTKGTPlus",
    "message": "The selected warehouse is not suitable for goods with the type \"ODC/CD+\". Upload the balances to the warehouse with the label - ODC or CD+",
    "data": [
      {
        "sku": "skuTest3",
        "amount": 10
      }
    ]
  }
]
```

*CargoWarehouseRestrictionKGTPlus:*

```json
[
  {
    "code": "CargoWarehouseRestrictionKGTPlus",
    "message": "The selected warehouse is not suitable for goods with the type \"CD+\". Upload the balances to the warehouse marked - CD+",
    "data": [
      {
        "sku": "skuTest3",
        "amount": 10
      }
    ]
  }
]
```

*NotFound:*

```json
[
  {
    "code": "NotFound",
    "message": "Not found",
    "data": [
      {
        "sku": "skuTest4",
        "amount": 10
      }
    ]
  }
]
```

*StoreIsProcessing:*

```json
[
  {
    "code": "StoreIsProcessing",
    "message": "The store is processing"
  }
]
```

*ProductPropertyConflict:*

```json
[
  {
    "code": "ProductPropertyConflict",
    "message": "Products are not allowed for sale under the selected supply scheme."
  }
]
```

*DeliveryTypeRestriction:*

```json
[
  {
    "data": [
      {
        "sku": "",
        "chrtId": 123456789,
        "amount": 10
      }
    ],
    "code": "DeliveryTypeRestriction",
    "message": "This product category is not available for sale under this delivery type."
  }
]
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
