# GET /api/v1/seller/events

**События чатов{{ /api/v1/seller/events }}**

теги: `Чат с покупателями`

**Полный путь:** `GET /api/v1/seller/events`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список событий всех [чатов с покупателями](./user-communication#tag/Chat-s-pokupatelyami/paths/~1api~1v1~1seller~1chats/get).

Чтобы получить все события:
  1. Сделайте первый запрос без параметра `next`.
  2. Повторяйте запрос со значением параметра `next` из ответа на предыдущий запрос, пока `totalEvents` не станет равным `0`. Это будет означать, что вы получили все события.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Сервисный | 10 сек | 10 запросов | 1 сек | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `next` | query | integer | нет | Пагинатор. С какого момента получить следующий пакет данных.<br>Формат Unix timestamp **с миллисекундами** |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `result` — $ref: EventsResult
- `errors` — array<string>. Ошибки, если есть

```json
{
  "result": {
    "next": 1698045576000,
    "newestEventTime": "2023-10-23T07:19:36Z",
    "oldestEventTime": "2023-10-23T05:02:20Z",
    "totalEvents": 4,
    "events": [
      {
        "chatID": "1:1e265a58-a120-b178-008c-60af2460207c",
        "eventID": "55adee45-11f0-33b6-a847-6ccc7c78b2ec",
        "eventType": "message",
        "isNewChat": true,
        "message": {
          "attachments": {
            "goodCard": {
              "date": "2023-10-18T11:46:01.528526Z",
              "nmID": 12345678,
              "price": 500,
              "priceCurrency": "RUB",
              "rid": "2fb52cd9e25e52538a5f05994e688ae5",
              "size": "0"
            },
            "files": [
              {
                "contentType": "application/pdf",
                "date": "2023-10-23T08:02:19.594Z",
                "downloadID": "ecaeb056-a4ee-45b4-ae45-666811755d38",
                "name": "Чек.pdf",
                "url": "https://chat-basket-01.wbbasket.ru/vol0/part3265/fb25c9e9-cae8-52db-b68e-736c1896a3f5/pdf/0380e781-281e-41b5-8ae1-ce281f15a4a7.pdf",
                "size": 1046143
              }
            ],
            "images": [
              {
                "date": "2023-10-23T08:02:20.717Z",
                "downloadID": "fd6be4e3-5447-41d7-a1e6-b2d3e06c3b05",
                "url": "https://chat-basket-01.wbbasket.ru/vol0/part2345/fb89c9e9-cae8-52db-b68e-736c1466a3f5/jpg/0823ff24-821e-40e9-8cdf-0a2b5fd86a32.jpg"
              }
            ]
          },
          "text": "Здравствуйте! У меня вопрос по товару \"Альбом, бренд Эконом, артикул 13480414, товар получен 18.10.2023\""
        },
        "source": "rusite",
        "addTimestamp": 1698037340000,
        "addTime": "2023-10-23T05:02:20Z",
        "replySign": "1:1e265a58-a120-b178-008c-60af2460207c:66f136e919a8207e136757754f253189bfb9ae1ad9da9170c9d5c478626663908888c370216525bef51c0ca8d77952e05c9c17f9b63ab00374c5555b42efc07d",
        "sender": "client",
        "clientName": "Алёна"
      },
      {
        "chatID": "1:1e265a58-a120-b178-008c-60af2460207c",
        "eventID": "cef95d3c-0345-4dc9-b6df-4c8c57a176a9",
        "eventType": "message",
        "message": {
          "text": "Здравствуйте! Пришёл не тот цвет. Можно вернуть и заказать другой товар?"
        },
        "source": "rusite",
        "addTimestamp": 1698037387000,
        "addTime": "2023-10-23T05:03:07Z",
        "sender": "client",
        "clientName": "Алёна"
      },
      {
        "chatID": "1:1e265a58-a120-b178-008c-60af2460207c",
        "eventID": "fd22e5bf-64fd-43f7-b3a0-ad29uu027f97",
        "eventType": "message",
        "message": {
          "text": "Здравствуйте. Да, сейчас оформим возврат."
        },
        "source": "seller-public-api",
        "addTimestamp": 1698038124000,
        "addTime": "2023-10-23T05:15:24Z",
        "sender": "seller"
      },
      {
        "chatID": "1:1e265a58-a120-b178-008c-60af2460207c",
        "eventID": "cef95d3c-0345-4dc9-b6df-4c8c75a176a7",
        "eventType": "message",
        "addTimestamp": 1698045576000,
        "addTime": "2023-10-23T07:19:36Z",
        "sender": "seller"
      }
    ]
  },
  "errors": null
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `status` — number. HTTP статус-код
- `title` — string. Заголовок ошибки
- `origin` — string. ID внутреннего сервиса WB
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `error` — string. Текст ошибки

*IncorrectNextParameter:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "Invalid number",
  "requestId": "62f59a4ce21064f20b1bbc28c85f38d8",
  "error": "Invalid number"
}
```

*IncorrectNextParameter1:*

```json
{
  "status": 400,
  "title": "Bad Request",
  "origin": "proxy-chats",
  "detail": "Invalid value for \"next\"",
  "requestId": "62f59a4ce21064f20b1bbc28c85f38d8",
  "error": "Invalid value for \"next\""
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
