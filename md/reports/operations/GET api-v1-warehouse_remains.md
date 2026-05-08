# GET /api/v1/warehouse_remains

**Создать отчёт{{ /api/v1/warehouse_remains }}**

теги: `Отчёт об остатках на складах`

**Полный путь:** `GET /api/v1/warehouse_remains`

## Описание

<span>Описание метода</span>

Метод создаёт [задание на генерацию](./reports#tag/Otchyot-ob-ostatkah-na-skladah/paths/~1api~1v1~1warehouse_remains~1tasks~1%7Btask_id%7D~1status/get) отчёта об [остатках на складах WB](./reports#tag/Otchyot-ob-ostatkah-na-skladah/paths/~1api~1v1~1warehouse_remains~1tasks~1%7Btask_id%7D~1download/get).

Параметры `groupBy` и `filter` (группировки и фильтры) можно задать в любой комбинации — аналогично [версии](https://seller.wildberries.ru/analytics-reports/warehouse-remains) в личном кабинете.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 5 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 5 запросов |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `locale` | query | string; пример: `ru` | нет | Язык полей ответа `subjectName` и `warehouseName`:   - `ru` — русский   - `en` — английский   - `zh` — китайский. Значения `warehouseName` на английском |
| `groupByBrand` | query | boolean; пример: `True` | нет | Разбивка по брендам |
| `groupBySubject` | query | boolean; пример: `True` | нет | Разбивка по предметам |
| `groupBySa` | query | boolean; пример: `True` | нет | Разбивка по артикулам продавца |
| `groupByNm` | query | boolean; пример: `True` | нет | Разбивка по артикулам WB. Если `groupByNm=true`, в ответе будет поле `volume` |
| `groupByBarcode` | query | boolean; пример: `True` | нет | Разбивка по баркодам |
| `groupBySize` | query | boolean; пример: `True` | нет | Разбивка по размерам |
| `filterPics` | query | integer; пример: `1` | нет | Фильтр по фото:   - `-1` — без фото   - `0` — не применять фильтр   - `1` — с фото |
| `filterVolume` | query | integer; пример: `3` | нет | Фильтр по объёму:   - `-1` — без габаритов   - `0` — не применять фильтр   - `3` — свыше трёх литров |

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

**Content-Type:** `application/json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "parameter \"groupByNm\" in query has an error: empty value is not allowed",
  "origin": "api-statistics",
  "requestId": "6a6c2fba81f08e58670a7dab835ff0d7",
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
