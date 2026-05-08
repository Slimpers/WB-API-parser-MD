# POST /api/v1/acceptance/options

**Опции приёмки{{ /api/v1/acceptance/options }}**

теги: `Информация для формирования поставок`

**Полный путь:** `POST /api/v1/acceptance/options`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о том, какие склады и типы упаковки доступны для поставки. Список складов определяется по баркоду и количеству товара.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 6 запросов | 10 сек | 6 запросов |
| Сервисный | 1 мин | 6 запросов | 10 сек | 6 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `warehouseID` | query | integer | нет | ID склада. <br> Если параметр не указан, возвращаются данные по всем складам.<br> **Максимум одно значение** |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- array of: $ref: models.Good

**Пример «RequestOptions»:**

```json
[
  {
    "quantity": 1,
    "barcode": "k"
  },
  {
    "quantity": 7,
    "barcode": "1111111111"
  }
]
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `result` — array<object>
  - *(элементы)*
    - `barcode` — string. Баркод из карточки товара
    - `error` — object. Данные ошибки. При наличии
      - `title` — string. ID ошибки
      - `detail` — string. Описание ошибки
    - `isError` — boolean. Наличие ошибки:
    - `warehouses` — array<object>. Список складов. При наличии ошибки будет `null`
      - *(элементы)*
        - `warehouseID` — integer. ID склада. По нему можно получить [информацию о складе](./orders-fbw#tag/Informaciya-dlya-formirovaniya-postavok/paths/~1api~1v1~1warehouses/get)
        - `canBox` — boolean. Тип упаковки **Короб**:
        - `canMonopallet` — boolean. Тип упаковки **Монопаллета**:
        - `canSupersafe` — boolean. Тип упаковки **Суперсейф**:
        - `isBoxOnPallet` — boolean. Тип поставки **Поштучная палета**:
- `requestId` — string. ID запроса при наличии ошибок

*Response:*

```json
{
  "result": [
    {
      "barcode": "Seller",
      "warehouses": null,
      "error": {
        "title": "barcode validation error",
        "detail": "barcode Seller is not found"
      },
      "isError": true
    },
    {
      "barcode": "123456789",
      "warehouses": [
        {
          "warehouseID": 205349,
          "canBox": true,
          "canMonopallet": false,
          "canSupersafe": false,
          "isBoxOnPallet": false
        },
        {
          "warehouseID": 211622,
          "canBox": false,
          "canMonopallet": true,
          "canSupersafe": false,
          "isBoxOnPallet": true
        },
        {
          "warehouseID": 214951,
          "canBox": true,
          "canMonopallet": false,
          "canSupersafe": false,
          "isBoxOnPallet": true
        },
        {
          "warehouseID": 206319,
          "canBox": true,
          "canMonopallet": false,
          "canSupersafe": false,
          "isBoxOnPallet": true
        }
      ]
    }
  ],
  "requestId": "kr53d2bRKYmkK2N6zaNKHs"
}
```

#### 400 — Некорректный запрос

**Content-Type:** `application/json`

- `status` — integer. HTTP статус-код
- `title` — string. ID ошибки
- `detail` — string. Описание ошибки
- `requestId` — string. ID запроса
- `origin` — string. Сервис, вернувший ошибку

*BadWarehouseIDsParam:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Неверный формат warehouseID",
  "requestId": "a6bdc2a4d2fde51c2036fa8af2483886",
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

#### 403 — Доступ запрещён


#### 404 — Не найдено


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
