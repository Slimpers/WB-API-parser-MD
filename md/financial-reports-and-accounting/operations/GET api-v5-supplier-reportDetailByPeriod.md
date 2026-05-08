# GET /api/v5/supplier/reportDetailByPeriod

**Отчёт о продажах по реализации{{ /api/v5/supplier/reportDetailByPeriod }}**

> ⚠️ DEPRECATED

теги: `Финансовые отчёты`

**Полный путь:** `GET /api/v5/supplier/reportDetailByPeriod`

## Описание

<span>Описание метода</span>

Данный метод устарел. Он будет удалён [15 июля](https://dev.wildberries.ru/release-notes?id=498).

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Сервисный | 1 мин | 1 запрос | 1 мин | 10 запросов |
| Базовый | 24 ч | 2 запроса | 12 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `dateFrom` | query | string (date-time) | да | Начальная дата отчёта.  Дата в формате RFC3339. Можно передать дату или дату со временем. Время можно указывать с точностью до секунд или миллисекунд.  Время передаётся в часовом поясе Москва (UTC+3).  Примеры:   - `2019-06-20`   - `2019-06-20T23:59:59`   - `2019-06-20T00:00:00.12345`   - `2017-03-25T00:00:00` |
| `dateTo` | query | string (date-time) | да | Конечная дата отчёта |
| `limit` | query | integer | нет | Количество строк в ответе |
| `rrdid` | query | integer | нет | Уникальный ID строки отчёта. Необходим для получения отчёта частями.  Загрузку отчёта нужно начинать с `rrdid = 0` и при последующих вызовах API передавать в запросе значение `rrd_id` из последней строки, полученной в результате предыдущего вызова.  Таким образом, для загрузки одного отчёта может понадобиться вызывать API до тех пор, пока не вернётся ответ 204. |
| `period` | query | string; enum: ["weekly", "daily"] | нет | Периодичность отчётов:   - `weekly` — еженедельные   - `daily` — ежедневные |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: $ref: DetailReportItem

```json
[
  {
    "realizationreport_id": 1234567,
    "date_from": "2022-10-17",
    "date_to": "2022-10-23",
    "create_dt": "2022-10-24",
    "currency_name": "руб",
    "rrd_id": 1232610467,
    "gi_id": 123456,
    "dlv_prc": 1.8,
    "fix_tariff_date_from": "2024-10-23",
    "fix_tariff_date_to": "2024-11-18",
    "subject_name": "Мини-печи",
    "nm_id": 1234567,
    "brand_name": "BlahBlah",
    "sa_name": "MAB123",
    "ts_name": "0",
    "barcode": "1231312352310",
    "doc_type_name": "Продажа",
    "quantity": 1,
    "retail_price": 1249,
    "retail_amount": 367,
    "sale_percent": 0,
    "commission_percent": 24,
    "office_name": "Коледино",
    "supplier_oper_name": "Продажа",
    "order_dt": "2022-10-13T00:00:00Z",
    "sale_dt": "2022-10-20T00:00:00Z",
    "rr_dt": "2022-10-20",
    "shk_id": 1239159661,
    "retail_price_withdisc_rub": 399.68,
    "delivery_amount": 0,
    "return_amount": 0,
    "delivery_rub": 0,
    "gi_box_type_name": "Монопаллета",
    "product_discount_for_report": 0,
    "supplier_promo": 0,
    "ppvz_spp_prc": 25.31,
    "ppvz_kvw_prc_base": 24.15,
    "ppvz_kvw_prc": 1.81,
    "ppvz_sales_commission": 23.74,
    "ppvz_for_pay": 376.99,
    "ppvz_reward": 0,
    "acquiring_fee": 14.89,
    "acquiring_percent": 4.06,
    "payment_processing": "Комиссия за организацию платежа с НДС",
    "acquiring_bank": "Тинькофф",
    "ppvz_vw": 22.25,
    "ppvz_vw_nds": 4.45,
    "ppvz_office_name": "Пункт самовывоза (ПВЗ)",
    "ppvz_office_id": 105383,
    "ppvz_supplier_id": 186465,
    "ppvz_supplier_name": "ИП Жасмин",
    "ppvz_inn": "010101010101",
    "declaration_number": "",
    "bonus_type_name": "Штраф МП. Невыполненный заказ (отмена клиентом после недовоза)",
    "sticker_id": "1964038895",
    "site_country": "Россия",
    "srv_dbs": true,
    "penalty": 231.35,
    "additional_payment": 0,
    "rebill_logistic_cost": 1.349,
    "rebill_logistic_org": "ИП Иванов Иван Иванович(123456789012)",
    "storage_fee": 12647.29,
    "deduction": 6354,
    "acceptance": 865,
    "assembly_id": 2816993144,
    "kiz": "0102900000376311210G2CIS?ehge)S\u001d91002A\u001d92F9Qof4FDo/31Icm14kmtuVYQzLypxm3HWkC1vQ/+pVVjm1dNAth1laFMoAGn7yEMWlTjxIe7lQnJqZ7TRZhlHQ==",
    "srid": "0f1c3999172603062979867564654dac5b702849",
    "report_type": 1,
    "is_legal_entity": false,
    "trbx_id": "WB-TRBX-1234567",
    "installment_cofinancing_amount": 0,
    "wibes_wb_discount_percent": 1,
    "cashback_amount": 0,
    "cashback_discount": 0,
    "cashback_commission_change": 0,
    "order_uid": "id375f16c4bec295d9995393af803ff7b",
    "payment_schedule": 0,
    "delivery_method": "FBS, (МГТ)",
    "seller_promo_id": 14350,
    "seller_promo_discount": 3,
    "loyalty_id": 0,
    "loyalty_discount": 0,
    "uuid_promocode": "",
    "sale_price_promocode_discount_prc": 0,
    "article_substitution": "",
    "sale_price_affiliated_discount_prc": 0,
    "agency_vat": 0,
    "sale_price_wholesale_discount_prc": 0
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
