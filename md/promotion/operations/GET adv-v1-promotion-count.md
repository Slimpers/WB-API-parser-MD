# GET /adv/v1/promotion/count

**Списки кампаний{{ /adv/v1/promotion/count }}**

теги: `Кампании`

**Полный путь:** `GET /adv/v1/promotion/count`

## Описание

<span>Описание метода</span>

Метод возвращает списки всех [рекламных кампаний](./promotion#tag/Kampanii/paths/~1api~1advert~1v2~1adverts/get) продавца с их ID. Кампании сгруппированы по типу и статусу, у каждой указана дата последнего изменения.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Сервисный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `adverts` — array<object>. Данные по кампаниям
  - *(элементы)*
    - `type` — integer. Тип кампании:
    - `status` — integer. Статус кампании
    - `count` — integer. Количество кампаний
    - `advert_list` — array<object>. Список кампаний
      - *(элементы)*
        - `advertId` — integer. ID кампании
        - `changeTime` — string (date-time). Дата и время последнего изменения кампании
- `all` — integer. Общее количество кампаний всех статусов и типов

```json
{
  "adverts": [
    {
      "type": 9,
      "status": 8,
      "count": 3,
      "advert_list": [
        {
          "advertId": 6485174,
          "changeTime": "2023-05-10T12:12:52.676254+03:00"
        },
        {
          "advertId": 6500443,
          "changeTime": "2023-05-10T17:08:46.370656+03:00"
        },
        {
          "advertId": 7936341,
          "changeTime": "2023-07-12T15:51:08.367478+03:00"
        }
      ]
    }
  ],
  "all": 3
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
