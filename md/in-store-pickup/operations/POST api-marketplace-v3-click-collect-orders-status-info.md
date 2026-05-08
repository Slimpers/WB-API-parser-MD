# POST /api/marketplace/v3/click-collect/orders/status/info

**Получить статусы сборочных заданий{{ /api/marketplace/v3/click-collect/orders/status/info }}**

теги: `Сборочные задания Самовывоз`

**Базовый URL:** `https://marketplace-api.wildberries.ru`

**Полный путь:** `POST https://marketplace-api.wildberries.ru/api/marketplace/v3/click-collect/orders/status/info`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает статусы [сборочных заданий](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz) по их ID.
<br><br>
`supplierStatus` — статус сборочного задания. Триггер его изменения - действие самого продавца.

Возможные значения `supplierStatus`:
| Статус   | Описание            | Как перевести сборочное задание в данный статус |
| -------  | ---------           | --------------------------------------|
| `new`      | **Новое сборочное задание** |
| `confirm`  | **На сборке**  | 	[Перевести сборочное задание на сборку](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1confirm/post)
| `prepare`  | **Готов к выдаче** | 	[Сообщить, что сборочное задание готово к выдаче](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1prepare/post)
| `receive`  | **Получено покупателем**   | [Сообщить, что заказ принят покупателем](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1receive/post)
| `reject`  | **Отказ покупателя при получении**    |  	[Сообщить, что покупатель отказался от заказа](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1reject/post)
| `cancel`   | **Отменено продавцом**    |  	[Отменить сборочное задание](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz/paths/~1api~1marketplace~1v3~1click-collect~1orders~1status~1cancel/post)
| `cancel_shelf_life` | **Отмена по истечении срока хранения**    |  	Переводится автоматически по возникновению события

<br><br>
`wbStatus` — статус системы Wildberries.

Возможные значения `wbStatus`:
- `waiting` - сборочное задание в работе
- `sold` - заказ получен покупателем
- `canceled` - отмена сборочного задания
- `canceled_by_client` - покупатель отменил заказ при получении
- `declined_by_client` - покупатель отменил заказ в первый чаc
<br> Отмена доступна покупателю в первый час с момента заказа, если заказ не переведён на сборку
- `defect` - отмена заказа по причине брака
- `ready_for_pickup` - заказ готов к выдаче

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий Самовывоз</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 сек | 1 запрос | 1 сек | 10 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `ordersIds` — array<integer>. Список ID сборочных заданий

**Пример:**

```json
{
  "ordersIds": [
    123456,
    234567
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<$ref: api.OrderStatusV2>. Информация о статусах

```json
{
  "orders": [
    {
      "supplierStatus": "confirm",
      "wbStatus": "waiting",
      "errors": [],
      "orderId": 123456
    },
    {
      "supplierStatus": "",
      "wbStatus": "",
      "errors": [
        {
          "code": 404,
          "detail": "NotFound"
        }
      ],
      "orderId": 789012
    }
  ]
}
```

#### 400

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` **(required)** — string; пример: `market-public-api`. ID внутреннего сервиса WB
- `requestId` **(required)** — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` **(required)** — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "market-public-api",
  "requestId": "f1787bd2d1fdс35d6f537316514у4a05",
  "title": "IncorrectRequest"
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

#### 403

**Content-Type:** `application/json`

- `detail` — object. Детали ошибки
  - *(пустой object)*
- `origin` **(required)** — string; пример: `market-public-api`. ID внутреннего сервиса WB
- `requestId` **(required)** — string; пример: `f1787bd2d1fdс35d6f537316514у4a05`. Уникальный ID запроса
- `title` **(required)** — string; пример: `IncorrectRequest`. Заголовок ошибки

```json
{
  "detail": {},
  "origin": "market-public-api",
  "requestId": "f1787bd2d1fdс35d6f537316514у4a05",
  "title": "AccessDenied"
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
