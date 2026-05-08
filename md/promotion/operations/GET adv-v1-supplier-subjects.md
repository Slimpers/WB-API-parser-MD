# GET /adv/v1/supplier/subjects

**Предметы для кампаний{{ /adv/v1/supplier/subjects }}**

теги: `Создание кампаний`

**Полный путь:** `GET /adv/v1/supplier/subjects`

## Описание

<span>Описание метода</span>

Метод возвращает список [предметов](./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1object~1all/get), которые можно добавить в рекламную [кампанию](./promotion#tag/Kampanii/paths/~1api~1advert~1v2~1adverts/get).

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 12 сек | 1 запрос | 12 сек | 5 запросов |
| Сервисный | 12 сек | 1 запрос | 12 сек | 5 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `payment_type` | query | string | нет | Тип оплаты: - `cpm` — за показы - `cpc` — за клик |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: object
  - `id` — integer. ID предмета
  - `name` — string. Предмет
  - `count` — integer. Количество Артикулов WB (`nmId`) с таким предметом.

*Array:*

```json
[
  {
    "name": "3D очки",
    "id": 2560,
    "count": 1899
  }
]
```

*null:*

```json
null
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

#### 404 — Не найдено


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
