# GET /api/v1/documents/list

**Список документов{{ /api/v1/documents/list }}**

теги: `Документы`

**Полный путь:** `GET /api/v1/documents/list`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список документов продавца. Вы можете получить [один](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1download/get) или [несколько](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1download~1all/post) документов из полученного списка.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 1 запрос | 10 сек | 5 запросов |
| Сервисный | 10 сек | 1 запрос | 10 сек | 5 запросов |
| Базовый | 24 ч | 1 запрос | 24 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `beginTime` | query | string (date); пример: `2024-07-09` | нет | Начало периода. Только вместе с `endTime` |
| `endTime` | query | string (date); пример: `2024-07-15` | нет | Конец периода. Только вместе с `beginTime` |
| `sort` | query | string; enum: ["date", "category"]; пример: `category` | нет | Сортировка:   - `date` — по дате создания документа   - `category` — по категории (только при `locale=ru`)  Только вместе с `order` |
| `order` | query | string; enum: ["desc", "asc"]; пример: `asc` | нет | Сортировка:   - `desc` — по убыванию   - `asc` — по возрастанию  Только вместе с `sort` |
| `category` | query | string; пример: `redeem-notification` | нет | ID [категории документов](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1categories/get) из поля `name` |
| `serviceName` | query | string; пример: `redeem-notification-44841941` | нет | Уникальный ID документа |
| `limit` | query | integer; пример: `10` | нет | Максимальное количество строк ответа |
| `offset` | query | integer; пример: `90` | нет | После какой строки выдавать данные |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `documents` — array<object>. Категории документов
    - *(элементы)*
      - `serviceName` — string; пример: `redeem-notification-44841941`. Уникальный ID документа
      - `name` — string; пример: `redeem-notification`. Название документа
      - `category` — string; пример: `Уведомление о выкупе`. Название [категории документов](./financial-reports-and-accounting#tag/Dokumenty/paths/~1api~1v1~1documents~1categories/get) из поля ответа `title`
      - `extensions` — array<string; пример: `zip`>. Форматы документа
      - `creationTime` — string; пример: `2023-10-03T00:18:06.879Z`. Дата и время создания документа
      - `viewed` — boolean; пример: `False`. Выгружен ли документ в личном кабинете

```json
{
  "data": {
    "documents": [
      {
        "serviceName": "redeem-notification-44841941",
        "name": "redeem-notification",
        "category": "Уведомление о выкупе",
        "extensions": [
          "zip"
        ],
        "creationTime": "2023-10-03T00:18:06.879Z",
        "viewed": false
      }
    ]
  }
}
```

#### 400

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `status` — number. HTTP статус-код
- `detail` — string. Детализация ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB

*BadSort&Orders:*

```json
{
  "title": "Bad Request",
  "status": 400,
  "detail": "sort and order must be both set or both not set",
  "requestId": "41fc3b08-051d-4871-9991-6502977912ad",
  "origin": "docs-public-api"
}
```

*BadLimit:*

```json
{
  "title": "Bad Request",
  "status": 400,
  "detail": "limit must be less than or equal to 50",
  "requestId": "46ce9c17-4b74-46ed-abb1-e40d2b0d52ce",
  "origin": "docs-public-api"
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
