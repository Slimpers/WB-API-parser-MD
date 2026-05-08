# GET /api/v1/analytics/goods-return

**Получить отчёт{{ /api/v1/analytics/goods-return }}**

теги: `Отчёт о возвратах и перемещении товаров`

**Полный путь:** `GET /api/v1/analytics/goods-return`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает отчёт о [возвратах товаров продавцу](https://seller.wildberries.ru/analytics-reports/goods-return). <br><br>

Можно получить отчёт максимум за 31 день.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date); пример: `2024-08-13` | да | Дата начала отчётного периода |
| `dateTo` | query | string (date); пример: `2024-08-27` | да | Дата окончания отчётного периода |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `report` — array<object>. Отчёт
  - *(элементы)*
    - `barcode` — string; пример: `1680063403480`. Баркод
    - `brand` — string; пример: `dub`. Бренд
    - `completedDt` — string; пример: `2025-03-31T11:33:53`. Дата и время выдачи возврата продавцу
    - `dstOfficeAddress` — string; пример: `Жуковский Улица Маяковского 19`. Адрес ПВЗ выдачи возврата
    - `dstOfficeId` — integer; пример: `310105`. ID ПВЗ выдачи возврата
    - `expiredDt` — string; пример: `2025-03-31T11:33:53`. Дата и время истечения срока хранения возврата
    - `isStatusActive` — integer; enum: [0, 1]; пример: `0`. Тип статуса возврата:
    - `nmId` — integer; пример: `12862181`. Артикул WB
    - `orderDt` — string (date); пример: `2024-08-26`. Дата заказа на возврат
    - `orderId` — integer; пример: `2034240826`. Номер сборочного задания
    - `readyToReturnDt` — string; пример: `2025-01-31T08:33:50`. Дата и время готовности возврата к выдаче
    - `reason` — string; пример: `Цвет`. Причина возврата
    - `returnType` — string; пример: `Возврат заблокированного товара`. Тип возврата
    - `shkId` — integer; пример: `23411783472`. Штрихкод
    - `srid` — string; пример: `ad3817664d3046c5a8d55054d8be96d6`. Уникальный ID заказа на возврат
    - `status` — string; пример: `В пути в пвз`. Статус возврата
    - `stickerId` — string; пример: `33811984302`. Стикер заказа на возврат
    - `subjectName` — string; пример: `Багажные бирки`. Предмет
    - `techSize` — string; пример: `0`. Размер

```json
{
  "report": [
    {
      "barcode": "1680063403480",
      "brand": "dub",
      "completedDt": "2025-03-31T11:33:53",
      "dstOfficeAddress": "Жуковский Улица Маяковского 19",
      "dstOfficeId": 310105,
      "expiredDt": "2025-03-31T11:33:53",
      "isStatusActive": 0,
      "nmId": 12862181,
      "orderDt": "2024-08-26",
      "orderId": 2034240826,
      "readyToReturnDt": "2025-01-31T08:33:50",
      "reason": "Цвет",
      "returnType": "Возврат заблокированного товара",
      "shkId": 23411783472,
      "srid": "ad3817664d3046c5a8d55054d8be96d6",
      "status": "В пути в пвз",
      "stickerId": "33811984302",
      "subjectName": "Багажные бирки",
      "techSize": "0"
    }
  ]
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
  "detail": "difference between dateFrom and dateTo should be less or equal 31 days",
  "origin": "api-statistics",
  "requestId": "d5a7c02990f5e611728c29293fb6c366",
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
