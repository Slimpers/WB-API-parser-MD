# POST /api/v1/feedbacks/order/return

**Возврат товара по ID отзыва{{ /api/v1/feedbacks/order/return }}**

теги: `Отзывы`

**Полный путь:** `POST /api/v1/feedbacks/order/return`

## Описание

<span>Описание метода</span>

Метод запрашивает возврат товара, по которому оставлен [отзыв](./user-communication#tag/Otzyvy/paths/~1api~1v1~1feedbacks/get).

Возврат доступен для отзывов с полем `"isAbleReturnProductOrders": true`.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Вопросы и отзывы</strong>:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Сервисный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `feedbackId` — string. ID отзыва

**Пример:**

```json
{
  "feedbackId": "absdfgerrrfff1234"
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*FeedbackErr400:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Не удалось получить отзыв",
  "additionalErrors": null,
  "requestId": "958d9676-b50c-41d6-b7ce-3c9f0bc3b822"
}
```

*RequestBodyErr400:*

```json
{
  "data": null,
  "error": true,
  "errorText": "failed to decode JSON request.",
  "additionalErrors": null,
  "requestId": "958d9676-b50c-41d6-b7ce-3c9f0bc3b822"
}
```

*RequestIDErr400:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Неправильный id в запросе",
  "additionalErrors": null,
  "requestId": "958d9676-b50c-41d6-b7ce-3c9f0bc3b822"
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

#### 422 — Ошибка обработки параметров запроса

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*responseInaccessibleBackGoodError422:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Запрос на возврат покупок недоступен",
  "additionalErrors": null,
  "requestId": "f551e94d-9bd5-431d-a4b6-b78106fe6348"
}
```

*responseUnsuccessfullyBackGoodError422:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Не удалось выполнить запрос на возврат покупок",
  "additionalErrors": null,
  "requestId": "93ea349d-d0ec-41b0-aaac-a8f5f137a109"
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
