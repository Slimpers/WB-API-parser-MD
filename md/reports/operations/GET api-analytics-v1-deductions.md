# GET /api/analytics/v1/deductions

**Подмены и неверные вложения{{ /api/analytics/v1/deductions }}**

`operationId`: getDeductions  
теги: `Отчёты об удержаниях`

**Полный путь:** `GET /api/analytics/v1/deductions`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает отчёт об удержаниях за [подмены и неверные вложения](https://seller.wildberries.ru/analytics-reports/dimensions-penalties/retentions)

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Сервисный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | нет | Начало отчётного периода. По умолчанию используются дата и время, когда были впервые получены данные для отчёта |
| `dateTo` | query | string (date-time) | да | Конец отчётного периода |
| `sort` | query | string; enum: ["nmId", "dtBonus", "bonusSumm"]; пример: `nmId` | нет | Сортировка: - `nmId` — по артикулу WB - `dtBonus` — по дате и времени удержания - `bonusSumm` — по сумме удержания |
| `order` | query | string; enum: ["desc", "asc"]; пример: `asc` | нет | Порядок выдачи: - `desc` — по убыванию - `asc` — по возрастанию |
| `limit` | query | integer; пример: `330` | да | Количество удержаний в ответе |
| `offset` | query | integer; пример: `220` | нет | Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` **(required)** — object. Данные ответа
  - `reports` **(required)** — array<object>. Удержания
    - *(элементы)*
      - `dtBonus` — string (date-time); пример: `2025-06-02T00:00:00Z`. Дата и время удержания
      - `nmId` — integer; пример: `544454`. Артикул WB
      - `oldShkId` — integer; пример: `26624352356`. Старый штрихкод
      - `oldColor` — string; пример: `темно-синий,голубой`. Старый цвет
      - `oldSize` — string; пример: `A`. Старый размер
      - `oldSku` — string; пример: `54532562`. Старый баркод
      - `oldVendorCode` — string; пример: `23535 Стемпинг 500`. Старый артикул продавца
      - `newShkId` — integer; пример: `123333223`. Новый штрихкод
      - `newColor` — string; пример: `темно-синий,голубой`. Новый цвет
      - `newSize` — string; пример: `A`. Новый размер
      - `newSku` — string; пример: `12323332223`. Новый баркод
      - `newVendorCode` — string; пример: `wh-service-podmena`. Новый артикул продавца
      - `bonusSumm` — number; пример: `247.5`. Сумма удержания
      - `bonusType` — string; пример: `Подмена FBW`. Причина удержания
      - `photoUrls` — array<string>. Фото замеров
  - `total` **(required)** — integer; пример: `11`. Количество удержаний в отчёте. Без учёта `limit` и `offset`

```json
{
  "data": {
    "reports": [
      {
        "dtBonus": "2025-06-02T00:00:00Z",
        "nmId": 544454,
        "oldShkId": 26624352356,
        "oldColor": "темно-синий,голубой",
        "oldSize": "A",
        "oldSku": "54532562",
        "oldVendorCode": "23535 Стемпинг 500",
        "newShkId": 123333223,
        "newColor": "темно-синий,голубой",
        "newSize": "A",
        "newSku": "12323332223",
        "newVendorCode": "wh-service-podmena",
        "bonusSumm": 247.5,
        "bonusType": "Подмена FBW",
        "photoUrls": [
          "https://static-basket-03.wb.ru/vol49/change_characteristics/19189882946-2023-12-15T10:18:21.125Z-1.webp",
          "https://static-basket-03.wb.ru/vol49/change_characteristics/19189052946-2023-12-15T10:18:35.249Z-2.webp"
        ]
      }
    ],
    "total": 11
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
