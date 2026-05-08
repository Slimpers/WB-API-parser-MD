# GET /adv/v1/balance

**Баланс{{ /adv/v1/balance }}**

теги: `Финансы`

**Полный путь:** `GET /adv/v1/balance`

## Описание

<span>Описание метода</span>

Метод возвращает информацию о:
  - счёте кабинета Продвижения WB. Его пополняет продавец.
  - балансе — максимальной сумме для оплаты кампании по взаиморасчету: удержании средств из будущих продаж. Баланс пополнить нельзя, он рассчитывается автоматически на основе отчётов по продвижению.
  - бонусных начислениях WB.

Информацию о бюджете кампаний можно получить в [отдельном методе](./promotion#tag/Finansy/paths/~1adv~1v1~1budget/get).

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Сервисный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `balance` — integer. Счёт, ₽
- `net` — integer. Баланс, ₽
- `bonus` — integer. Бонусы, ₽
- `cashbacks` — array<object>. Промо-бонусы
  - *(элементы)*
    - `sum` — integer. Промо-бонусы, ₽
    - `percent` — integer. Процент от суммы пополнения бюджета кампании, который можно оплатить промо-бонусами за один раз
    - `expiration_date` — string (ISO 8601). Дата окончания действия промо-бонусов

```json
{
  "balance": 11083,
  "net": 0,
  "bonus": 15187,
  "cashbacks": [
    {
      "sum": 10672,
      "percent": 50,
      "expiration_date": "2026-04-17T10:46:02.176174Z"
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- string

*IncorrectSupplierIdAdv:*

```json
"Некорректный ID продавца"
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
