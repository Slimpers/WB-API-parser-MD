# GET /adv/v1/payments

**Получение истории пополнений счёта{{ /adv/v1/payments }}**

теги: `Финансы`

**Полный путь:** `GET /adv/v1/payments`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает историю пополнений счёта **WB Продвижение** за заданный период.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Сервисный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `from` | query | string (date); пример: `2023-07-31` | нет | Начало интервала |
| `to` | query | string (date); пример: `2023-08-02` | нет | Конец интервала. <br> (Минимальный интервал 1 день, максимальный 31) |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: object
  - `id` — integer. ID платежа
  - `date` — string (time-date). Дата платежа
  - `sum` — integer. Сумма платежа
  - `type` — integer. Тип источника списания:
  - `statusId` — integer. Статус:
  - `cardStatus` — string. Статус операции(при оплате картой):

```json
[
  {
    "id": 1036666,
    "date": "2022-02-04T09:06:47.985843Z",
    "sum": 600,
    "type": 0,
    "statusId": 1,
    "cardStatus": ""
  },
  {
    "id": 55261296,
    "date": "2023-04-13T10:07:42",
    "sum": 1500,
    "type": 3,
    "statusId": 1,
    "cardStatus": "succeeded"
  }
]
```

#### 204 — История пополнений счета не найдена


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
