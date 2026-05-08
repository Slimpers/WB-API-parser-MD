# POST /api/v2/nm-report/downloads

**Создать отчёт{{ /api/v2/nm-report/downloads }}**

теги: `Аналитика продавца CSV`

**Полный путь:** `POST /api/v2/nm-report/downloads`

## Описание

<span>Описание метода</span>

Метод создаёт задание на генерацию отчёта с расширенной аналитикой продавца.

Вы можете создать CSV-версии отчётов по [воронке продаж](./analytics#tag/Voronka-prodazh) или [параметрам поиска](./analytics#tag/Poiskovye-zaprosy-po-vashim-tovaram) с группировкой по:
  * артикулам WB
  * предметам, брендам и ярлыкам

В отчётах по воронке продаж можно группировать данные по дням, неделям или месяцам.

Также можете создать CSV-версии отчётов по [текстам поисковых запросов](./analytics#tag/Poiskovye-zaprosy-po-vashim-tovaram/paths/~1api~1v2~1search-report~1product~1search-texts/post) и [остаткам](./analytics#tag/Istoriya-ostatkov).

Каждый новый отчёт должен иметь уникальный ID.

  Не используйте одинаковые ID для разных отчётов — это может привести к ошибкам при генерации

Набор параметров запроса в объекте `params` зависит от типа отчёта. Чтобы получить описание параметров, выберите тип отчёта в раскрывающемся списке в описании параметра `reportType`.

Параметры `includeSubstitutedSKUs` и `includeSearchTexts` не могут одновременно иметь значение `false`.

Если не удалось [получить отчёт](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads~1file~1%7BdownloadId%7D/get), можно создать [повторное задание на генерацию](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads~1retry/post). Также можно [получить список и проверить статусы](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads/get) отчётов.

  Отчёты по <a href="https://seller.wildberries.ru/content-analytics/history-remains">остаткам</a> — типы <code>STOCK_HISTORY_REPORT_CSV</code> и <code>STOCK_HISTORY_DAILY_CSV</code> — можно создать без подписки <a href="https://seller.wildberries.ru/monetization/jam">Джем</a>

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`


**Пример «SalesFunnelProductReq»:**

```json
{
  "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "DETAIL_HISTORY_REPORT",
  "userReportName": "Card report",
  "params": {
    "nmIDs": [
      1234567
    ],
    "subjectIds": [
      1234567
    ],
    "brandNames": [
      "Name"
    ],
    "tagIds": [
      1234567
    ],
    "startDate": "2024-06-21",
    "endDate": "2024-06-23",
    "timezone": "Europe/Moscow",
    "aggregationLevel": "day",
    "skipDeletedNm": false
  }
}
```

**Пример «SalesFunnelGroupReq»:**

```json
{
  "id": "06eea887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "GROUPED_HISTORY_REPORT",
  "userReportName": "Subject report",
  "params": {
    "subjectIds": [
      1234567
    ],
    "brandNames": [
      "Name"
    ],
    "tagIds": [
      1234567
    ],
    "startDate": "2024-06-21",
    "endDate": "2024-06-23",
    "timezone": "Europe/Moscow",
    "aggregationLevel": "day",
    "skipDeletedNm": false
  }
}
```

**Пример «SearchReportGroupReq»:**

```json
{
  "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "SEARCH_QUERIES_PREMIUM_REPORT_GROUP",
  "userReportName": "Subject report",
  "params": {
    "currentPeriod": {
      "start": "2024-02-10",
      "end": "2024-02-10"
    },
    "pastPeriod": {
      "start": "2024-02-08",
      "end": "2024-02-08"
    },
    "nmIds": [
      162579635,
      166699779
    ],
    "subjectIds": [
      64,
      334
    ],
    "brandNames": [
      "nikkle",
      "abikas"
    ],
    "tagIds": [
      32,
      53
    ],
    "orderBy": {
      "field": "avgPosition",
      "mode": "asc"
    },
    "positionCluster": "all",
    "includeSubstitutedSKUs": true,
    "includeSearchTexts": false
  }
}
```

**Пример «SearchReportProductReq»:**

```json
{
  "id": "06eea887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "SEARCH_QUERIES_PREMIUM_REPORT_PRODUCT",
  "userReportName": "Card report",
  "params": {
    "currentPeriod": {
      "start": "2024-02-10",
      "end": "2024-02-10"
    },
    "pastPeriod": {
      "start": "2024-02-08",
      "end": "2024-02-08"
    },
    "subjectId": 123,
    "brandName": "Abble",
    "tagId": 45,
    "nmIds": [
      162579635,
      166699779
    ],
    "orderBy": {
      "field": "buyoutCount",
      "mode": "asc"
    },
    "positionCluster": "all",
    "includeSubstitutedSKUs": false,
    "includeSearchTexts": true
  }
}
```

**Пример «SearchReportTextReq»:**

```json
{
  "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "SEARCH_QUERIES_PREMIUM_REPORT_TEXT",
  "userReportName": "Subject report",
  "params": {
    "currentPeriod": {
      "start": "2024-02-10",
      "end": "2024-02-10"
    },
    "pastPeriod": {
      "start": "2024-02-08",
      "end": "2024-02-08"
    },
    "nmIds": [
      162579635,
      166699779
    ],
    "subjectIds": [
      64,
      334
    ],
    "brandNames": [
      "nikkle",
      "abikas"
    ],
    "tagIds": [
      32,
      53
    ],
    "topOrderBy": "openCard",
    "orderBy": {
      "field": "avgPosition",
      "mode": "asc"
    },
    "includeSubstitutedSKUs": true,
    "includeSearchTexts": true,
    "limit": 50
  }
}
```

**Пример «InventoryMetricsReportReq»:**

```json
{
  "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "STOCK_HISTORY_REPORT_CSV",
  "userReportName": "Inventory report",
  "params": {
    "nmIDs": [
      111222333,
      444555666
    ],
    "subjectIDs": [
      123,
      456
    ],
    "brandNames": [
      "ЭгКа",
      "Stock"
    ],
    "tagIDs": [
      3,
      4,
      5
    ],
    "currentPeriod": {
      "start": "2024-02-10",
      "end": "2024-02-10"
    },
    "stockType": "mp",
    "skipDeletedNm": true,
    "availabilityFilters": [
      "deficient",
      "balanced"
    ],
    "orderBy": {
      "field": "avgOrders",
      "mode": "asc"
    }
  }
}
```

**Пример «InventoryHistoryReportReq»:**

```json
{
  "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
  "reportType": "STOCK_HISTORY_DAILY_CSV",
  "userReportName": "Inventory report",
  "params": {
    "nmIds": [
      111222333,
      444555666
    ],
    "subjectIds": [
      123,
      456
    ],
    "brandNames": [
      "ЭгКа",
      "Stock"
    ],
    "tagIds": [
      3,
      4,
      5
    ],
    "currentPeriod": {
      "start": "2025-12-13",
      "end": "2025-12-15"
    },
    "stockType": "",
    "skipDeletedNm": true
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — string; пример: `Началось формирование файла/отчета`. Уведомление, что началась генерация отчёта

```json
{
  "data": "Началось формирование файла/отчета"
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` **(required)** — string. Заголовок ошибки
- `detail` **(required)** — string. Детали ошибки
- `requestId` **(required)** — string. Уникальный ID запроса
- `origin` **(required)** — string. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Invalid request body",
  "detail": "userReportName can not contain emojis",
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

#### 403 — Доступ запрещён

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Authorization error",
  "detail": "Authorization error",
  "requestId": "51b7828b-e298-4dfa-b7cd-45ab179921d3",
  "origin": "analytics-open-api"
}
```

#### 429 — Слишком много запросов

**Content-Type:** `application/json`

