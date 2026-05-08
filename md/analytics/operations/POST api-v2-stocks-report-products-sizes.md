# POST /api/v2/stocks-report/products/sizes

**Данные по размерам{{ /api/v2/stocks-report/products/sizes }}**

теги: `История остатков`

**Полный путь:** `POST /api/v2/stocks-report/products/sizes`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод формирует набор данных об остатках по размерам товара.
<br><br>
Возможны случаи:
1. Товар имеет размеры и `"includeOffice":true`, тогда в ответе будут данные об остатках по каждому из размеров с вложенной детализацией по складам.
2. Товар имеет размеры и `"includeOffice":false`, тогда в ответе будут данные об остатках по каждому из размеров без вложенной детализации по складам.
3. Товар не имеет размера и `"includeOffice":true`, тогда в ответе будет детализация по складам. Без данных об остатках по каждому из размеров.
4. Товар не имеет размера и `"includeOffice":false`, тогда тело ответа будет пустым.<br></br>
Товар не имеет размера, если у него единственный размер с `"techSize":"0"`. В ответах метода получения данных по [товарам](./analytics#tag/Istoriya-ostatkov/paths/~1api~1v2~1stocks-report~1products~1products/post) у таких товаров `"hasSizes":false`.<br></br>
Данные по складам продавца приходят в агрегированном виде — по всем сразу, без детализации по конкретным складам — эти записи будут с `"regionName":"Маркетплейс"` и `"officeName":""`.<br><br>

Данные отчёта обновляются 1 раз в час.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

Параметры запроса об остатках по размерам товара
- $ref: CommonSizeFilters

**Пример:**

```json
{
  "nmID": 123456789,
  "currentPeriod": {
    "start": "2024-02-10",
    "end": "2024-02-10"
  },
  "stockType": "mp",
  "orderBy": {
    "field": "avgOrders",
    "mode": "asc"
  },
  "includeOffice": true
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — $ref: TableSizeResponse

```json
{
  "data": {
    "offices": [
      {
        "regionName": "Центральный",
        "officeID": 123456,
        "officeName": "Коледино"
      }
    ],
    "sizes": [
      {
        "name": "50",
        "chrtID": 123321,
        "offices": [
          {
            "regionName": "Центральный",
            "officeID": 123456,
            "officeName": "Коледино"
          }
        ]
      }
    ],
    "currency": "RUB"
  }
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` **(required)** — string; пример: `Invalid request body`. Заголовок ошибки
- `detail` **(required)** — string; пример: `code=400, message=invalid: positionCluster (field required), limit (field required), offset (field required), internal=invalid: positionCluster (field required), limit (field required), offset (field required`. Детали ошибки
- `requestId` **(required)** — string; пример: `fb25c9e9-cae8-52db-b68e-736c1466a3f5`. Уникальный ID запроса
- `origin` **(required)** — string; пример: `analytic-open-api`. ID внутреннего сервиса WB

```json
{
  "title": "Invalid request body",
  "detail": "code=400, message=invalid: positionCluster (field required), limit (field required), offset (field required), internal=invalid: positionCluster (field required), limit (field required), offset (field required",
  "requestId": "fb25c9e9-cae8-52db-b68e-736c1466a3f5",
  "origin": "analytic-open-api"
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

#### 403 — Доступ запрещён

**Content-Type:** `application/json`

- `title` **(required)** — string; пример: `Authorization error`. Заголовок ошибки
- `detail` **(required)** — string; пример: `Authorization error`. Детали ошибки
- `requestId` **(required)** — string; пример: `fb25c9e9-cae8-52db-b68e-736c1466a3f5`. Уникальный ID запроса
- `origin` **(required)** — string; пример: `analytic-open-api`. ID внутреннего сервиса WB

```json
{
  "title": "Authorization error",
  "detail": "Authorization error",
  "requestId": "fb25c9e9-cae8-52db-b68e-736c1466a3f5",
  "origin": "analytic-open-api"
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
