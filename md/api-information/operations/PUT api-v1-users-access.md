# PUT /api/v1/users/access

**Изменить права доступа пользователей{{ /api/v1/users/access }}**

теги: `Управление пользователями продавца`

**Полный путь:** `PUT /api/v1/users/access`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_token">
Метод доступен по<strong> Персональному</strong> <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">токену</a>
</div>

Метод меняет права доступа одному или нескольким пользователям.<br>
<br>
Обновляются только права доступа, переданные в параметрах запроса. Остальные поля остаются без изменений.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 5 запросов |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `usersAccesses` **(required)** — array<$ref: UserAccess>. Настройки доступа для пользователя

**Пример:**

```json
{
  "usersAccesses": [
    {
      "userId": 42334965,
      "access": [
        {
          "code": "balance",
          "disabled": false
        },
        {
          "code": "finance",
          "disabled": true
        },
        {
          "code": "feedbacks",
          "disabled": false
        }
      ]
    },
    {
      "userId": 52334965,
      "access": [
        {
          "code": "balance",
          "disabled": true
        },
        {
          "code": "changeJam",
          "disabled": false
        },
        {
          "code": "showcase",
          "disabled": false
        }
      ]
    }
  ]
}
```

## Ответы


#### 200 — Успешно


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
