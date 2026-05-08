# GET /adv/v1/upd

**Получение истории затрат{{ /adv/v1/upd }}**

теги: `Финансы`

**Полный путь:** `GET /adv/v1/upd`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод формирует список фактических затрат на рекламные кампании за заданный период.

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
| `from` | query | string (date); пример: `2023-07-31` | да | Начало интервала |
| `to` | query | string (date); пример: `2023-08-02` | да | Конец интервала. <br> (Минимальный интервал 1 день, максимальный 31) |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: object
  - `updNum` — integer. Номер выставленного документа
  - `updTime` — string (time-date). Время списания
  - `updSum` — integer. Выставленная сумма
  - `advertId` — integer. ID кампании
  - `campName` — string. Название кампании
  - `advertType` — integer. Тип кампании
  - `paymentType` — string. Источник списания:
  - `advertStatus` — integer. Статус кампании:

```json
[
  {
    "updNum": 0,
    "updTime": "2023-07-31T12:12:54.060536+03:00",
    "updSum": 24,
    "advertId": 3355881,
    "campName": "лук лучок",
    "advertType": 6,
    "paymentType": "Баланс",
    "advertStatus": 9
  },
  {
    "updNum": 0,
    "updTime": null,
    "updSum": 107,
    "advertId": 3366882,
    "campName": "золотая луковица",
    "advertType": 8,
    "paymentType": "Счет",
    "advertStatus": 11
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `text/plain`

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
