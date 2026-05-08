# GET /api/v1/supplies/{ID}

**Детали поставки{{ /api/v1/supplies/{ID} }}**

теги: `Информация о поставках`

**Полный путь:** `GET /api/v1/supplies/{ID}`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает детали поставки по ID.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 30 запросов | 2 сек | 10 запросов |
| Сервисный | 1 мин | 30 запросов | 2 сек | 10 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `ID` | path | integer | да | ID поставки или заказа |
| `isPreorderID` | query | boolean | нет | Поиск по:   - `true` — ID заказа, если в `ID` передаёте ID заказа   - `false` — ID поставки, если в `ID` передаёте ID поставки |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `phone` — string. Телефон пользователя, создавшего поставку
- `statusID` — integer; enum: [1, 2, 3, 4, 5, 6]. ID статуса поставки:
- `virtualTypeID` — integer. ID типа виртуальной поставки. Отображается только для поставок с `"boxTypeID":0`.
- `boxTypeID` — integer. ID типа поставки:
- `createDate` — string. Дата и время создания поставки
- `supplyDate` — string. Плановая дата отгрузки поставки
- `factDate` — string. Дата фактической отгрузки поставки
- `updatedDate` — string. Дата изменения поставки
- `warehouseID` — integer. ID склада, на который планируется поставка
- `warehouseName` — string. Название склада, на который планируется поставка
- `actualWarehouseID` — integer. ID склада, на который поставка была привезена
- `actualWarehouseName` — string. Название склада, на который поставка привезена
- `transitWarehouseID` — integer. ID транзитного склада
- `transitWarehouseName` — string. Название транзитного склада
- `acceptanceCost` — number. Предварительная стоимость приёмки, ₽
- `paidAcceptanceCoefficient` — number. Коэффициент приёмки
- `rejectReason` — string. Причина, по которой поставка не может быть принята
- `supplierAssignName` — string. Краткое название продавца
- `storageCoef` — string. Коэффициент хранения
- `deliveryCoef` — string. Коэффициент логистики
- `quantity` — integer. Добавлено в поставку/заказ, шт
- `readyForSaleQuantity` — integer. Поступило в продажу, шт
- `acceptedQuantity` — integer. Принято, шт
- `unloadingQuantity` — integer. Количество товара, находящегося на раскладке, шт
- `depersonalizedQuantity` — integer. Количество обезличенного товара, шт
- `isBoxOnPallet` — boolean. Тип поставки — **Поштучная палета**:

```json
{
  "phone": "+7 903 *** 98 62",
  "statusID": 5,
  "boxTypeID": 2,
  "createDate": "2025-07-15T17:17:45+03:00",
  "supplyDate": "2025-07-15T00:00:00+03:00",
  "factDate": "2025-07-18T11:37:32+03:00",
  "updatedDate": "2025-07-18T12:59:53+03:00",
  "warehouseID": 507,
  "warehouseName": "Коледино",
  "actualWarehouseID": 507,
  "actualWarehouseName": "Коледино",
  "transitWarehouseID": null,
  "transitWarehouseName": "",
  "acceptanceCost": 5000,
  "paidAcceptanceCoefficient": 10,
  "rejectReason": null,
  "supplierAssignName": "Магазин",
  "storageCoef": "215",
  "deliveryCoef": "200",
  "quantity": 10,
  "readyForSaleQuantity": 0,
  "acceptedQuantity": 10,
  "unloadingQuantity": 10,
  "depersonalizedQuantity": 0,
  "isBoxOnPallet": true
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `status` — integer. HTTP статус-код
- `title` — string. ID ошибки
- `detail` — string. Описание ошибки
- `requestId` — string. ID запроса
- `origin` — string. Сервис, вернувший ошибку

*BadPathParamFormat:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "неверный формат id (должен быть int64)",
  "requestId": "aee7d3a5378ef3c7ec0e7a5bc94abfcf",
  "origin": "supply-api"
}
```

*BadisPreorderIDFormat:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "Неверный формат isPreorderID",
  "requestId": "a6bdc2a4d2fde51c2036fa8af2483886",
  "origin": "supply-api"
}
```

*PreorderIdSearchError:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "fail to get supply details: по заказу 123456789 найдена поставка 987654321. Используйте поиск по ID поставки",
  "requestId": "bc28456e85d5590c74decbcd9f63cd91",
  "origin": "supply-api"
}
```

*BadID:*

```json
{
  "status": 400,
  "title": "bad request",
  "detail": "id выходит за рамки int64",
  "requestId": "0e35ac7fdbb94695db4004cb4c4ca12b",
  "origin": "supply-api"
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

#### 404 — Не найдено

**Content-Type:** `application/json`

- `status` — integer. HTTP статус-код
- `title` — string. ID ошибки
- `detail` — string. Описание ошибки
- `requestId` — string. ID запроса
- `origin` — string. Сервис, вернувший ошибку

*SupplyNotFound:*

```json
{
  "status": 404,
  "title": "not found",
  "detail": "поставка 1234 не найдена",
  "requestId": "a6bdc2a4d2fde51c2036fa8af2483886",
  "origin": "supply-api"
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
