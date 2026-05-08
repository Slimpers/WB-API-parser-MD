# GET /ping

**Проверка подключения{{ /ping }}**

теги: `Проверка подключения к WB API`

**Полный путь:** `GET /ping`

## Описание

<span>Описание метода</span>

Метод проверяет:
  1. Успешно ли запрос доходит до WB API
  2. Валидность токена авторизации и URL запроса
  3. Совпадают ли категория токена и сервис

  Метод не предназначен для проверки доступности сервисов WB

У каждого сервиса есть свой вариант метода в зависимости от домена:

| Категория | URL запроса |
|---------------|-----------------------|
| Контент | `https://content-api.wildberries.ru/ping`
`https://content-api-sandbox.wildberries.ru/ping` |
| Аналитика | `https://seller-analytics-api.wildberries.ru/ping` |
| Цены и скидки | `https://discounts-prices-api.wildberries.ru/ping`
`https://discounts-prices-api-sandbox.wildberries.ru/ping` |
| Маркетплейс | `https://marketplace-api.wildberries.ru/ping` |
| Статистика | `https://statistics-api.wildberries.ru/ping`
`https://statistics-api-sandbox.wildberries.ru/ping` |
| Продвижение | `https://advert-api.wildberries.ru/ping`
`https://advert-api-sandbox.wildberries.ru/ping` |
| Вопросы и отзывы | `https://feedbacks-api.wildberries.ru/ping`
`https://feedbacks-api-sandbox.wildberries.ru/ping` |
| Чат с покупателями | `https://buyer-chat-api.wildberries.ru/ping` |
| Поставки | `https://supplies-api.wildberries.ru/ping` |
| Возвраты покупателями | `https://returns-api.wildberries.ru/ping` |
| Документы | `https://documents-api.wildberries.ru/ping` |
| Финансы | `https://finance-api.wildberries.ru/ping` |
| Тарифы, Новости, Получить информацию о продавце | `https://common-api.wildberries.ru/ping` |
| Управление пользователями продавца | `https://user-management-api.wildberries.ru/ping` |

  Максимум 3 запроса за 30 <a href='./api-information#tag/Vvedenie/Limity-zaprosov'>секунд</a>. Если попытаться автоматизировать использование метода, запросы будут временно заблокированы. Лимит действует отдельно для каждого варианта метода в зависимости от домена

## Авторизация

- `HeaderApiKey` (scopes: —)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `TS` — string. Timestamp запроса
- `Status` — string; enum: ["OK"]. Статус

```json
{
  "TS": "2024-08-16T11:19:05+03:00",
  "Status": "OK"
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
