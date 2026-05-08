# POST /api/marketplace/v3/dbw/orders/meta/delete

**Удалить метаданные сборочных заданий{{ /api/marketplace/v3/dbw/orders/meta/delete }}**

теги: `Метаданные DBW`

**Полный путь:** `POST /api/marketplace/v3/dbw/orders/meta/delete`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод удаляет значение указанных [метаданных сборочного задания](/openapi/orders-dbw#tag/Metadannye-DBW/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1details/post) для переданного ключа.
<br><br>
В одном запросе можно удалить метаданные только одного типа. Укажите тип метаданных в запросе:
  - `imei` — [IMEI](/openapi/orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1imei/put)
  - `uin` — [УИН](/openapi/orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1uin/put)
  - `gtin` — [GTIN](/openapi/orders-dbw#tag/Metadannye-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta~1imei/put)
  - `sgtin` — [код маркировки](/openapi/orders-dbw#tag/Metadannye-DBW/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1sgtin/post)

Можно передать только один ключ.

  <div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для следующих методов DBW:
<ul>
    <li>получение и обновление списка контактов</li>
    <li>получение и удаление метаданных</li>
    <li>методы сборочных заданий</li>
</ul> 

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `key` — string; пример: `sgtin`. Название метаданных для удаления (imei, uin, gtin, sgtin). Передаётся только одно значение
- `ordersIds` — array<integer>. Список ID сборочных заданий

**Пример:**

```json
{
  "key": "sgtin",
  "ordersIds": [
    123456789
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `requestId` — string. Уникальный ID запроса. Отображается для ответов с ошибками
- `results` **(required)** — array<object>
  - *(элементы)*
    - `errors` — array<object>. Детали ошибки
      - *(элементы)*
        - `code` **(required)** — integer. Код ошибки:
        - `detail` **(required)** — string. - `NotFound` — сборочное задание не найдено
    - `isError` **(required)** — boolean. Есть ли ошибки
    - `orderId` **(required)** — integer. ID сборочного задания с успешно обновлёнными данными

```json
{
  "requestId": "03615778-eb9e-4f55-b4Of-fd3ac0fad2сc",
  "results": [
    {
      "orderId": 42131238,
      "isError": true,
      "errors": [
        {
          "code": 409,
          "detail": "FailedToUpdateMeta"
        }
      ]
    },
    {
      "orderId": 4279781545,
      "isError": false
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": ""
}
```

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": ""
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": ""
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
