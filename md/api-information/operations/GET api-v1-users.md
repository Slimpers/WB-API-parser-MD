# GET /api/v1/users

**Получить список активных или приглашённых пользователей продавца{{ /api/v1/users }}**

теги: `Управление пользователями продавца`

**Полный путь:** `GET /api/v1/users`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_token">
Метод доступен по<strong> Персональному</strong> <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">токену</a>
</div>

Метод возвращает список активных или приглашённых пользователей профиля продавца.<br><br>
Чтобы выбрать список, укажите значение параметра `isInviteOnly`:
  - `isInviteOnly=true` — список приглашённых пользователей, которые ещё не активировали доступ
  - `isInviteOnly=false` или не указан — список активных пользователей

По каждому пользователю можно получить:
  - роль пользователя
  - разделы, к которым есть доступы
  - статус приглашения

Список приглашённых пользователей в ответе всегда отсортирован по дате создания: от новых до старых.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 5 запросов |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `limit` | query | integer (int64) | нет | Количество активных или приглашённых пользователей в ответе |
| `offset` | query | integer (int64) | нет | Сколько элементов пропустить. Например, для значения 10 ответ начнется с 11 элемента |
| `isInviteOnly` | query | boolean | нет | - `true` — список приглашённых пользователей, которые ещё не активировали доступ - `false` или не указан — список активных пользователей профиля продавца |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `total` **(required)** — integer. Общее количество активных или приглашённых пользователей
- `countInResponse` **(required)** — integer. Количество активных или приглашённых пользователей на текущей странице
- `users` **(required)** — array<object>. Информация о пользователях
  - *(элементы)*
    - `id` **(required)** — integer. ID пользователя
    - `role` **(required)** — string; enum: ["user", ""]. Роль пользователя:
    - `position` **(required)** — string. Должность пользователя
    - `phone` **(required)** — string. Номер телефона пользователя
    - `email` **(required)** — string. Email пользователя
    - `isOwner` **(required)** — boolean. Является ли пользователь владельцем профиля продавца
    - `firstName` **(required)** — string. Имя пользователя
    - `secondName` **(required)** — string. Фамилия пользователя
    - `patronymic` **(required)** — string. Отчество пользователя
    - `goodsReturn` **(required)** — boolean. Может ли пользователь одобрять возвраты товаров
    - `isInvitee` **(required)** — boolean. Приглашён ли пользователь
    - `inviteeInfo` **(required)** — object. Информация о приглашении, если пользователь приглашён
      - `phoneNumber` — string. Номер телефона приглашённого пользователя
      - `position` — string. Должность приглашённого пользователя
      - `inviteUuid` — string (UUID). ID приглашения
      - `expiredAt` — string (date-time). Дата и время окончания срока действия приглашения
      - `isActive` — boolean. - `true` — приглашение активно
    - `access` **(required)** — $ref: Access

*invitesOnly:*

```json
{
  "total": 2,
  "countInResponse": 2,
  "users": [
    {
      "id": 0,
      "role": "",
      "position": "Аналитик",
      "phone": "79998888888",
      "email": "",
      "isOwner": false,
      "firstName": "",
      "secondName": "",
      "patronymic": "",
      "goodsReturn": false,
      "isInvitee": true,
      "inviteeInfo": {
        "phoneNumber": "79998888888",
        "position": "Аналитик",
        "inviteUuid": "00000000-0000-4000-8000-000000000001",
        "expiredAt": "2025-12-01T00:00:00Z",
        "isActive": true
      },
      "access": [
        {
          "code": "supply",
          "disabled": true
        },
        {
          "code": "changeJam",
          "disabled": true
        },
        {
          "code": "showcase",
          "disabled": false
        },
        {
          "code": "suppliersDocuments",
          "disabled": false
        },
        {
          "code": "discountPrice",
          "disabled": true
        },
        {
          "code": "feedbacks",
          "disabled": false
        },
        {
          "code": "questions",
          "disabled": false
        },
        {
          "code": "wbPoint",
          "disabled": false
        },
        {
          "code": "brands",
          "disabled": true
        },
        {
          "code": "pointsForReviews",
          "disabled": false
        },
        {
          "code": "pinFeedbacks",
          "disabled": false
        },
        {
          "code": "finance",
          "disabled": true
        },
        {
          "code": "feedbacksQuestions",
          "disabled": false
        },
        {
          "code": "balance",
          "disabled": false
        },
        {
          "code": "oldAnalyticsReports",
          "disabled": false
        },
        {
          "code": "marketplace",
          "disabled": false
        }
      ]
    },
    {
      "id": 0,
      "role": "",
      "position": "",
      "phone": "7999XXXX102",
      "email": "",
      "isOwner": false,
      "firstName": "",
      "secondName": "",
      "patronymic": "",
      "goodsReturn": false,
      "isInvitee": true,
      "inviteeInfo": {
        "phoneNumber": "79996666666",
        "position": "Аналитик",
        "inviteUuid": "00000000-0000-4000-8000-000000000002",
        "expiredAt": "2025-12-10T00:00:00Z",
        "isActive": false
      },
      "access": [
        {
          "code": "supply",
          "disabled": true
        },
        {
          "code": "changeJam",
          "disabled": true
        },
        {
          "code": "showcase",
          "disabled": false
        },
        {
          "code": "suppliersDocuments",
          "disabled": false
        },
        {
          "code": "discountPrice",
          "disabled": true
        },
        {
          "code": "feedbacks",
          "disabled": false
        },
        {
          "code": "questions",
          "disabled": false
        },
        {
          "code": "wbPoint",
          "disabled": false
        },
        {
          "code": "brands",
          "disabled": true
        },
        {
          "code": "pointsForReviews",
          "disabled": false
        },
        {
          "code": "pinFeedbacks",
          "disabled": false
        },
        {
          "code": "finance",
          "disabled": true
        },
        {
          "code": "feedbacksQuestions",
          "disabled": false
        },
        {
          "code": "balance",
          "disabled": false
        },
        {
          "code": "oldAnalyticsReports",
          "disabled": false
        },
        {
          "code": "marketplace",
          "disabled": false
        }
      ]
    }
  ]
}
```

