# POST /api/v1/invite

**Создать приглашение для нового пользователя{{ /api/v1/invite }}**

теги: `Управление пользователями продавца`

**Полный путь:** `POST /api/v1/invite`

## Описание

<span>Описание метода</span>

Метод доступен по<strong> Персональному</strong> <a href="./api-information#tag/Avtorizaciya/Pravila-ispolzovaniya-tokenov-dostupa-k-API">токену</a>

Метод создаёт приглашение для нового пользователя с настройкой доступов к разделам профиля продавца.

Как выдаются права доступа:
- Если `access` пустой (`[]`) или не указан — по умолчанию выдаются все доступы, кроме доступов к витрине (`showcase`) и **Джем** (`changeJam`)
- Если в `access` указана часть разделов профиля, то кроме тех доступов, что указаны в запросе, также выдаются все доступы по умолчанию
- Если в `access` перечислены все возможные разделы, доступы будут выданы согласно запросу, без доступов по умолчанию
- Если в `access` дважды указан один и тот же раздел (`code`):
  - при разных значениях `disabled` (`true` и `false`) доступ не будет выдан
  - при одинаковых значениях `"disabled": true` доступ не будет выдан
  - при одинаковых значениях `"disabled": false` доступ будет выдан

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 5 запросов |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `access` — $ref: Access
- `invite` **(required)** — object
  - `phoneNumber` **(required)** — string. Номер телефона пользователя для приглашения.
  - `position` — string. Должность пользователя

**Пример:**

```json
{
  "access": [
    {
      "code": "balance",
      "disabled": false
    },
    {
      "code": "pointsForReviews",
      "disabled": false
    },
    {
      "code": "brands",
      "disabled": true
    },
    {
      "code": "finance",
      "disabled": true
    },
    {
      "code": "supply",
      "disabled": true
    }
  ],
  "invite": {
    "phoneNumber": "79999999999",
    "position": "Менеджер"
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

Данные приглашения
- `inviteID` **(required)** — string (uuid). ID приглашения
- `expiredAt` **(required)** — string (date-time). Дата и время окончания срока действия приглашения
- `isSuccess` **(required)** — boolean. - `true` — приглашение создано успешно
- `inviteUrl` **(required)** — string (uri). URL приглашения, по которому должен перейти пользователь

```json
{
  "inviteID": "741b8aa6-08ac-4782-8a9d-d931bcbbf608",
  "expiredAt": "2025-10-06T10:56:04.335060746Z",
  "isSuccess": true,
  "inviteUrl": "https://seller.wildberries.ru/supplier-settings/supplier-card?inviteId=e5a813c7-65e0-4599-a550-a6b3d85661ed"
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
