# POST /api/v2/search-report/product/search-texts

**Поисковые запросы по товару{{ /api/v2/search-report/product/search-texts }}**

теги: `Поисковые запросы по вашим товарам`

**Полный путь:** `POST /api/v2/search-report/product/search-texts`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод формирует топ поисковых запросов по товару.

Параметры выбора поисковых запросов:
 - `limit` — количество запросов, максимум 30. Для тарифов [Джема](https://seller.wildberries.ru/monetization/tariffs) **Продвинутый** и **Премиальный** максимум — 100.
 - `topOrderBy` — способ выбора топа запросов

Параметры `includeSubstitutedSKUs` и `includeSearchTexts` не могут одновременно иметь значение `false`.<br><br>

Данные отчёта обновляются 1 раз в час.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

Параметры для запроса по рейтингу поисковых запросов:
  - `currentPeriod` — текущий период
  - `pastPeriod` — предыдущий период для сравнения
- `currentPeriod` **(required)** — $ref: Period
- `pastPeriod` — $ref: pastPeriod
- `nmIds` **(required)** — array<integer (uint64)>. Список артикулов WB
- `topOrderBy` **(required)** — string; enum: ["openCard", "addToCart", "openToCart", "orders", "cartToOrder"]; пример: `openToCart`. Фильтрация по поисковым запросам, по которым больше всего:
- `includeSubstitutedSKUs` — boolean; пример: `True`. Показать данные по прямым запросам с [подменным артикулом](https://seller.wildberries.ru/help-center/article/A-524)
- `includeSearchTexts` — boolean; пример: `False`. Показать данные по поисковым запросам без учёта подменного артикула
- `orderBy` **(required)** — $ref: OrderByGrTe
- `limit` **(required)** — $ref: TextLimit

**Пример:**

```json
{
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
  "topOrderBy": "openToCart",
  "includeSubstitutedSKUs": true,
  "includeSearchTexts": false,
  "orderBy": {
    "field": "avgPosition",
    "mode": "asc"
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`


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
