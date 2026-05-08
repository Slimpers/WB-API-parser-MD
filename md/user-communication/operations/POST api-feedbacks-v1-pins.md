# POST /api/feedbacks/v1/pins

**Закрепить отзывы{{ /api/feedbacks/v1/pins }}**

теги: `Закреплённые отзывы`

**Полный путь:** `POST /api/feedbacks/v1/pins`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод позволяет закрепить отзывы в карточке товара или в группе [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек. <br>
Чтобы получить ID отзывов, используйте метод [Список закреплённых и откреплённых отзывов](./user-communication#tag/Zakreplyonnye-otzyvy/paths/~1api~1feedbacks~1v1~1pins/get).<br>
<br>
Метод доступен по [подписке Джем](https://seller.wildberries.ru/monetization/jam) или c [тарифной опцией](https://seller.wildberries.ru/tariff-constructor) **Закрепление отзыва**.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Вопросы и отзывы</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Сервисный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- array of: $ref: openapi.PinReviewItem

**Пример:**

```json
[
  {
    "pinMethod": "subscription",
    "pinOn": "imt",
    "feedbackId": "VlbkVVl7mtw37wуWkJZz"
  },
  {
    "pinMethod": "tariff",
    "pinOn": "imt",
    "feedbackId": "DibuRAImknLyiqgzvGcU"
  }
]
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `requestId` **(required)** — string. ID запроса
- `status` **(required)** — integer. HTTP статус-код
- `title` **(required)** — string. Заголовок ошибки

```json
{
  "detail": "invalid request body",
  "origin": "pin-open-api",
  "requestId": "7b64у8ffc3523450d613723fwу61873e",
  "status": 400,
  "title": "Bad Request"
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

- `detail` — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `requestId` **(required)** — string. ID запроса
- `status` **(required)** — integer. HTTP статус-код
- `title` **(required)** — string. Заголовок ошибки

```json
{
  "origin": "pin-open-api",
  "requestId": "7b64у8ffc3523450d613723fwу61873e",
  "status": 403,
  "title": "no active subscription or tariff",
  "detail": "this feature requires active subscription or active tariff"
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
