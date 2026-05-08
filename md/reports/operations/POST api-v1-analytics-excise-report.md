# POST /api/v1/analytics/excise-report

**Получить отчёт{{ /api/v1/analytics/excise-report }}**

теги: `Отчёт о товарах c обязательной маркировкой`

**Полный путь:** `POST /api/v1/analytics/excise-report`

## Описание

<span>Описание метода</span>

Метод возвращает отчёт с [операциями по товарам с обязательной маркировкой](https://seller.wildberries.ru/analytics-reports/excise-report).

Данный отчёт можно сохранить в [формате таблиц](https://dev.wildberries.ru/cases/1).

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 5 ч | 10 запросов | 30 мин | 10 запросов |
| Сервисный | 5 ч | 10 запросов | 30 мин | 10 запросов |
| Базовый | 24 ч | 2 запроса | 12 ч | 1 запрос |

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `countries` — array<string; enum: ["AM", "BY", "KG", "KZ", "RU", "UZ"]>. Код стран по стандарту ISO 3166-2. Чтобы получить данные по всем странам, оставьте параметр пустым

**Пример:**

```json
{
  "countries": [
    "AM",
    "RU"
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `response` — $ref: models.ExciseReportResponse

```json
{
  "response": {
    "data": [
      {
        "name": "Россия",
        "price": 100,
        "currency_name_short": "руб",
        "excise_short": "0102900254680370215_Re/=lSbNiGD",
        "barcode": "2038893425820",
        "nm_id": 169085355,
        "operation_type_id": 1,
        "fiscal_doc_number": 12345678,
        "fiscal_dt": "2024-01-01",
        "rid": 606217433440,
        "srid": "7513432034713632943.1.0"
      }
    ]
  }
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "request body has an error: doesn't match schema #/components/schemas/ExciseReportRequest: Error at \"/countries/0\": value is not one of the allowed values [\"AM\",\"BY\",\"KG\",\"KZ\",\"RU\",\"UZ\"]",
  "origin": "tariffs",
  "requestId": "8bbd7db59522d09926dd059892dbeff0",
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
