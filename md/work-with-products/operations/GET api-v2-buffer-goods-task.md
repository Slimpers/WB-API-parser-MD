# GET /api/v2/buffer/goods/task

**Детализация необработанной загрузки{{ /api/v2/buffer/goods/task }}**

теги: `Цены и скидки`

**Полный путь:** `GET /api/v2/buffer/goods/task`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о товарах и ошибках в товарах из загрузки в обработке.

<div class="description_important">
  Необработанная загрузка — это загрузка скидок в <a href="./promotion#tag/Kalendar-akcij">календаре акций</a>. Такие скидки применятся к товарам только в момент старта акции.
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Цены и скидки</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Сервисный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - `uploadID` — integer; пример: `3235236546`. ID загрузки
  - `bufferGoods` — array<$ref: GoodBufferHistory>. Информация о товарах в загрузке
- `error` — boolean; пример: `False`. Флаг ошибки
- `errorText` — string; пример: ``. Текст ошибки

```json
{
  "data": {
    "uploadID": 3235236546,
    "bufferGoods": [
      {
        "nmID": 544833232,
        "vendorCode": "34552332",
        "sizeID": 54483342,
        "techSizeName": "XXL",
        "price": 1500,
        "currencyIsoCode4217": "RUB",
        "discount": 25,
        "clubDiscount": 5,
        "status": 1
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
