# GET /api/v1/paid_storage/tasks/{task_id}/download

**Получить отчёт{{ /api/v1/paid_storage/tasks/{task_id}/download }}**

теги: `Платное хранение`

**Полный путь:** `GET /api/v1/paid_storage/tasks/{task_id}/download`

## Описание

<span>Описание метода</span>

Метод возвращает отчёт о [платном хранении](https://seller.wildberries.ru/analytics-reports/paid-storage/storage) по ID [задания на генерацию](./reports#tag/Platnoe-hranenie/paths/~1api~1v1~1paid_storage/get).

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Сервисный | 1 мин | 1 запрос | 1 мин | 1 запрос |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `task_id` | path | string; пример: `06e06887-9d9f-491f-b16a-bb1766fcb8d2` | да | ID задания на генерацию |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- array of: object
  - `date` — string. Дата, за которую был расчёт или перерасчёт
  - `logWarehouseCoef` — number. Коэффициент логистики и хранения
  - `officeId` — integer. ID склада
  - `warehouse` — string. Название склада
  - `warehouseCoef` — number. Коэффициент склада
  - `giId` — integer. ID поставки
  - `chrtId` — integer. ID размера для этого артикула WB
  - `size` — string. Размер (`techSize` в карточке товара)
  - `barcode` — string. Баркод
  - `subject` — string. Предмет
  - `brand` — string. Бренд
  - `vendorCode` — string. Артикул продавца
  - `nmId` — integer. Артикул WB
  - `volume` — number. Объём товара
  - `calcType` — string. Способ расчёта
  - `warehousePrice` — number. Сумма хранения
  - `barcodesCount` — integer. Количество единиц товара (штук), подлежащих тарифицированию за расчётные сутки
  - `palletPlaceCode` — integer. Код паллетоместа
  - `palletCount` — number. Количество паллет
  - `originalDate` — string. Если был перерасчёт, это дата первоначального расчёта. Если перерасчёта не было, совпадает с `date`
  - `loyaltyDiscount` — number. Скидка программы лояльности, ₽
  - `tariffFixDate` — string. Дата фиксации тарифа
  - `tariffLowerDate` — string. Дата понижения тарифа

```json
[
  {
    "date": "2023-10-01",
    "logWarehouseCoef": 1,
    "officeId": 507,
    "warehouse": "Коледино",
    "warehouseCoef": 1.7,
    "giId": 123456,
    "chrtId": 1234567,
    "size": "0",
    "barcode": "",
    "subject": "Маски одноразовые",
    "brand": "1000 Каталог",
    "vendorCode": "567383",
    "nmId": 1234567,
    "volume": 12,
    "calcType": "короба: без габаритов",
    "warehousePrice": 7.65,
    "barcodesCount": 1,
    "palletPlaceCode": 0,
    "palletCount": 0,
    "originalDate": "2023-03-01",
    "loyaltyDiscount": 10,
    "tariffFixDate": "2023-10-01",
    "tariffLowerDate": "2023-11-01"
  }
]
```

#### 204 — Нет данных


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "Invalid format for parameter task_id: error unmarshaling '7b8875---9f03-46f1-af21-b9b4b22fe821' text as *uuid.UUID: invalid UUID format",
  "origin": "api-statistics",
  "requestId": "44bac63ab29c46cb2d49392e6604c1a0",
  "title": "Bad Request"
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

**Content-Type:** `application/problem+json`

- `detail` — string. Детали ошибки
- `origin` — string. ID внутреннего сервиса WB
- `requestId` — string. Уникальный ID запроса
- `title` — string. Заголовок ошибки

```json
{
  "detail": "not found",
  "origin": "api-statistics",
  "requestId": "c777731fc180f215a49c9896c2f1200d",
  "title": "Not Found"
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
