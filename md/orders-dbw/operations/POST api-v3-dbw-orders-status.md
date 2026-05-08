# POST /api/v3/dbw/orders/status

**Получить статусы сборочных заданий{{ /api/v3/dbw/orders/status }}**

теги: `Сборочные задания DBW`

**Полный путь:** `POST /api/v3/dbw/orders/status`

## Описание

<span>Описание метода</span>

Метод возвращает статусы сборочных заданий по их ID.

`supplierStatus` — статус сборочного задания.
Триггер его изменения — действие самого продавца.

Возможные значения `supplierStatus`:
| Статус   | Описание            | Как перевести сборочное задание в данный статус |
| -------  | ---------           | --------------------------------------|
| `new`      | **Новое сборочное задание** | |
| `confirm`  | **На сборке**      |  [Перевести сборочное задание на сборку](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1{orderId}~1confirm/patch)
| `complete` | **В доставке**  | [Перевести сборочное задание в доставку](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1marketplace~1v3~1dbw~1orders~1status~1assemble/post) |
| `receive`  | **Получено покупателем**|  Переводится курьером
| `reject`   | **Отказ покупателя при получении**| Переводится курьером
| `cancel`   | **Отменено продавцом**   |  [Отменить сборочное задание](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1{orderId}~1cancel/patch)
| `cancel_missed_call` | **Отмена по причине недозвона**
 | Статус меняется автоматически |

`wbStatus` — статус системы Wildberries.

Возможные значения `wbStatus`:
- `waiting` — сборочное задание в работе
- `sold` — заказ получен покупателем
- `canceled` — отмена сборочного задания
- `canceled_by_client` — покупатель отменил заказ при получении
- `declined_by_client` — покупатель отменил заказ в первый чаc

Отмена доступна покупателю в первый час с момента заказа, если заказ не переведен на сборку
- `defect` — отмена заказа по причине брака
- `canceled_by_missed_call` — отмена заказа по причине недозвона
- `postponed_delivery` — курьерская доставка отложена

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для следующих методов DBW:
<ul>
    <li>получение и обновление списка контактов</li>
    <li>получение и удаление метаданных</li>
    <li>методы сборочных заданий</li>
</ul>

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов

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
    - `supplierStatus` — string; пример: `new`. Статус сборочного задания, установленный продавцом
    - `wbStatus` — string. Статус сборочного задания в системе Wildberries

```json
{
  "orders": [
    {
      "id": 5632423,
      "supplierStatus": "new"
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
  "message": ""
}
```

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": ""
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": ""
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
  "message": ""
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
