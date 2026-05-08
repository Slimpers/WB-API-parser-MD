# POST /api/v1/feedbacks/answer

**Ответить на отзыв{{ /api/v1/feedbacks/answer }}**

теги: `Отзывы`

**Полный путь:** `POST /api/v1/feedbacks/answer`

## Описание

<span>Описание метода</span>

Метод позволяет ответить на [отзыв](./user-communication#tag/Otzyvy/paths/~1api~1v1~1feedbacks/get) покупателя.

  ID отзыва не валидируется. Если в запросе вы передали некорректный ID, вы не получите ошибку.

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

**Content-Type:** `application/json`

- `id` **(required)** — string; пример: `J2FMRjUj6hwvwCElqssz`. ID отзыва
- `text` **(required)** — string; пример: `Спасибо за Ваш отзыв!`. Текст ответа

**Пример:**

```json
{
  "id": "J2FMRjUj6hwvwCElqssz",
  "text": "Спасибо за Ваш отзыв!"
}
```

## Ответы


#### 204 — Успешно


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB
- `detail` — string. Детали ошибки

*contentTypeHeaderNotSpecified:*

```json
{
  "title": "bad request",
  "requestId": "e6c4100223db8bf5818b2e5f12705891",
  "origin": "fbapi",
  "detail": "content-type header not specified"
}
```

*incorrectContentTypeHeader:*

```json
{
  "title": "bad request",
  "requestId": "e3676d061de748d9beaaa752d53e1670",
  "origin": "fbapi",
  "detail": "content-type is not a valid mime-type: u"
}
```

*incorrectContentType:*

```json
{
  "title": "bad request",
  "requestId": "cb4e8b210b4841ce9a3424946b497cb3",
  "origin": "fbapi",
  "detail": "not a json content-type: application/javascript"
}
```

*invalidJsonSyntax:*

```json
{
  "title": "bad request",
  "requestId": "7f5a4faf91634812de5e143955ca0371",
  "origin": "fbapi",
  "detail": "Неверный синтаксис JSON"
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
