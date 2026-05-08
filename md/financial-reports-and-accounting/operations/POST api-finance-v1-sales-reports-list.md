# POST /api/finance/v1/sales-reports/list

**Список отчётов реализации{{ /api/finance/v1/sales-reports/list }}**

`operationId`: postV1SalesReportsList  
теги: `Финансовые отчёты`

**Полный путь:** `POST /api/finance/v1/sales-reports/list`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_token">Метод доступен по <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">типам токенов</a>:<strong> Персональный</strong>,<strong> Сервисный</strong> </div>

Метод возвращает список отчётов релизации по формату [таблицы отчётов](https://seller.wildberries.ru/suppliers-mutual-settlements).
<br><br>
Данные доступны с 1 января 2025 года.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 1 запрос | 1 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

Параметры запроса
- `dateFrom` **(required)** — string; пример: `2026-03-17`. Начальная дата отчёта.<br>Можно передать дату или дату со временем. Время можно указывать с точностью до секунд или миллисекунд.<br>Дата передаётся в формате [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339), время — в часовом поясе Москва `UTC+3`.<br>Примеры:
- `dateTo` **(required)** — string; пример: `2026-03-20`. Конечная дата отчёта.<br>Дата в формате [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339). Можно передать дату или дату со временем. Время можно указывать с точностью до секунд или миллисекунд.<br>Время передаётся в часовом поясе Москва `UTC+3`.<br>Примеры:
- `limit` — integer; пример: `211`. Количество отчётов в ответе
- `offset` — integer; пример: `345`. Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента
- `period` — string; enum: ["daily", "weekly"]; пример: `daily`. Периодичность отчётов:

**Пример:**

```json
{
  "dateFrom": "2026-03-17",
  "dateTo": "2026-03-20",
  "limit": 211,
  "offset": 345,
  "period": "daily"
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: SalesReportListRes

```json
[
  {
    "reportId": 307401554,
    "sellerFinanceName": "ИП Кружинин В. Р.",
    "dateFrom": "2026-03-16",
    "dateTo": "2026-03-22",
    "createDate": "2026-03-23",
    "currency": "RUB",
    "reportType": 1,
    "retailAmountSum": "258",
    "forPaySum": "183.79",
    "avgSalePercent": 0,
    "deliveryServiceSum": "2558.47",
    "paidStorageSum": "626.84",
    "paidAcceptanceSum": "243.81",
    "deductionSum": "150",
    "penaltySum": "1457.61",
    "additionalPaymentSum": "9509.71",
    "cashbackAmountSum": "2",
    "cashbackDiscountSum": "19",
    "cashbackCommissionChangeSum": "0.2",
    "paymentSchedule": "-1",
    "bankPaymentSum": "5172.94"
  }
]
```

#### 204 — Нет данных


#### 400

**Content-Type:** `application/problem+json`

- `status` — integer; пример: `400`. HTTP статус-код
- `title` — string; пример: `GetReportDetailByPeriodNB decode error`. Заголовок ошибки
- `detail` — string; пример: `GetReportDetailByPeriodNB decode error: missing dateTo params`. Детали ошибки
- `requestId` — string; пример: `b065c204-c5f7-431b-b12c-d4c2cc6347ec`. ID запроса
- `origin` — string; пример: `open-api-finreports`. ID внутреннего сервиса WB

```json
{
  "status": 400,
  "title": "GetReportDetailByPeriodNB decode error",
  "detail": "GetReportDetailByPeriodNB decode error: missing dateTo params",
  "requestId": "b065c204-c5f7-431b-b12c-d4c2cc6347ec",
  "origin": "open-api-finreports"
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
