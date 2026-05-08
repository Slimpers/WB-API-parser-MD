# POST /api/analytics/v3/sales-funnel/grouped/history

**Статистика групп карточек товаров по дням{{ /api/analytics/v3/sales-funnel/grouped/history }}**

`operationId`: postSalesFunnelGroupedHistory  
теги: `Воронка продаж`

**Полный путь:** `POST /api/analytics/v3/sales-funnel/grouped/history`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает статистику карточек товаров по дням или неделям.<br>
Карточки товаров сгруппированы по предметам, брендам и ярлыкам.<br>
Можно получить данные максимум за последнюю неделю.<br><br>

Данные отчёта обновляются 1 раз в час.<br><br>

В течение часа после события появляется большая часть данных:
  - о заказах
  - о переходах в карточку товара
  - о добавлениях товаров в корзину

Малая часть этих данных может появляться в течение нескольких дней.<br><br>

Выкупы, отмены и возвраты отображаются в отчёте за тот день, когда товар был заказан. Например, если заказ был сделан 1 января, а покупатель вернул товар 10 января, данные об этом возврате появятся в отчёте за 1 января.<br>
Окончательные итоги продаж вы можете отслеживать с помощью [детализаций к отчётам реализации](./financial-reports-and-accounting#tag/Finansovye-otchyoty/paths/~1api~1v5~1supplier~1reportDetailByPeriod/get).<br><br>

Параметры `brandNames`, `subjectIds`, `tagIds` могут быть пустыми `[]`, тогда группировка происходит по всем карточкам продавца.<br><br>

Произведение количества предметов, брендов, ярлыков в запросе может быть не больше 16. Например, 4 бренда и 4 предмета или 2 предмета, 2 ярлыка и 4 бренда.

<div class="description_important">
  Чтобы получать отчёты за период до года, используйте методы <a href='./analytics#tag/Analitika-prodavca-CSV'>Аналитика продавца CSV</a> — тип <code>GROUPED_HISTORY_REPORT</code>. Отчёты этого типа доступны только с подпиской <a href='https://seller.wildberries.ru/monetization/jam'>Джем</a>
</div>

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

- `selectedPeriod` **(required)**
- `brandNames` — array<string>. Список брендов для фильтрации
- `subjectIds` — array<integer (uint64)>. Список ID предметов для фильтрации
- `tagIds` — array<integer (uint64)>. Список ID ярлыков для фильтрации
- `skipDeletedNm` — boolean; пример: `False`. Скрыть удалённые товары
- `aggregationLevel` — $ref: Level

**Пример:**

```json
{
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
  "aggregationLevel": "day"
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — $ref: GroupedHistoryResponse

```json
{
  "data": [
    {
      "history": [
        {
          "date": "2024-10-23",
          "openCount": 45,
          "cartCount": 34,
          "orderCount": 19,
          "orderSum": 1262,
          "buyoutCount": 19,
          "buyoutSum": 1262,
          "buyoutPercent": 35,
          "addToCartConversion": 43
        }
      ],
      "currency": "RUB"
    }
  ]
}
```

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
