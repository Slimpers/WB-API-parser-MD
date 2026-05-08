# POST /api/finance/v1/sales-reports/detailed

**Детализации к отчётам реализации за период{{ /api/finance/v1/sales-reports/detailed }}**

`operationId`: postV1SalesReportsDetailed  
теги: `Финансовые отчёты`

**Полный путь:** `POST /api/finance/v1/sales-reports/detailed`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает детализации к [отчётам реализации](https://seller.wildberries.ru/suppliers-mutual-settlements) за указанный период.
<br><br>
Данные доступны с 29 января 2024 года.

<div class="description_important">
  Вы можете выгрузить данные в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a4-650c-7b04-9596-ba441936f9d3">Google Таблицы</a>
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Сервисный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Базовый | 24 ч | 2 запроса | 12 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

Параметры запроса
- `dateFrom` **(required)** — string; пример: `2026-03-17`. Начальная дата отчёта.<br>Можно передать дату или дату со временем. Время можно указывать с точностью до секунд или миллисекунд.<br>Дата передаётся в формате [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339), время — в часовом поясе Москва `UTC+3`.<br>Примеры:
- `dateTo` **(required)** — string; пример: `2026-03-20`. Конечная дата отчёта.<br>Дата в формате [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339). Можно передать дату или дату со временем. Время можно указывать с точностью до секунд или миллисекунд.<br>Время передаётся в часовом поясе Москва `UTC+3`.<br>Примеры:
- `limit` — integer; пример: `21100`. Количество строк в ответе
- `rrdId` — integer. ID строки ответа. Необходим для получения отчёта частями.<br>Начинайте загрузку отчёта с `"rrdid":0`. В последующих запросах передавайте значение `rrdId` из последней строки предыдущего ответа.<br>Повторяйте запрос, пока не получите ответ `204`
- `period` — string; enum: ["daily", "weekly"]; пример: `daily`. Периодичность отчётов:
- `fields` — array<string>. Список полей, которые вернутся в ответе. Если параметр не указан, возвращаются все поля

**Пример:**

```json
{
  "dateFrom": "2026-03-17",
  "dateTo": "2026-03-20",
  "limit": 21100,
  "period": "daily",
  "fields": [
    "rrdId",
    "nmId",
    "docTypeName",
    "retailAmount",
    "acquiringFee",
    "srid"
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: SalesReportsDetailedRes

```json
[
  {
    "reportId": 1234567,
    "dateFrom": "2026-03-16",
    "dateTo": "2026-03-22",
    "createDate": "2026-03-23",
    "currency": "RUB",
    "reportType": 1,
    "rrdId": 1232610467,
    "giId": 123456,
    "dlvPrc": 1.8,
    "fixTariffDateFrom": "2026-03-18",
    "fixTariffDateTo": "2026-03-19",
    "subjectName": "Мини-печи",
    "nmId": 1234567,
    "brandName": "BlahBlah",
    "vendorCode": "MAB123",
    "title": "ДС тарелка",
    "techSize": "0",
    "sku": "1231312352310",
    "docTypeName": "Продажа",
    "quantity": 1,
    "retailPrice": "1249",
    "retailAmount": "367",
    "salePercent": 0,
    "commissionPercent": 24,
    "officeName": "Коледино",
    "sellerOperName": "Продажа",
    "orderDt": "2026-03-14T00:00:00Z",
    "saleDt": "2026-03-21T00:00:00Z",
    "rrDate": "2025-10-20",
    "shkId": 1239159661,
    "retailPriceWithDisc": "399.68",
    "deliveryAmount": 0,
    "returnAmount": 0,
    "deliveryService": "0",
    "giBoxTypeName": "Монопаллета",
    "productDiscountForReport": 0,
    "sellerPromo": "0",
    "spp": 25.31,
    "kvwBase": 24.15,
    "kvw": 1.81,
    "ppvzSalesCommission": "23.74",
    "forPay": "376.99",
    "ppvzReward": "0",
    "acquiringFee": "14.89",
    "acquiringPercent": 4.06,
    "paymentProcessing": "Комиссия за организацию платежа с НДС",
    "acquiringBank": "Тинькофф",
    "vw": "22.25",
    "vwNds": "4.45",
    "ppvzOfficeName": "Москва Москва Очаковское шоссе 6к2",
    "ppvzOfficeId": 105383,
    "ppvzSupplierName": "ИП Жасмин",
    "ppvzSupplierInn": "010101010101",
    "declarationNumber": "",
    "bonusTypeName": "Штраф МП. Невыполненный заказ (отмена клиентом после недовоза)",
    "stickerId": "1964038895",
    "country": "Россия",
    "srvDbs": true,
    "penalty": "231.35",
    "additionalPayment": "0",
    "rebillLogisticCost": "1.349",
    "rebillLogisticOrg": "ИП Иванов Иван Иванович(123456789012)",
    "paidStorage": "12647.29",
    "deduction": "6354",
    "paidAcceptance": "865",
    "orderId": 2816993144,
    "kiz": "0102900000376311210G2CIS?ehge)S\u001d91002A\u001d92F9Qof4FDo/31Icm14kmtuVYQzLypxm3HWkC1vQ/+pVVjm1dNAth1laFMoAGn7yEMWlTjxIe7lQnJqZ7TRZhlHQ==",
    "isB2b": false,
    "trbxId": "WB-TRBX-1234567",
    "installmentCofinancingAmount": "0",
    "wibesDiscountPercent": 1,
    "cashbackAmount": "2",
    "cashbackDiscount": "19",
    "cashbackCommissionChange": "0.2",
    "paymentSchedule": "-1",
    "deliveryMethod": "FBS, (МГТ)",
    "sellerPromoId": 14350,
    "sellerPromoDiscount": 3,
    "loyaltyId": 0,
    "loyaltyDiscount": 0,
    "uuidPromocode": "",
    "salePricePromocodeDiscountPrc": 0,
    "articleSubstitution": "",
    "salePriceAffiliatedDiscountPrc": 0,
    "agencyVat": 0,
    "salePriceWholesaleDiscountPrc": 0,
    "orderUid": "id375f16c4bec295d9995393af803ff7b",
    "srid": "0f1c3999172603062979867564654dac5b702849"
  }
]
```

#### 204 — Нет данных


#### 400

**Content-Type:** `application/problem+json`

- `status` — integer; пример: `400`. HTTP статус-код
- `title` — string; пример: `GetReportDetailByPeriodNB decode error`. Заголовок ошибки
- `detail` — string; пример: `GetReportDetailByPeriodNB decode error: missing dateTo params`. Детали ошибки
- `requestId` — string; пример: `b065c204-c5f7-431b-b12c-d4c2cc6347ec`. ID запроса
- `origin` — string; пример: `open-api-finreports`. ID внутреннего сервиса WB

```json
{
  "status": 400,
  "title": "GetReportDetailByPeriodNB decode error",
  "detail": "GetReportDetailByPeriodNB decode error: missing dateTo params",
  "requestId": "b065c204-c5f7-431b-b12c-d4c2cc6347ec",
  "origin": "open-api-finreports"
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
