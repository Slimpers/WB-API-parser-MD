# PATCH /api/marketplace/v3/supplies/{supplyId}/orders

**Добавить сборочные задания к поставке{{ /api/marketplace/v3/supplies/{supplyId}/orders }}**

теги: `Поставки FBS`

**Полный путь:** `PATCH /api/marketplace/v3/supplies/{supplyId}/orders`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод добавляет до 100 [сборочных заданий](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) к поставке и переводит их в [статус](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1status/post) `confirm` — на сборке.

Может перемещать сборочные задания:
  - между активными поставками
  - из закрытой поставки в активную, если сборочные задания требуют [повторной отгрузки](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1supplies~1orders~1reshipment/get)

<div class="description_important">
  В пустую поставку можно добавить сборочные задания любого габаритного типа. Поставка приобретает габаритный тип первого добавленного сборочного задания <a href ="./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D/get">из поля</a> <code>cargoType</code>.
  <br>
  После этого в поставку можно добавить сборочные задания только того же габаритного типа, что и у поставки.
 </div>

<div class="description_important">
В поставку нельзя добавить сборочные задания, поступившие на разные склады.
</div>
<div class="description_important">
В пустую поставку можно добавить сборочные задания трансграничных или внутренних поставок.
После этого поставка приобретает тип первого добавленного сборочного задания из поля <code>crossBorderType</code>.
Далее в неё можно добавить только сборочные задания такого же типа.
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `orders` — array<integer>. ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    5632423,
    3453452,
    7654533,
    4529544
  ]
}
```

## Ответы


#### 204 — Сборочные задания закреплены за поставкой


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "Передан некорректный параметр"
}
```

#### 401

**Content-Type:** `application/json`

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

#### 403

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": "Доступ запрещён"
}
```

#### 404

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "NotFound",
  "message": "Не найдено"
}
```

#### 409 — Ошибка добавления сборочного задания к поставке

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

*FailedToAddSupplyOrder:*

```json
{
  "code": "FailedToAddSupplyOrder",
  "message": "Не удалось закрепить сборочное задание за поставкой. Убедитесь, что сборочное задание и поставка удовлетворяют всем необходимым требованиям."
}
```

#### 429

**Content-Type:** `application/json`

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
