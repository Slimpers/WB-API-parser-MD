# POST /api/v1/documents/download/all

**Получить документы{{ /api/v1/documents/download/all }}**

теги: `Документы`

**Полный путь:** `POST /api/v1/documents/download/all`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод загружает несколько документов из [списка документов продавца](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1list/get).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 5 мин | 1 запрос | 5 мин | 5 запросов |
| Сервисный | 5 мин | 1 запрос | 5 мин | 5 запросов |
| Базовый | 24 ч | 1 запрос | 24 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `params` — array<object>
  - *(элементы)*
    - `extension` — string. Формат документа
    - `serviceName` — string. Уникальный ID документа

**Пример:**

```json
{
  "params": [
    {
      "extension": "zip",
      "serviceName": "redeem-notification-44841941"
    },
    {
      "extension": "xlsx",
      "serviceName": "act-income-mp-392460936"
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `fileName` — string; пример: `documents.zip`. Название документа
  - `extension` — string; пример: `zip`. Формат документа
  - `document` — string; пример: `UEsDBBQACAgIAAAAAAAAAAAAAAAAAAAAAABHAAAA0KPQstC10LTQvtC80LvQtdC90LjQtSDQviDQstGL0LrRg9C/0LUg4oSWNDQ4NDE5NDEg0L7RgiAyNS4wOS4yMDIzLnhsc3jsnQk0lP3f/0dEUiRkNwmVECI7o0WS7EklxprdkH2bKVkqISRkGSlkaxRlN2TPnmzJvu/Gzmz/Uz33fY/L8/Q8zrn/x/07565zcjrn9f1cn/V6f69v53zTVCWnYATtA+0DAX/Rg0AgM5ip5l2Yg5OwKeyu+Wl3O1vbcA3YV5FDVfPej2vXKptOK1V9LjycmPDG72uW4vcG9xdsOI1V2wj86sk6+4nHJeZ92NFgC/He3gmDlccFXSyumXYUGSKK4hLLsqu5aBTspu5lqlcGB/JNlQVn1Eumj6o8ZEWPRotEVGkH9/kf457totEKj2N2P4dSZWAIaC0ajy5J+VL5fen1YOhcGMxvvUw+XOKFOHL...LSL/tC77s0GzTi2iBuHorbMpcOaw0Hmsc/gpk7ty3/cdDYRmhkRUPAIC37P94CA8oiP/fIvpPK8n9l43YARWRgH/tI6E3ntD/nfOfPyj9jxxDwn+b8/8dZqBDQPjPNSAACJgBAAD21P9s/y8AAP//UEsHCFHrudyQEwAASxQAAFBLAQIUABQACAgIAAAAAACH4v2BaSgAAGNjAABHAAAAAAAAAAAAAAAAAAAAAADQo9Cy0LXQtNC+0LzQu9C10L3QuNC1INC+INCy0YvQutGD0L/QtSDihJY0NDg0MTk0MSDQvtGCIDI1LjA5LjIwMjMueGxzeFBLAQIUABQACAgIAAAAAADTmLxwRQcAAGAPAABLAAAAAAAAAAAAAAAAAN4oAADQo9Cy0LXQtNC+0LzQu9C10L3QuNC1INC+INCy0YvQutGD0L/QtSDihJY0NDg0MTk0MSDQvtGCIDI1LjA5LjIwMjMueGxzeC5zaWdQSwECFAAUAAgACAAAAAAAUeu53JATAABLFAAACAAAAAAAAAAAAAAAAACcMAAAbWNoZC56aXBQSwUGAAAAAAMAAwAkAQAAYkQAAAAA`. Документ в кодировке base64

```json
{
  "data": {
    "fileName": "documents.zip",
    "extension": "zip",
    "document": "UEsDBBQACAgIAAAAAAAAAAAAAAAAAAAAAABHAAAA0KPQstC10LTQvtC80LvQtdC90LjQtSDQviDQstGL0LrRg9C/0LUg4oSWNDQ4NDE5NDEg0L7RgiAyNS4wOS4yMDIzLnhsc3jsnQk0lP3f/0dEUiRkNwmVECI7o0WS7EklxprdkH2bKVkqISRkGSlkaxRlN2TPnmzJvu/Gzmz/Uz33fY/L8/Q8zrn/x/07565zcjrn9f1cn/V6f69v53zTVCWnYATtA+0DAX/Rg0AgM5ip5l2Yg5OwKeyu+Wl3O1vbcA3YV5FDVfPej2vXKptOK1V9LjycmPDG72uW4vcG9xdsOI1V2wj86sk6+4nHJeZ92NFgC/He3gmDlccFXSyumXYUGSKK4hLLsqu5aBTspu5lqlcGB/JNlQVn1Eumj6o8ZEWPRotEVGkH9/kf457totEKj2N2P4dSZWAIaC0ajy5J+VL5fen1YOhcGMxvvUw+XOKFOHL...LSL/tC77s0GzTi2iBuHorbMpcOaw0Hmsc/gpk7ty3/cdDYRmhkRUPAIC37P94CA8oiP/fIvpPK8n9l43YARWRgH/tI6E3ntD/nfOfPyj9jxxDwn+b8/8dZqBDQPjPNSAACJgBAAD21P9s/y8AAP//UEsHCFHrudyQEwAASxQAAFBLAQIUABQACAgIAAAAAACH4v2BaSgAAGNjAABHAAAAAAAAAAAAAAAAAAAAAADQo9Cy0LXQtNC+0LzQu9C10L3QuNC1INC+INCy0YvQutGD0L/QtSDihJY0NDg0MTk0MSDQvtGCIDI1LjA5LjIwMjMueGxzeFBLAQIUABQACAgIAAAAAADTmLxwRQcAAGAPAABLAAAAAAAAAAAAAAAAAN4oAADQo9Cy0LXQtNC+0LzQu9C10L3QuNC1INC+INCy0YvQutGD0L/QtSDihJY0NDg0MTk0MSDQvtGCIDI1LjA5LjIwMjMueGxzeC5zaWdQSwECFAAUAAgACAAAAAAAUeu53JATAABLFAAACAAAAAAAAAAAAAAAAACcMAAAbWNoZC56aXBQSwUGAAAAAAMAAwAkAQAAYkQAAAAA"
  }
}
```

#### 400

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `status` — number. HTTP статус-код
- `detail` — string. Детализация ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB

*badRequestBodyElement:*

```json
{
  "title": "Bad Request",
  "status": 400,
  "detail": "request body must contain at least one element with serviceName and extension",
  "requestId": "6c364410-625c-4493-a434-8cbe79dfbf18",
  "origin": "docs-public-api"
}
```

*badRequestBodyElementCount:*

```json
{
  "title": "Bad Request",
  "status": 400,
  "detail": "documents count must be less than or equal to 50",
  "requestId": "0cf25b67-865e-4126-b971-1ff2e17fe84a",
  "origin": "docs-public-api"
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
