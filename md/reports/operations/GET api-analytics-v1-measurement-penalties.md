# GET /api/analytics/v1/measurement-penalties

**Удержания за занижение габаритов упаковки{{ /api/analytics/v1/measurement-penalties }}**

`operationId`: getMeasurementPenalties  
теги: `Отчёты об удержаниях`

**Полный путь:** `GET /api/analytics/v1/measurement-penalties`

## Описание

<span>Описание метода</span>

Метод возвращает отчёт об [удержаниях за занижение габаритов упаковки](https://seller.wildberries.ru/analytics-reports/dimensions-penalties)

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Сервисный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Базовый | 6 ч | 1 запрос | 6 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | нет | Начало отчётного периода. По умолчанию используется дата, когда были впервые получены данные для отчёта |
| `dateTo` | query | string (date-time) | да | Конец отчётного периода |
| `limit` | query | integer; пример: `330` | да | Количество удержаний в ответе |
| `offset` | query | integer; пример: `220` | нет | Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — object. Данные ответа
  - `reports` **(required)** — array<object>. Удержания
    - *(элементы)*
      - `nmId` — integer; пример: `123456789`. Артикул WB
      - `subjectName` — string; пример: `Костюмы спортивные`. Предмет
      - `dimId` — integer; пример: `123456789`. ID замера
      - `prcOver` — number; пример: `130.71`. Разница в габаритах, %
      - `volume` — number; пример: `6.47`. Объём, л (фактические габариты по замеру на складе)
      - `width` — integer; пример: `7`. Ширина, см (фактические габариты по замеру на складе)
      - `length` — integer; пример: `28`. Длина, см (фактические габариты по замеру на складе)
      - `height` — integer; пример: `33`. Высота, см (фактические габариты по замеру на складе)
      - `volumeSup` — number; пример: `4.95`. Объём, л (габариты карточки товара)
      - `widthSup` — integer; пример: `8`. Ширина, см (габариты карточки товара)
      - `lengthSup` — integer; пример: `33`. Длина, см (габариты карточки товара)
      - `heightSup` — integer; пример: `33`. Высота, см (габариты карточки товара)
      - `photoUrls` — array<string>. Фото замеров
      - `dtBonus` — string (date-time); пример: `2025-06-02T00:00:00Z`. Дата штрафа
      - `isValid` — boolean; пример: `True`. Статус обмера:
      - `isValidDt` — string (date-time); пример: `2025-05-29T13:35:57Z`. Дата и время подтверждения или отмены обмера
      - `reversalAmount` — number; пример: `0`. Сумма сторно
      - `penaltyAmount` — number; пример: `449.83`. Сумма штрафа
  - `total` **(required)** — integer; пример: `11`. Количество удержаний в отчёте. Без учёта `limit` и `offset`

*MeasurementPenalties:*

```json
{
  "data": {
    "reports": [
      {
        "nmId": 9234567890,
        "subjectName": "Костюмы спортивные",
        "dimId": 98151405,
        "prcOver": 130.71,
        "volume": 6.47,
        "width": 7,
        "length": 28,
        "height": 33,
        "volumeSup": 4.95,
        "widthSup": 30,
        "lengthSup": 33,
        "heightSup": 5,
        "photoUrls": [
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/measurement_on_table/wbs35154094220_em907759_n1_b2eaa5ed-bf21-4c58-b419-b5b5ec6f29ee.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/measurement_on_table/wbs35159094420_em907759_n2_040407b0-7752-4ae7-a4a4-7ec016e86511.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/measurement_on_table/wbs35189094220_em904757_n3_9f502e24-3b3e-4efd-9hac-802813046ac3.webp"
        ],
        "dtBonus": "2025-06-02T00:00:00Z",
        "isValid": true,
        "isValidDt": "2025-05-29T13:35:57Z",
        "reversalAmount": 0,
        "penaltyAmount": 449.83
      },
      {
        "nmId": 9123456789,
        "subjectName": "Масло топленое",
        "dimId": 97079587,
        "prcOver": 136.09,
        "volume": 4.37,
        "width": 14,
        "length": 24,
        "height": 13,
        "volumeSup": 3.21,
        "widthSup": 13,
        "lengthSup": 13,
        "heightSup": 19,
        "photoUrls": [
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35619967012_em1178949_nphotoA_d037721f-62c2-4bdd-a5a8-4ad0905e3f8e.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35619967012_em1178949_nphotoB_fb161a65-e4b0-08d7-bb01-1bdba1b4d741.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35619967012_em1178949_nphotoC_9a8b10f7-26c4-4fc0-b2c5-a7e29a545aa4.webp"
        ],
        "dtBonus": "2025-06-02T00:00:00Z",
        "isValid": true,
        "isValidDt": "2025-05-23T01:24:19Z",
        "reversalAmount": 0,
        "penaltyAmount": 350.08
      },
      {
        "nmId": 9234567809,
        "subjectName": "Фонарики бытовые",
        "dimId": 96989876,
        "prcOver": 246.75,
        "volume": 2.28,
        "width": 12,
        "length": 19,
        "height": 10,
        "volumeSup": 0.92,
        "widthSup": 11,
        "lengthSup": 14,
        "heightSup": 6,
        "photoUrls": [
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35776508795_em644504_nphotoA_1bdac868-a6c0-435a-950f-489f74acdb2e.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35776508795_em644504_nphotoB_8f1802b8-5552-4aae-b930-19e8efbee597.webp",
          "https://static-basket-09.wbbasket.ru/vol184/obmer-tovarov/handheld-goods-measurements-photo/gId35776508795_em644504_nphotoC_5d8f1832-e219-46cd-931b-d6d238d6784b.webp"
        ],
        "dtBonus": "2025-06-02T00:00:00Z",
        "isValid": true,
        "isValidDt": "2025-05-23T01:24:19Z",
        "reversalAmount": 0,
        "penaltyAmount": 501.6
      }
    ],
    "total": 3
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
