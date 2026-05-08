# POST /api/v3/orders/stickers/cross-border

**Получить стикеры сборочных заданий трансграничных поставок{{ /api/v3/orders/stickers/cross-border }}**

теги: `Сборочные задания FBS`

**Полный путь:** `POST /api/v3/orders/stickers/cross-border`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список стикеров [сборочных заданий](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) трансграничных поставок в формате PDF.<br><br>

Для каждого сборочного задания в ответе указывается статус генерации стикера:
  - `awaitingTrackNumber` — стикер не готов. Ожидается трек-номер от перевозчика.
  - `ready` — стикер готов

<div class="description_important">
  Стикер может генерироваться с задержкой. Повторяйте запрос, пока не получите статус <code>ready</code>.
</div>

Ограничения:
  - За один запрос можно получить максимум 100 стикеров.
  - Можно получить стикеры только для сборочных заданий, находящихся на сборке или в доставке — [статусы](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1status/post) `confirm`, `complete`.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` — array<integer (int64); пример: `3869227998`>. Список ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    3869227998
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `stickers` — array<object>
  - *(элементы)*
    - `orderId` — integer; пример: `3869227998`. ID сборочного задания
    - `status` — string; enum: ["awaitingTrackNumber", "ready"]; пример: `ready`. Статус генерации стикера:
    - `parcelId` — string; пример: `WB0000000001`. Трек-номер в стикере для отслеживания сборочного задания
    - `file` — string (byte); пример: `JVBERi0xLjQKJSBjcmVhdGVkIGJ5IFBpbGxvdyBQREYgZHJpdmVyCjQgMCBvYmo8PAovVHlwZSAvQ2F0YWxvZwovUGFnZXMgNSAwIFIKPj5lbmRvYmoKNSAwIG9iajw8Ci9UeXBlIC9QYWdlcwovQ291bnQgMQovS2lkcyBbIDIgMCBSIF0KPj5lbmRvYmoKMSAwIG9iajw8Ci9UeXBlIC9YT2JqZWN0Ci9TdWJ0eXBlIC9JbWFnZQovV2lkdGggMjkwCi9IZWlnaHQgMjkwCi9GaWx0ZXIgWyAvQ0NJVFRGYXhEZWNvZGUgXQovRGVjb2RlUGFybXMgWyA8PAovSyAtMQovQmxhY2tJczEgdHJ1ZQovQ29sdW1ucyAyOTAKL1Jvd3MgMjkwCj4+IF0KL0JpdHNQZXJDb21wb25lbnQgMQovQ29sb3JTcGFjZSAvRGV2aWNlR3JheQovTGVuZ3RoIDY2Ngo+PnN0cmVhbQomoLYaX////////////8g2b4gpHITff///////////8nBSkIB8nBS/////////////////////+QgHkNB/IQD////////////////////////////+P//////////////////////////IQ5CHIQ////////////////////////////////jkNB/H/////////////////////4yEOQh+P//////////////////EhoKR//////yDYchDkIchDyBg2E4aCcFL////////////////////////IgFIiAhODQTg0f/////////////////+ThCICEQGgnDQTg0E4NBODZ////////////////////////4k4NESEOJCCP/////////////////8gpHIQ5CCCEEENB8hDyBg2f//////////////////////////xEZKQhOEJwhOB5f//////////////yDZviDQIjkDBS///////////////ycFLEnCCThP//////////////////kIB5CHkQEEnCEQEJwbP///////////////////////////4ycGgnBoIgFL/////////////////////+QhxIQ4kIcg0H////////////////////////8cSEOJCHEhAP//////////////////jIQDIQ+Qh5OE////////////////////////4iIiI/////////////wAQAQJAAABAwABAAAAIgEAAAEBAwABAAAAIgEAAAIBAwABAAAAAQAAAAMBAwABAAAABAAAAAYBAwABAAAAAQAAABEBBAABAAAACAAAABYBAwABAAAAIgEAABcBBAABAAAAKAIAABwBAwABAAAAAQAAAAAAAAAKZW5kc3RyZWFtCmVuZG9iagoyIDAgb2JqPDwKL1Jlc291cmNlcyA8PAovUHJvY1NldCBbIC9QREYgL0ltYWdlQiBdCi9YT2JqZWN0IDw8Ci9pbWFnZSAxIDAgUgo+Pgo+PgovTWVkaWFCb3ggWyAwIDAgMjkwLjAgMjkwLjAgXQovQ29udGVudHMgMyAwIFIKL1R5cGUgL1BhZ2UKL1BhcmVudCA1IDAgUgo+PmVuZG9iagozIDAgb2JqPDwKL0xlbmd0aCA0Nwo+PnN0cmVhbQpxIDI5MC4wMDAwMDAgMCAwIDI5MC4wMDAwMDAgMCAwIGNtIC9pbWFnZSBEbyBRCgplbmRzdHJlYW0KZW5kb2JqCjYgMCBvYmo8PAovQ3JlYXRpb25EYXRlIChEOjIwMjUxMTA3MTMzNTE1WikKL01vZERhdGUgKEQ6MjAyNTExMDcxMzM1MTVaKQo+PmVuZG9iagp4cmVmCjAgNwowMDAwMDAwMDAwIDY1NTM2IGYgCjAwMDAwMDAxNDQgMDAwMDAgbiAKMDAwMDAwMTA1MiAwMDAwMCBuIAowMDAwMDAxMjE0IDAwMDAwIG4gCjAwMDAwMDAwNDAgMDAwMDAgbiAKMDAwMDAwMDA4NyAwMDAwMCBuIAowMDAwMDAxMzA5IDAwMDAwIG4gCnRyYWlsZXIKPDwKL1Jvb3QgNCAwIFIKL1NpemUgNwovSW5mbyA2IDAgUgo+PgpzdGFydHhyZWYKMTM5MQolJUVPRg==`. Стикер в формате PDF, кодировка base64
    - `partA` — string; пример: `231648`. Первая часть ID стикера для печати подписи
    - `partB` — string; пример: `9753`. Вторая часть ID стикера для печати подписи
    - `barcode` — string; пример: `!uKEtQZVx`. Закодированное значение стикера

