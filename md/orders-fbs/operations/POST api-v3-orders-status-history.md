# POST /api/v3/orders/status/history

**История статусов для сборочных заданий трансграничных поставок{{ /api/v3/orders/status/history }}**

теги: `Сборочные задания FBS`

**Полный путь:** `POST /api/v3/orders/status/history`

## Описание

<span>Описание метода</span>

Метод возвращает историю [статусов](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1status/post) для [сборочных заданий](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) трансграничных поставок.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` — array<integer>. ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    123456789,
    987654321
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<object>. Список сборочных заданий
  - *(элементы)*
    - `deliveryDate` — string (date-time). Планируемая дата доставки, [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339)
    - `statuses` — array<object>. Статусы
      - *(элементы)*
        - `date` — string. Дата присвоения статуса
        - `code` — string; пример: `SORTED`. Статус-код сборочного задания/заказа:
    - `orderID` — integer; пример: `123456789`. ID сборочного задания

```json
{
  "orders": [
    {
      "statuses": [
        {
          "code": "SORTED"
        }
      ],
      "orderID": 123456789
    }
  ]
}
```

#### 400 — Неправильный запрос


#### 401

**Content-Type:** `application/json`

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
  "message": "Доступ запрещён"
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
  "message": "Не найдено"
}
```

#### 429

**Content-Type:** `application/json`

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
