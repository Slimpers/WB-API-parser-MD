# POST /api/v3/orders/status

**Получить статусы сборочных заданий{{ /api/v3/orders/status }}**

теги: `Сборочные задания FBS`

**Полный путь:** `POST /api/v3/orders/status`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает статусы [сборочных заданий](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders/get) по их ID.
<br><br>
`supplierStatus` — статус сборочного задания. Триггер его изменения — действие самого продавца.

Возможные значения `supplierStatus`:

| Статус   | Описание            | Как перевести сборочное задание в данный статус |
|-------|----------------------|--------------------------------------|
| `new`      | **Новое сборочное задание** |  |
| `confirm`  | **На сборке** |[Добавить сборочное задание к поставке](/openapi/orders-fbs#tag/Postavki-FBS/paths/~1api~1marketplace~1v3~1supplies~1%7BsupplyId%7D~1orders/patch)
| `complete` | **В доставке** | [Передать поставку в доставку](/openapi/orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1deliver/patch) |
| `cancel`   | **Отменено продавцом**   | [Отменить сборочное задание](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1cancel/patch)|
| `cancel_carrier`   | **Отменено перевозчиком** <br>Только для трансграничных поставок   | Переводится перевозчиком |

<br><br>
`wbStatus` — статус системы Wildberries.

Возможные значения `wbStatus`:
- `waiting` — сборочное задание в работе
- `sorted` — сборочное задание отсортировано
- `sold` — заказ получен покупателем
- `canceled` — отмена сборочного задания
- `canceled_by_client` — покупатель отменил заказ при получении
- `declined_by_client` — покупатель отменил заказ. Отмена доступна покупателю в первый час с момента заказа, если заказ не переведён на сборку
- `defect` — отмена заказа по причине брака
- `ready_for_pickup` — заказ прибыл на пункт выдачи заказов (ПВЗ)
- `accepted_by_carrier` — продавец передал заказ в службу доставки в своей стране
- `sent_to_carrier` — заказ отправлен на склад службы доставки в стране продавца
- `canceled_by_carrier` — заказ отменён перевозчиком. Только для трансграничных поставок

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` **(required)** — array<integer (int64); пример: `5632423`>. Список ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    5632423
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<object>
  - *(элементы)*
    - `id` — integer (int64); пример: `5632423`. ID сборочного задания
    - `isCancellable` — boolean; пример: `False`. Доступна ли [отмена](/openapi/orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1cancel/patch) сборочного задания:
    - `supplierStatus` — string; enum: ["new", "confirm", "complete", "cancel"]; пример: `new`. Статус сборочного задания, установленный продавцом
    - `wbStatus` — string; enum: ["waiting", "sorted", "sold", "canceled", "canceled_by_client", "declined_by_client", "defect", "ready_for_pickup", "postponed_delivery", "accepted_by_carrier"]. Статус сборочного задания в системе Wildberries

```json
{
  "orders": [
    {
      "id": 5632423,
      "isCancellable": false,
      "supplierStatus": "new",
      "wbStatus": "waiting"
    }
  ]
}
```

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

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": "Некорректное тело запроса"
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": "Переданы некорректные данные"
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

#### 402

**Content-Type:** `application/problem+json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки. Ошибка возвращается только сервисам из [Каталога решений для бизнеса](https://dev.wildberries.ru/business-solutions)

```json
{
  "title": "payment required",
  "detail": "wb solution for business has insufficient funds on its balance. please top up the balance in the company's personal account https://dev.wildberries.ru/company"
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
