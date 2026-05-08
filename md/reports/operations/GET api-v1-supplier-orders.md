# GET /api/v1/supplier/orders

**Заказы{{ /api/v1/supplier/orders }}**

теги: `Основные отчёты`

**Полный путь:** `GET /api/v1/supplier/orders`

## Описание

<span>Описание метода</span>

Метод возвращает информацию о заказах.
Данные обновляются раз в 30 минут.

1 строка = 1 заказ = 1 сборочное задание = 1 единица товара.
Для определения заказа рекомендуем использовать поле `srid`.

Информация о заказе хранится 90 дней с момента оформления.

В ответах могут отсутствовать заказы, по которым не подтверждена оплата. Например, заказы с отложенными платежами или оплатой в рассрочку. При этом, если по таким заказам есть продажи, вы можете получить их с помощью [детализаций к отчётам реализации](./financial-reports-and-accounting#tag/Finansovye-otchyoty/paths/~1api~1v5~1supplier~1reportDetailByPeriod/get).

Чтобы получить все оформленные заказы, используйте [Ленту заказов](https://seller.wildberries.ru/content-analytics/order-feed) в личном кабинете.

  Данные этого отчёта являются предварительными и служат для оперативного мониторинга

Для одного ответа на запрос с `flag=0` или без `flag` в системе установлено условное ограничение 80000 строк. Поэтому, чтобы получить все заказы, может потребоваться более, чем один запрос. Во втором и далее запросе в параметре `dateFrom` используйте полное значение поля `lastChangeDate` из последней строки ответа на предыдущий запрос.
 Если в ответе отдаётся пустой массив `[]`, все заказы уже выгружены.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 3 ч | 1 запрос | 3 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | да | Дата и время последнего изменения по заказу.  Дата в формате RFC3339. Можно передать дату или дату со временем. Время можно указывать с точностью до [секунд](./api-information#tag/Vvedenie/Limity-zaprosov) или миллисекунд.  Время передаётся в часовом поясе Москва (UTC+3).  Примеры:   - `2019-06-20`   - `2019-06-20T23:59:59`   - `2019-06-20T00:00:00.12345`   - `2017-03-25T00:00:00` |
| `` |  |  | нет |  |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: OrdersItem

```json
[
  {
    "date": "2022-03-04T18:08:31",
    "lastChangeDate": "2022-03-06T10:11:07",
    "warehouseName": "Подольск",
    "warehouseType": "Склад продавца",
    "countryName": "Россия",
    "oblastOkrugName": "Центральный федеральный округ",
    "regionName": "Московская",
    "supplierArticle": "12345",
    "nmId": 1234567,
    "barcode": "123453559000",
    "category": "Бытовая техника",
    "subject": "Мультистайлеры",
    "brand": "Тест",
    "techSize": "0",
    "incomeID": 56735459,
    "isSupply": false,
    "isRealization": true,
    "totalPrice": 1887,
    "discountPercent": 18,
    "spp": 26,
    "finishedPrice": 1145,
    "priceWithDisc": 1547,
    "isCancel": true,
    "cancelDate": "2022-03-09T00:00:00",
    "sticker": "926912515",
    "gNumber": "34343462218572569531",
    "srid": "11.rf9ef11fce1684117b0nhj96222982382.3.0"
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`


*DateFromFieldRequired:*

```json
{
  "errors": [
    "dateFrom: field required"
  ]
}
```

*DateFromValueNotValidated:*

```json
{
  "errors": "dateFrom: Value not validated"
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
