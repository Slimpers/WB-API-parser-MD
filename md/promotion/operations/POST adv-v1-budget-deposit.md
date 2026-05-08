# POST /adv/v1/budget/deposit

**Пополнение бюджета кампании{{ /adv/v1/budget/deposit }}**

теги: `Финансы`

**Полный путь:** `POST /adv/v1/budget/deposit`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод пополняет [бюджет](./promotion#tag/Finansy/paths/~1adv~1v1~1budget/get) кампании. <br>
Чтобы запустить кампанию после пополнения бюджета, используйте метод [Запуск кампании](./promotion#tag/Upravlenie-kampaniyami/paths/~1adv~1v0~1start/get).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Сервисный | 1 сек | 1 запрос | 1 сек | 5 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `id` | query | integer; пример: `1234567` | да | ID кампании |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `sum` — integer; пример: `5000`. Общая сумма пополнения бюджета
- `cashback_sum` — integer; пример: `1000`. Сумма пополнения бюджета промо-бонусами.
- `cashback_percent` — integer; пример: `50`. Процент от суммы пополнения, который можно пополнить промо-бонусами. Нужно указать значение поля percent из ответа метода получения [баланса](./promotion#tag/Finansy/paths/~1adv~1v1~1balance/get)
- `type` — integer; пример: `1`. Тип источника пополнения:
- `return` — boolean. Флаг возврата ответа (`true` — в ответе вернется обновлённый размер бюджета кампании, `false` или не указать параметр вообще — не вернётся.)

**Пример:**

```json
{
  "sum": 5000,
  "cashback_sum": 1000,
  "cashback_percent": 50,
  "type": 1
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`


*ResponseWithReturn:*

```json
{
  "total": 7289
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `error` — string

*DepositAmountMultiple50:*

```json
{
  "error": "Сумма пополнения должна быть кратна 50 руб"
}
```

*MinimumDepositAmountIs500:*

```json
{
  "error": "Минимальная сумма пополнения 1000 рублей"
}
```

*IncorrectType:*

```json
{
  "error": "Invalid Params: cashback can not be used with such type"
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
