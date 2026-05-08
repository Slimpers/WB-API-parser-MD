# GET /api/analytics/v1/warehouse-measurements

**Замеры склада{{ /api/analytics/v1/warehouse-measurements }}**

`operationId`: getWarehouseMeasurements  
теги: `Отчёты об удержаниях`

**Полный путь:** `GET /api/analytics/v1/warehouse-measurements`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает отчёт о [замерах склада](https://seller.wildberries.ru/analytics-reports/dimensions-penalties/warehouse-measurements)

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Сервисный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Базовый | 6 ч | 1 запрос | 6 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | нет | Начало отчётного периода. По умолчанию используется дата, когда были впервые получены данные для отчёта |
| `dateTo` | query | string (date-time) | да | Конец отчётного периода |
| `limit` | query | integer; пример: `330` | да | Количество замеров в ответе |
| `offset` | query | integer; пример: `220` | нет | Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — object. Данные ответа
  - `reports` **(required)** — array<object>. Замеры
    - *(элементы)*
      - `nmId` — integer; пример: `123456789`. Артикул WB
      - `subjectName` — string; пример: ``. Предмет
      - `dimId` — integer; пример: `123456789`. ID замера
      - `volume` — number. Объём, л
      - `width` — integer; пример: `66`. Ширина, см
      - `length` — integer; пример: `54`. Длина, см
      - `height` — integer; пример: `11`. Высота, см
      - `photoUrls` — array<string>. Фото замеров
      - `dt` — string (date-time); пример: `2025-04-01T00:06:00Z`. Дата и время
  - `total` **(required)** — integer; пример: `11`. Количество замеров в отчёте. Без учёта `limit` и `offset`

*Measurements:*

```json
{
  "data": {
    "reports": [
      {
        "nmId": 9234567089,
        "subjectName": "Чемоданы",
        "dimId": 4983331,
        "volume": 16.25,
        "width": 26,
        "length": 25,
        "height": 25,
        "photoUrls": [
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/282504229_98bd4653-cc2e-496c-7aee-e035c2329ac0.jpg",
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/282504229_55f71345-58d9-48ef-6ae8-548e34abefc9.jpg",
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/282504229_576b1f5b-5245-4e55-4ff4-351fc7a77f72.jpg"
        ],
        "dt": "2025-06-05T00:00:00Z"
      },
      {
        "nmId": 9234560789,
        "subjectName": "Платья",
        "dimId": 86840305,
        "volume": 39.2,
        "width": 66,
        "length": 54,
        "height": 11,
        "photoUrls": [
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/8906416_a9f839da-c3b7-4ea6-737c-a9e731250fb0.jpg",
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/8906416_2aac23b7-c8f9-42db-74e9-b4a9c916017c.jpg",
          "https://static-basket-03.wb.ru/vol54/handheld-goods-measurements-photo/8906416_ff93b7c4-19d6-e0a2-4dba-7c2f09f06b3.jpg"
        ],
        "dt": "2025-04-01T00:06:00Z"
      }
    ],
    "total": 2
  }
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` — string; пример: `bad request`. Заголовок ошибки
- `status` — integer; пример: `400`. HTTP статус-код
- `detail` — string; пример: `invalid parameter: dateTo`. Детали ошибки
- `requestId` — string; пример: `31db50b5-14c0-4f4e-965e-6e1f9607ee78`. Уникальный ID запроса
- `origin` — string; пример: `dimension-penalty`. ID внутреннего сервиса WB

```json
{
  "title": "bad request",
  "status": 400,
  "detail": "invalid parameter: dateTo",
  "requestId": "31db50b5-14c0-4f4e-965e-6e1f9607ee78",
  "origin": "dimension-penalty"
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

- `title` — string; пример: `access denied`. Заголовок ошибки
- `status` — integer; пример: `403`. HTTP статус-код
- `detail` — string; пример: `abac: access denied`. Детали ошибки
- `requestId` — string; пример: `31db50b5-14c0-4f4e-965e-6e1f9607ee78`. Уникальный ID запроса
- `origin` — string; пример: `dimension-penalty`. ID внутреннего сервиса WB

```json
{
  "title": "access denied",
  "status": 403,
  "detail": "abac: access denied",
  "requestId": "31db50b5-14c0-4f4e-965e-6e1f9607ee78",
  "origin": "dimension-penalty"
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
