# GET /adv/v1/adverts

**Список медиакампаний{{ /adv/v1/adverts }}**

теги: `Медиа`

**Полный путь:** `GET /adv/v1/adverts`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список всех [медиакампаний](./promotion#tag/Media/paths/~1adv~1v1~1advert/get) продавца по их типам и статусам.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Сервисный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `status` | query | integer; пример: `1` | нет | Статус медиакампании:   - `1` — черновик   - `2` — модерация   - `3` — отклонена (с возможностью вернуть на модерацию)   - `4` — готова к запуску   - `5` — запланирована   - `6` — на показах   - `7` — завершена   - `8` — отменена   - `9` — приостановлена продавцом   - `10` — пауза по дневному лимиту   - `11` — пауза |
| `type` | query | integer; пример: `1` | нет | Тип медиакампании: - `1` — размещение по дням - `2` — размещение по просмотрам |
| `limit` | query | integer; пример: `1` | нет | Количество кампаний в ответе |
| `offset` | query | integer; пример: `1` | нет | Смещение относительно первой медиакампании |
| `order` | query | string; пример: `id` | нет | Порядок вывода ответа: - `create` — по времени создания медиакампании - `id` — по ID медиакампании |
| `direction` | query | string; пример: `desc` | нет | Порядок сортировки: - `desc` — от большего к меньшему - `asc` — от меньшего к большему |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: object
  - `advertId` — integer. ID медиакампании
  - `name` — string. Название медиакампании
  - `brand` — string. Название бренда
  - `type` — integer. Тип медиакампании:
  - `status` — integer. Статус медиакампании:
  - `createTime` — string (date-time). Время создания медиакампании
  - `endTime` — string (date-time). Время завершения медиакампании

```json
[
  {
    "advertId": 123456,
    "name": "тост",
    "brand": "brand",
    "type": 2,
    "status": 8,
    "createTime": "2023-03-25T20:35:57.116943+03:00"
  },
  {
    "advertId": 54321,
    "name": "тест",
    "brand": "brandname",
    "type": 1,
    "status": 7,
    "createTime": "2023-07-24T16:48:20.935599+03:00",
    "endTime": "2023-07-25T20:35:50.104978Z"
  }
]
```

#### 204 — Медиакампании не найдены


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
