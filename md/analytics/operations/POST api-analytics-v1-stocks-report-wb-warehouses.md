# POST /api/analytics/v1/stocks-report/wb-warehouses

**Остатки на складах WB{{ /api/analytics/v1/stocks-report/wb-warehouses }}**

`operationId`: postV1StocksReportWbWarehouses  
теги: `История остатков`

**Полный путь:** `POST /api/analytics/v1/stocks-report/wb-warehouses`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_token">Метод доступен по <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">типам токенов</a>:<strong> Персональный</strong>,<strong> Сервисный</strong> </div>

Метод возвращает текущие остатки товаров на складах WB.
<br><br>
Данные обновляются 1 раз в 30 минут.
<br><br>
1 строка ответа — данные об 1 размере товара на 1 складе WB.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 3 запроса | 20 сек | 1 запрос |
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

Параметры запроса текущих остатков на складах WB
- `nmIds` — array<integer (int64)>. Артикулы WB
- `chrtIds` — array<integer (int64)>. ID размеров. Используется только для указанных в массиве `nmIds` артикулов
- `limit` — integer (uint32); пример: `250000`. Количество строк в ответе
- `offset` — integer (uint32); пример: `500000`. Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента

**Пример:**

```json
{
  "nmIds": [
    111222333,
    47254354
  ],
  "chrtIds": [
    111222333,
    91663228
  ],
  "limit": 250000,
  "offset": 500000
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — $ref: InventoryWbResponse

```json
{
  "data": {
    "items": [
      {
        "nmId": 47254354,
        "chrtId": 91663228,
        "warehouseId": 507,
        "warehouseName": "Коледино",
        "regionName": "Центральный",
        "quantity": 43,
        "inWayToClient": 14,
        "inWayFromClient": 11
      }
    ]
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