```json
{
  "stickers": [
    {
      "orderId": 987654320,
      "status": "awaitingTrackNumber",
      "parcelId": "",
      "file": "",
      "partA": "",
      "partB": "",
      "barcode": ""
    },
    {
      "orderId": 123456789,
      "status": "ready",
      "parcelId": "WB0000000001",
      "file": "JVBERi0xLjQKJSBjcmVhdGVkIGJ5IFBpbGxvdyBQREYgZHJpdmVyCjQgMCBvYmo8PAovVHlwZSAvQ2F0YWxvZwovUGFnZXMgNSAwIFIKPj5lbmRvYmoKNSAwIG9iajw8Ci9UeXBlIC9QYWdlcwovQ291bnQgMQovS2lkcyBbIDIgMCBSIF0KPj5lbmRvYmoKMSAwIG9iajw8Ci9UeXBlIC9YT2JqZWN0Ci9TdWJ0eXBlIC9JbWFnZQovV2lkdGggMjkwCi9IZWlnaHQgMjkwCi9GaWx0ZXIgWyAvQ0NJVFRGYXhEZWNvZGUgXQovRGVjb2RlUGFybXMgWyA8PAovSyAtMQovQmxhY2tJczEgdHJ1ZQovQ29sdW1ucyAyOTAKL1Jvd3MgMjkwCj4+IF0KL0JpdHNQZXJDb21wb25lbnQgMQovQ29sb3JTcGFjZSAvRGV2aWNlR3JheQovTGVuZ3RoIDY2Ngo+PnN0cmVhbQomoLYaX////////////8g2b4gpHITff///////////8nBSkIB8nBS/////////////////////+QgHkNB/IQD////////////////////////////+P//////////////////////////IQ5CHIQ////////////////////////////////jkNB/H/////////////////////4yEOQh+P//////////////////EhoKR//////yDYchDkIchDyBg2E4aCcFL////////////////////////IgFIiAhODQTg0f/////////////////+ThCICEQGgnDQTg0E4NBODZ////////////////////////4k4NESEOJCCP/////////////////8gpHIQ5CCCEEENB8hDyBg2f//////////////////////////xEZKQhOEJwhOB5f//////////////yDZviDQIjkDBS///////////////ycFLEnCCThP//////////////////kIB5CHkQEEnCEQEJwbP///////////////////////////4ycGgnBoIgFL/////////////////////+QhxIQ4kIcg0H////////////////////////8cSEOJCHEhAP//////////////////jIQDIQ+Qh5OE////////////////////////4iIiI/////////////wAQAQJAAABAwABAAAAIgEAAAEBAwABAAAAIgEAAAIBAwABAAAAAQAAAAMBAwABAAAABAAAAAYBAwABAAAAAQAAABEBBAABAAAACAAAABYBAwABAAAAIgEAABcBBAABAAAAKAIAABwBAwABAAAAAQAAAAAAAAAKZW5kc3RyZWFtCmVuZG9iagoyIDAgb2JqPDwKL1Jlc291cmNlcyA8PAovUHJvY1NldCBbIC9QREYgL0ltYWdlQiBdCi9YT2JqZWN0IDw8Ci9pbWFnZSAxIDAgUgo+Pgo+PgovTWVkaWFCb3ggWyAwIDAgMjkwLjAgMjkwLjAgXQovQ29udGVudHMgMyAwIFIKL1R5cGUgL1BhZ2UKL1BhcmVudCA1IDAgUgo+PmVuZG9iagozIDAgb2JqPDwKL0xlbmd0aCA0Nwo+PnN0cmVhbQpxIDI5MC4wMDAwMDAgMCAwIDI5MC4wMDAwMDAgMCAwIGNtIC9pbWFnZSBEbyBRCgplbmRzdHJlYW0KZW5kb2JqCjYgMCBvYmo8PAovQ3JlYXRpb25EYXRlIChEOjIwMjUxMTA3MTMzNTE1WikKL01vZERhdGUgKEQ6MjAyNTExMDcxMzM1MTVaKQo+PmVuZG9iagp4cmVmCjAgNwowMDAwMDAwMDAwIDY1NTM2IGYgCjAwMDAwMDAxNDQgMDAwMDAgbiAKMDAwMDAwMTA1MiAwMDAwMCBuIAowMDAwMDAxMjE0IDAwMDAwIG4gCjAwMDAwMDAwNDAgMDAwMDAgbiAKMDAwMDAwMDA4NyAwMDAwMCBuIAowMDAwMDAxMzA5IDAwMDAwIG4gCnRyYWlsZXIKPDwKL1Jvb3QgNCAwIFIKL1NpemUgNwovSW5mbyA2IDAgUgo+PgpzdGFydHhyZWYKMTM5MQolJUVPRg==",
      "partA": "231648",
      "partB": "9753",
      "barcode": "!uKEtQZVx"
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
