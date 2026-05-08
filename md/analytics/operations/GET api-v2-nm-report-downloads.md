# GET /api/v2/nm-report/downloads

**Получить список отчётов{{ /api/v2/nm-report/downloads }}**

теги: `Аналитика продавца CSV`

**Полный путь:** `GET /api/v2/nm-report/downloads`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список отчётов с расширенной аналитикой продавца. Ответ содержит ID [созданных отчётов](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads/post) и статусы генерации.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `filter[downloadIds]` | query | array<string (uuid)> | нет | ID отчёта |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — array<object>
  - *(элементы)*
    - `id` **(required)** — string (uuid); пример: `06eae887-9d9f-491f-b16a-bb1766fcb8d2`. ID отчёта
    - `createdAt` **(required)** — string; пример: `2024-06-26 20:05:32`. Дата и время завершения генерации
    - `status` **(required)** — string; пример: `SUCCESS`. Статус отчёта:
    - `name` **(required)** — string; пример: `Card report`. Название отчёта
    - `size` **(required)** — integer; пример: `123`. Размер отчёта, Б
    - `startDate` **(required)** — string (date); пример: `2024-06-21`. Начало периода
    - `endDate` **(required)** — string (date); пример: `2024-06-23`. Конец периода

```json
{
  "data": [
    {
      "id": "06eae887-9d9f-491f-b16a-bb1766fcb8d2",
      "createdAt": "2024-06-26 20:05:32",
      "status": "SUCCESS",
      "name": "Card report",
      "size": 123,
      "startDate": "2024-06-21",
      "endDate": "2024-06-23"
    }
  ]
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
  "detail": "download id was not found",
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
