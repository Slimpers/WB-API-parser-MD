# GET /api/v1/seller-info

**Получить информацию о продавце{{ /api/v1/seller-info }}**

теги: `Информация о продавце`

**Полный путь:** `GET /api/v1/seller-info`

## Описание

<span>Описание метода</span>

  Информацию о продавце можно получить с <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токеном</a> любой категории

Метод позволяет получать наименование продавца и ID его профиля.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 24 ч | 1 запрос | 24 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `name` — string. Наименование продавца
- `sid` — string (UUID). Уникальный ID продавца на Wildberries, [находящийся в публичном поле токена](./api-information#tag/Avtorizaciya/Kak-ustroen-token)
- `tin` — string. ИНН
- `tradeMark` — string. Торговое наименование продавца

```json
{
  "name": "ИП Кружинин В. Р.",
  "sid": "e8923014-e233-47q8-898e-3cc86d67ea61",
  "tin": "1234567890",
  "tradeMark": "Flax Store"
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
