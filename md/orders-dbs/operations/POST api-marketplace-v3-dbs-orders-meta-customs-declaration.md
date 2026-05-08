# POST /api/marketplace/v3/dbs/orders/meta/customs-declaration

**Закрепить за сборочными заданиями номер ГТД{{ /api/marketplace/v3/dbs/orders/meta/customs-declaration }}**

теги: `Метаданные DBS`

**Полный путь:** `POST /api/marketplace/v3/dbs/orders/meta/customs-declaration`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод обновляет номер ГТД — грузовой таможенной декларации — в [метаданных сборочных заданий](./orders-dbs#tag/Metadannye-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1meta~1details/post).
<br><br>
У одного сборочного задания может быть только один ГТД.

Добавлять номер ГТД можно только для сборочных заданий, которые находятся в [статусе](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1v3~1dbs~1orders~1status/post) `deliver`.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов <strong>закрепления метаданных DBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 500 запросов | 120 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` — array<object>
  - *(элементы)*
    - `customsDeclaration` **(required)** — string; пример: `10704010/010624/0000302`. Номер ГТД
    - `orderId` **(required)** — integer. ID сборочного задания

**Пример:**

```json
{
  "orders": [
    {
      "customsDeclaration": "10704010/010624/0000302"
    }
  ]
}
```

## Ответы


#### 204 — Обновлено


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": "Некорректное тело запроса"
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": "Переданы некорректные данные"
}
```

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "Передан некорректный параметр"
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

#### 403

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": ""
}
```

#### 404

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "NotFound",
  "message": ""
}
```

#### 409 — Ошибка добавления маркировки

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*FailedToUpdateMeta:*

```json
{
  "code": "FailedToUpdateMeta",
  "message": "Не удалось обновить метаданные сборочного задания. Убедитесь, что сборочное задание удовлетворяет всем необходимым требованиям (сборочное задание существует, находится в статусе \"На сборке\", сборочному заданию доступны метаданные см. описание метода **Получить метаданные сборочного задания**)"
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
