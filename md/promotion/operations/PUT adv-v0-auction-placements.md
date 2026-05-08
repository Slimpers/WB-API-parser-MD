# PUT /adv/v0/auction/placements

**Изменение мест размещения в кампаниях с ручной ставкой{{ /adv/v0/auction/placements }}**

теги: `Управление кампаниями`

**Полный путь:** `PUT /adv/v0/auction/placements`

## Описание

<span>Описание метода</span>

Метод меняет места размещения в кампаниях с ручной ставкой и моделью оплаты за показы — `cpm`.

Для кампаний в статусах `4`, `9` и `11`.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 1 запрос |
| Сервисный | 1 сек | 1 запрос | 1 сек | 1 запрос |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `placements` **(required)** — array<object>. Места размещения в кампаниях
  - *(элементы)*
    - `advert_id` **(required)** — integer (int64). ID кампании
    - `placements` **(required)** — object. Места размещения
      - `search` **(required)** — boolean. Размещение в поиске:
      - `recommendations` **(required)** — boolean. Размещение в рекомендациях:

**Пример:**

```json
{
  "placements": [
    {
      "advert_id": 12345,
      "placements": {
        "search": true,
        "recommendations": true
      }
    }
  ]
}
```

## Ответы


#### 204 — Успешно


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `6023d2950af564838f9b44a279d2140c`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `invalid payload`. Заголовок ошибки

*BadRequest:*

```json
{
  "detail": "can not deserialize response body",
  "origin": "camp-api-public-cache",
  "request_id": "9a929a81ea9dc1601fcc4be81f32c1cb",
  "status": 400,
  "title": "invalid payload"
}
```

*BadAdvertPaymentType:*

```json
{
  "detail": "advert 12345 has payment type cpc, placements cannot be changed",
  "origin": "camp-api-public-cache",
  "request_id": "e53addfabe9274d5b8f77272ca085ac4",
  "status": 400,
  "title": "invalid payload"
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
