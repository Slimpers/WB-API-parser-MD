# GET /api/v1/analytics/brand-share/parent-subjects

**Родительские категории бренда{{ /api/v1/analytics/brand-share/parent-subjects }}**

теги: `Доля бренда в продажах`

**Полный путь:** `GET /api/v1/analytics/brand-share/parent-subjects`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает родительские категории бренда продавца для отчёта о [доле бренда в продажах](https://seller.wildberries.ru/analytics-reports/brand-share).<br><br>

Можно получить отчёт максимум за 365 дней. Данные доступны с 1 ноября 2022.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 5 сек | 1 запрос | 5 сек | 20 запросов |
| Сервисный | 5 сек | 1 запрос | 5 сек | 20 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `locale` | query | string; пример: `ru` | нет | Язык поля ответа `parentName`:   - `ru` — русский   - `en` — английский   - `zh` — китайский |
| `brand` | query | string; пример: `H%26M` | да | Бренд |
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — array<object>. Категории бренда
  - *(элементы)*
    - `parentId` — integer. ID родительской категории
    - `parentName` — string. Название родительской категории

```json
{
  "data": [
    {
      "parentId": 3,
      "parentName": "Аксессуары"
    },
    {
      "parentId": 7,
      "parentName": "Игрушки"
    },
    {
      "parentId": 1,
      "parentName": "Одежда"
    },
    {
      "parentId": 239,
      "parentName": "Спортивный товар"
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

*IncorrectDateFrom:*

```json
{
  "detail": "date cannot be earlier than 2022-11-01",
  "origin": "api-statistics",
  "requestId": "68472ed47542fb51572de64273075bc0",
  "title": "Bad Request"
}
```

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
  "detail": "difference between dateFrom and dateTo should be less or equal 365 days",
  "origin": "api-statistics",
  "requestId": "cfd15c87683c88203e79a47f6774ff08",
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

*LocaleError:*

```json
{
  "detail": "parameter \"locale\" in query has an error: value is not one of the allowed values [\"ru\",\"en\",\"zh\"]",
  "origin": "api-statistics",
  "requestId": "af5b14cceb985597464ce500137bc1af",
  "title": "Bad Request"
}
```

*MissingBrand:*

```json
{
  "detail": "parameter \"brand\" in query has an error: value is required but missing",
  "origin": "api-statistics",
  "requestId": "e358b83254107a12f4bd39361379b9a0",
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
