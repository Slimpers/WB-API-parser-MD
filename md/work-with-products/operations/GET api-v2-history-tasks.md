# GET /api/v2/history/tasks

**Состояние обработанной загрузки{{ /api/v2/history/tasks }}**

теги: `Цены и скидки`

**Полный путь:** `GET /api/v2/history/tasks`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию об обработанной загрузке цен и скидок.

<div class="description_important">
  Обработанная загрузка — это загрузка цен и скидок для <a href="./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task/post">товаров</a>, цен для <a href="./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task~1size/post">размеров товаров</a> и скидок <a href="./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task~1club-discount/post">WB Клуба</a>.
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Цены и скидки</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Сервисный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — $ref: SupplierTaskMetadata
- `error` — boolean; пример: `False`. Флаг ошибки
- `errorText` — string; пример: ``. Текст ошибки

```json
{
  "data": {
    "uploadID": 395643565,
    "status": 3,
    "uploadDate": "2022-08-21T22:00:13+02:00",
    "activationDate": "2022-08-21T22:00:13+02:00"
  },
  "error": false,
  "errorText": ""
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*InvalidRequestParameters:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Invalid request parameters"
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

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

*AccessDenied:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Access denied"
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
