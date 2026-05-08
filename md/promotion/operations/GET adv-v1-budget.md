# GET /adv/v1/budget

**Бюджет кампании{{ /adv/v1/budget }}**

теги: `Финансы`

**Полный путь:** `GET /adv/v1/budget`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о бюджете [кампании](./promotion#tag/Kampanii/paths/~1api~1advert~1v2~1adverts/get) — максимальной сумме затрат на кампанию. Бюджет кампании можно [пополнить](./promotion#tag/Finansy/paths/~1adv~1v1~1budget~1deposit/post).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 4 запроса | 250 мс | 4 запроса |
| Сервисный | 1 сек | 4 запроса | 250 мс | 4 запроса |
| Базовый | 1 ч | 4 запроса | 15 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `id` | query | integer; пример: `1` | да | ID кампании |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `cash` — integer. Поле не используется. Значение всегда 0.
- `netting` — integer. Поле не используется. Значение всегда 0.
- `total` — integer. Бюджет кампании, ₽

```json
{
  "cash": 0,
  "netting": 0,
  "total": 500
}
```

#### 400 — Неправильный запрос

**Content-Type:** `text/plain`

- string

*CampaignNotBelongSeller:*

```json
"кампания не принадлежит продавцу"
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
