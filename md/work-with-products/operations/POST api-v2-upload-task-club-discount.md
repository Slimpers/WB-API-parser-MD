# POST /api/v2/upload/task/club-discount

**Установить скидки WB Клуба{{ /api/v2/upload/task/club-discount }}**

теги: `Цены и скидки`

**Полный путь:** `POST /api/v2/upload/task/club-discount`

## Описание

<span>Описание метода</span>

Устанавливает скидки для товаров в рамках подписки [WB Клуб](https://seller.wildberries.ru/help-center/article/A-337).

  Получить информацию о процессе установки цен и скидок можно с помощью методов <a href="./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1history~1tasks/get">состояния</a> и <a href="./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1history~1goods~1task/get">детализации</a> обработанной загрузки.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Цены и скидки</strong>:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Сервисный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `data` **(required)** — $ref: ClubDisc

**Пример:**

```json
{
  "data": [
    {
      "nmID": 123,
      "clubDiscount": 5
    }
  ]
}
```

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - `id` — integer. ID загрузки
  - `alreadyExists` — boolean; пример: `False`. Флаг дублирования загрузки: `true` — такая загрузка уже есть
- `error` — boolean; пример: `False`. Флаг ошибки
- `errorText` — string; пример: ``. Текст ошибки

```json
{
  "data": {
    "alreadyExists": false
  },
  "error": false,
  "errorText": ""
}
```

#### 208

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - `id` — integer. ID загрузки
  - `alreadyExists` — boolean. Флаг дублирования загрузки: `true` — такая загрузка уже есть
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*This task already exists:*

```json
{
  "data": {
    "id": 1111111,
    "alreadyExists": true
  },
  "error": false,
  "errorText": "This task already exists"
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*CheckTheWBClubDiscount:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Check the field values in the WB Club Discount column. Field format: a whole number between {{.WbClubMinDiscount}} and {{.WbClubMaxDiscount}}, without dots or commas"
}
```

*DiscountsAreTheSameAsThoseAlreadySet:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Discounts in the file are the same as those already set. To change discounts, edit the file and upload it again"
}
```

*AllItemNosAreSpecifiedIncorrectlyOrDiscounts:*

```json
{
  "data": null,
  "error": true,
  "errorText": "All item Nos. are specified incorrectly, or the specified discounts are already set"
}
```

*InvalidDiscountValue:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Invalid discount value"
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

#### 409 — Ошибка при конвертации валюты

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*CurrencySwitchingError:*

```json
{
  "data": null,
  "error": true,
  "errorText": "You can't change prices and discounts while switching to another currency"
}
```

#### 422 — Неожидаемый результат

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*UnexpectedResult:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Unexpected result"
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
