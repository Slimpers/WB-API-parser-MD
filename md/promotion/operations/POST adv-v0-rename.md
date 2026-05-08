# POST /adv/v0/rename

**Переименование кампании{{ /adv/v0/rename }}**

теги: `Управление кампаниями`

**Полный путь:** `POST /adv/v0/rename`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод меняет название [кампании](./promotion#tag/Kampanii/paths/~1api~1advert~1v2~1adverts/get). Это можно сделать в любой момент существования кампании.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Сервисный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `advertId` **(required)** — integer. ID кампании, в которой меняется название
- `name` **(required)** — string. Новое название (максимум 100 символов)

**Пример:**

```json
{
  "advertId": 2233344,
  "name": "newname"
}
```

## Ответы


#### 200 — Успешно


#### 400 — Неправильный запрос

**Content-Type:** `text/plain`

- string

*InvalidRcIdAdv:*

```json
"Некорректный ID РК"
```

*IncorrectName:*

```json
"Некорректное название"
```

*IncorrectSupplierIdAdv:*

```json
"Некорректный ID продавца"
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

#### 422 — Ошибка обработки параметров запроса

**Content-Type:** `text/plain`

- string

*RequestBodyProcessErrorAdv:*

```json
"Ошибка обработки тела запроса"
```

*CompanyNameChangeErr:*

```json
"Ошибка изменения названия кампании"
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
