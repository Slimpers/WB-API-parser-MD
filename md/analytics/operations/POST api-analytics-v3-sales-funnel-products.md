# POST /api/analytics/v3/sales-funnel/products

**Статистика карточек товаров за период{{ /api/analytics/v3/sales-funnel/products }}**

`operationId`: postSalesFunnelProducts  
теги: `Воронка продаж`

**Полный путь:** `POST /api/analytics/v3/sales-funnel/products`

## Описание

<span>Описание метода</span>

Метод формирует отчёт о товарах, сравнивая ключевые показатели за текущий период с аналогичным прошлым.

Данные отчёта обновляются 1 раз в час.

В течение часа после события появляется большая часть данных:
  - о заказах
  - о переходах в карточку товара
  - о добавлениях товаров в корзину

Малая часть этих данных может появляться в течение нескольких дней.

Выкупы, отмены и возвраты отображаются в отчёте за тот день, когда товар был заказан. Например, если заказ был сделан 1 января, а покупатель вернул товар 10 января, данные об этом возврате появятся в отчёте за 1 января.

Окончательные итоги продаж вы можете отслеживать с помощью [детализаций к отчётам реализации](./financial-reports-and-accounting#tag/Finansovye-otchyoty/paths/~1api~1v5~1supplier~1reportDetailByPeriod/get).

Параметры `brandNames`,`subjectIds`, `tagIds`, `nmIds` могут быть пустыми `[]`, тогда в ответе возвращаются все карточки продавца.

Если вы указали несколько параметров, в ответе будут карточки, в которых есть одновременно все эти параметры. Если карточки не подходят по параметрам запроса, вернётся пустой ответ `[]`.

Можно получить отчёт максимум за последние 365 дней.

В данных предыдущего периода:
  * Данные в `pastPeriod` указаны за такой же период, что и в `selectedPeriod`
  * Если дата начала  `pastPeriod` раньше, чем год назад от текущей даты, она будет приведена к виду: `pastPeriod.start = текущая дата — 365 дней`

Можно использовать пагинацию.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `selectedPeriod` **(required)**
- `pastPeriod`
- `nmIds` — array<integer (uint64)>. Артикулы WB, по которым нужно составить отчёт. Оставьте пустым, чтобы получить отчёт обо всех товарах
- `brandNames` — array<string>. Список брендов для фильтрации
- `subjectIds` — array<integer (uint64)>. Список ID предметов для фильтрации
- `tagIds` — array<integer (uint64)>. Список ID ярлыков для фильтрации
- `skipDeletedNm` — boolean; пример: `False`. Скрыть удалённые товары
- `orderBy` — $ref: OrderBy
- `limit` — integer (uint32); пример: `231`. Количество карточек товара в ответе
- `offset` — integer (uint32); пример: `10`. Сколько элементов пропустить. Например, для значения `10` ответ начнётся с 11 элемента

**Пример:**

```json
{
  "nmIds": [
    1234567
  ],
  "brandNames": [
    "nike",
    "adidas"
  ],
  "subjectIds": [
    64,
    334
  ],
  "tagIds": [
    32,
    53
  ],
  "skipDeletedNm": false,
  "orderBy": {
    "field": "openCard",
    "mode": "asc"
  },
  "limit": 231,
  "offset": 10
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)**

#### 400

**Content-Type:** `application/json`

- `title` **(required)** — string; пример: `SKU not found`. Заголовок ошибки
- `detail` **(required)** — string; пример: `SKU xxx doesn't exist`. Детали ошибки
- `requestId` **(required)** — string; пример: `fb25c9e9-cae8-52db-b68e-736c1466a3f5`. Уникальный ID запроса
- `origin` **(required)** — string; пример: `analytic-open-api`. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Invalid request body",
  "detail": "code=400, message=invalid: positionCluster (field required), internal=invalid: positionCluster (field required)",
  "requestId": "51b7828b-e298-4dfa-b7cd-45ab179921d3",
  "origin": "analytics-open-api"
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

#### 403

**Content-Type:** `application/json`

- `title` **(required)** — string; пример: `SKU not found`. Заголовок ошибки
- `detail` **(required)** — string; пример: `SKU xxx doesn't exist`. Детали ошибки
- `requestId` **(required)** — string; пример: `fb25c9e9-cae8-52db-b68e-736c1466a3f5`. Уникальный ID запроса
- `origin` **(required)** — string; пример: `analytic-open-api`. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Authorization error",
  "detail": "Authorization error",
  "requestId": "51b7828b-e298-4dfa-b7cd-45ab179921d3",
  "origin": "analytics-open-api"
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
