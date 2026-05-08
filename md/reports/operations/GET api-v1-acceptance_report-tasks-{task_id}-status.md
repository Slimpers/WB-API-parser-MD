# GET /api/v1/acceptance_report/tasks/{task_id}/status

**Проверить статус{{ /api/v1/acceptance_report/tasks/{task_id}/status }}**

теги: `Операции при приёмке`

**Полный путь:** `GET /api/v1/acceptance_report/tasks/{task_id}/status`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает статус [задания на генерацию](./reports#tag/Operacii-pri-priyomke/paths/~1api~1v1~1acceptance_report/get) отчёта об [операциях при приёмке](./reports#tag/Operacii-pri-priyomke/paths/~1api~1v1~1acceptance_report~1tasks~1%7Btask_id%7D~1download/get).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 5 сек | 1 запрос | 5 сек | 1 запрос |
| Сервисный | 5 сек | 1 запрос | 5 сек | 1 запрос |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `task_id` | path | string; пример: `06e06887-9d9f-491f-b16a-bb1766fcb8d2` | да | ID задания на генерацию |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — $ref: GetTasksResponseData

*GetTasksResponseData:*

```json
{
  "data": {
    "id": "cad56ec5-91ec-43a2-b5e8-efcf244cf309",
    "status": "done"
  }
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/problem+json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "Invalid format for parameter task_id: error unmarshaling '7b8875---9f03-46f1-af21-b9b4b22fe821' text as *uuid.UUID: invalid UUID format",
  "origin": "api-statistics",
  "requestId": "44bac63ab29c46cb2d49392e6604c1a0",
  "title": "Bad Request"
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

#### 404 — Не найдено

**Content-Type:** `application/problem+json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "not found",
  "origin": "api-statistics",
  "requestId": "c777731fc180f215a49c9896c2f1200d",
  "title": "Not Found"
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
