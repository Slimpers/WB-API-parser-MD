# POST /adv/v0/normquery/list

**Списки активных и неактивных поисковых кластеров{{ /adv/v0/normquery/list }}**

теги: `Поисковые кластеры`

**Полный путь:** `POST /adv/v0/normquery/list`

## Описание

<span>Описание метода</span>

Метод возвращает списки активных и неактивных поисковых кластеров, по которым было не меньше 100 показов.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 5 запросов | 200 мс | 10 запросов |
| Сервисный | 1 сек | 5 запросов | 200 мс | 10 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `items` **(required)** — array<$ref: V0GetNormQueryListRequestItem>

**Пример:**

```json
{
  "items": [
    {
      "advertId": 123456789,
      "nmId": 987654321
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `items` **(required)** — array<$ref: V0GetNormQueryListResponseItem>

```json
{
  "items": [
    {
      "advertId": 123456789,
      "nmId": 987654321,
      "normQueries": {
        "active": null,
        "excluded": [
          "бест трикотаж",
          "горы футболка для мужчин",
          "одежда для моря",
          "одежда на море",
          "поло мужское",
          "поло мужское летнее",
          "футболка дельфин",
          "футболка мужская с принтом светлая",
          "футболка поло",
          "футболка поло мужская",
          "футболка с воротником мужские"
        ]
      }
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `6023d2950af564838f9b44a279d2140c`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `invalid payload`. Заголовок ошибки

```json
{
  "detail": "incorrect request body, please check API documentation",
  "origin": "camp-api-public-cache",
  "request_id": "33e7d9f3fc221648cdf096bf8e62e482",
  "status": 400,
  "title": "invalid request body"
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
