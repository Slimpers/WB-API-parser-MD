# PATCH /api/v3/supplies/{supplyId}/deliver

**Передать поставку в доставку{{ /api/v3/supplies/{supplyId}/deliver }}**

теги: `Поставки FBS`

**Полный путь:** `PATCH /api/v3/supplies/{supplyId}/deliver`

## Описание

<span>Описание метода</span>

Метод закрывает [поставку](/openapi/orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D/get) и переводит все [сборочные задания](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) в ней в [статус](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1status/post) `complete` — в доставке. После закрытия поставки добавить новые сборочные задания к ней нельзя.

Если поставка не была передана в доставку, то при приёмке первого товара поставка автоматически закроется.

Передать поставку в доставку можно только если в ней:
  - есть хотя бы одно сборочное задание
  - для всех сборочных заданий указана обязательная маркировка
  - маркировка всех сборочных заданий прошла валидацию

Если поставка содержит сборочные задания с обязательным УИН, убедитесь, что вы заранее создали и загрузили спецификацию с договором на поставку. [ГИИС ДМДК](https://minfin.gov.ru/ru/perfomance/jewels/dmdk) требуется около 30 минут для обработки изменений в статусах УИН.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Ответы


#### 204 — Передано в доставку


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
  "message": "Передан некорректный параметр"
}
```

#### 401

**Content-Type:** `application/json`

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

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": "Доступ запрещён"
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
  "message": "Не найдено"
}
```

#### 409 — Ошибка закрытия поставки

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - `orders` — array<object>. Сборочные задания, метаданные которых не прошли или ещё не завершили валидацию
    - *(элементы)*
      - `id` — integer. ID сборочного задания
      - `metaDetails` — array<object>. Информация об ошибках

*SupplyHasZeroOrders:*

```json
{
  "code": "SupplyHasZeroOrders",
  "message": "Не удалось обработать поставку. Убедитесь, что за ней закреплён хотя бы одно сборочное задание."
}
```

*MetaValidationFail:*

```json
{
  "code": "MetaValidationFail",
  "message": "Fix them to dispatch items",
  "data": {
    "orders": [
      {
        "id": 123456789,
        "metaDetails": [
          {
            "key": "uin",
            "value": "null",
            "decision": "uinBadStatus"
          }
        ]
      }
    ]
  }
}
```

#### 429

**Content-Type:** `application/json`

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
