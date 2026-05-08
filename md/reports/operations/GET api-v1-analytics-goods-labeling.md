# GET /api/v1/analytics/goods-labeling

**Маркировка товара{{ /api/v1/analytics/goods-labeling }}**

теги: `Отчёты об удержаниях`

**Полный путь:** `GET /api/v1/analytics/goods-labeling`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает отчёт о штрафах за отсутствие обязательной маркировки товаров.<br>

В отчёте представлены фотографии товаров, на которых маркировка отсутствует либо не считывается.<br><br>

Можно получить данные максимум за 31 день. Данные доступны с марта 2024.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `report` — array<object>
  - *(элементы)*
    - `amount` — number. Сумма штрафа, руб
    - `date` — string (date-time). Дата
    - `incomeId` — integer. Номер поставки
    - `nmID` — integer. Артикул WB
    - `photoUrls` — array<string>. URL фото товара
    - `shkID` — integer. Штрихкод товара в WB
    - `sku` — string. Баркод из карточки товара

```json
{
  "report": [
    {
      "amount": 1500,
      "date": "2024-03-26T01:00:00Z",
      "incomeId": 18484008,
      "nmID": 49434732,
      "photoUrls": [
        "https://static-basket-03.wildberries.ru/vol54/photo-fixation-violation-shk-excise/12345678900-1811460999-1.jpg",
        "https://static-basket-03.wildberries.ru/vol54/photo-fixation-violation-shk-excise/12345678900-1811461000-2.jpg",
        "https://static-basket-03.wildberries.ru/vol54/photo-fixation-violation-shk-excise/12345678900-1811461001-3.jpg"
      ],
      "shkID": 17346434621,
      "sku": "4630153500834"
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