*usersOnly:*

```json
{
  "total": 2,
  "countInResponse": 2,
  "users": [
    {
      "id": 1001,
      "role": "user",
      "position": "Аналитик",
      "phone": "79999999999",
      "email": "user1@example.com",
      "isOwner": true,
      "firstName": "Иван",
      "secondName": "Иванов",
      "patronymic": "",
      "goodsReturn": true,
      "isInvitee": false,
      "inviteeInfo": null,
      "access": [
        {
          "code": "supply",
          "disabled": true
        },
        {
          "code": "changeJam",
          "disabled": true
        },
        {
          "code": "showcase",
          "disabled": false
        },
        {
          "code": "suppliersDocuments",
          "disabled": false
        },
        {
          "code": "discountPrice",
          "disabled": true
        },
        {
          "code": "feedbacks",
          "disabled": false
        },
        {
          "code": "questions",
          "disabled": false
        },
        {
          "code": "wbPoint",
          "disabled": false
        },
        {
          "code": "brands",
          "disabled": true
        },
        {
          "code": "pointsForReviews",
          "disabled": false
        },
        {
          "code": "pinFeedbacks",
          "disabled": false
        },
        {
          "code": "finance",
          "disabled": true
        },
        {
          "code": "feedbacksQuestions",
          "disabled": false
        },
        {
          "code": "balance",
          "disabled": false
        },
        {
          "code": "oldAnalyticsReports",
          "disabled": false
        },
        {
          "code": "marketplace",
          "disabled": false
        }
      ]
    },
    {
      "id": 1002,
      "role": "user",
      "position": "Менеджер",
      "phone": "79997777777",
      "email": "user2@example.com",
      "isOwner": false,
      "firstName": "Владимир",
      "secondName": "Смирнов",
      "patronymic": "",
      "goodsReturn": true,
      "isInvitee": true,
      "inviteeInfo": {
        "phoneNumber": "79997777777",
        "position": "Менеджер",
        "inviteUuid": "00000000-0000-4000-8000-000000000001",
        "expiredAt": "2025-12-01T00:00:00Z",
        "isActive": true
      },
      "access": [
        {
          "code": "supply",
          "disabled": true
        },
        {
          "code": "changeJam",
          "disabled": true
        },
        {
          "code": "showcase",
          "disabled": false
        },
        {
          "code": "suppliersDocuments",
          "disabled": false
        },
        {
          "code": "discountPrice",
          "disabled": true
        },
        {
          "code": "feedbacks",
          "disabled": false
        },
        {
          "code": "questions",
          "disabled": false
        },
        {
          "code": "wbPoint",
          "disabled": false
        },
        {
          "code": "brands",
          "disabled": true
        },
        {
          "code": "pointsForReviews",
          "disabled": false
        },
        {
          "code": "pinFeedbacks",
          "disabled": false
        },
        {
          "code": "finance",
          "disabled": true
        },
        {
          "code": "feedbacksQuestions",
          "disabled": false
        },
        {
          "code": "balance",
          "disabled": false
        },
        {
          "code": "oldAnalyticsReports",
          "disabled": false
        },
        {
          "code": "marketplace",
          "disabled": false
        }
      ]
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` **(required)** — string. Заголовок ошибки
- `detail` **(required)** — string. Детали ошибки
- `requestId` **(required)** — string. ID запроса
- `origin` **(required)** — string. Название внутреннего сервиса
- `status` **(required)** — number. HTTP статус-код

```json
{
  "title": "Bad Request",
  "status": 400,
  "detail": "bad request cause: user is not in current supplier",
  "requestId": "c479c04d0b576a9ba0b20fdf235004c2",
  "origin": "public-acl"
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
