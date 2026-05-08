# GET /api/v1/paid_storage

**Создать отчёт{{ /api/v1/paid_storage }}**

теги: `Платное хранение`

**Полный путь:** `GET /api/v1/paid_storage`

## Описание

<span>Описание метода</span>

Метод создаёт [задание на генерацию](./reports#tag/Platnoe-hranenie/paths/~1api~1v1~1paid_storage~1tasks~1%7Btask_id%7D~1status/get) отчёта о [платном хранении](./reports#tag/Platnoe-hranenie/paths/~1api~1v1~1paid_storage~1tasks~1%7Btask_id%7D~1download/get).

Можно получить отчёт максимум за 8 дней.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 5 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string; пример: `2022-01-01` | да | Начало отчётного периода в формате RFC3339. Можно передать дату или дату со временем. Примеры:    * `2019-06-20`   * `2019-06-20T23:59:59`   * `2019-06-20T00:00:00.12345`   * `2017-03-25T00:00:00` |
| `dateTo` | query | string; пример: `2022-01-09` | да | Конец отчётного периода в формате RFC3339. Можно передать дату или дату со временем. Примеры:    * `2019-06-20`   * `2019-06-20T23:59:59`   * `2019-06-20T00:00:00.12345`   * `2017-03-25T00:00:00` |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — $ref: CreateTaskResponseData

*CreateResponseData:*

```json
{
  "data": {
    "taskId": "219eaecf-e532-4bd8-9f15-8036ec1b042d"
  }
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

*MissingDateTimeFrom:*

```json
{
  "detail": "parameter \"dateFrom\" in query has an error: value is required but missing",
  "origin": "api-statistics",
  "requestId": "320ce05be8ed69060fe4c359a8e77ed6",
  "title": "Bad Request"
}
```

*MissingDateTimeTo:*

```json
{
  "detail": "parameter \"dateTo\" in query has an error: value is required but missing",
  "origin": "api-statistics",
  "requestId": "0e3c2f6760c8d1971760b93ed4213cc4",
  "title": "Bad Request"
}
```

*IncorrectDateTimeFrom:*

```json
{
  "detail": "can't parse dateFrom",
  "origin": "api-statistics",
  "requestId": "31a5d21782082b9f161c4f77fcf9ba33",
  "title": "Bad Request"
}
```

*IncorrectDateTimeTo:*

```json
{
  "detail": "can't parse dateTo",
  "origin": "api-statistics",
  "requestId": "7361df9e49f9821e3de911b5931a136c",
  "title": "Bad Request"
}
```

*DateRangeExceeded:*

```json
{
  "detail": "Difference between dateFrom and dateTo should be less or equal 8 days",
  "origin": "api-statistics",
  "requestId": "f9274b5d8d0a9d50ed9990d73d29f5d2",
  "title": "Bad Request"
}
```

*DateRanges:*

```json
{
  "detail": "dateTo should be greater dateFrom",
  "origin": "api-statistics",
  "requestId": "00725309a5e7566730fd13f756d20d20",
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
