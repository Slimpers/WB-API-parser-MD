# GET /api/v1/analytics/banned-products/blocked

**Заблокированные карточки{{ /api/v1/analytics/banned-products/blocked }}**

теги: `Скрытые товары`

**Полный путь:** `GET /api/v1/analytics/banned-products/blocked`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список [заблокированных карточек товаров продавца](https://seller.wildberries.ru/analytics-reports/banned-products) с причинами блокировки.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 10 сек | 1 запрос | 10 сек | 6 запросов |
| Сервисный | 10 сек | 1 запрос | 10 сек | 6 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `sort` | query | string; enum: ["brand", "nmId", "title", "vendorCode", "reason"]; пример: `nmId` | да | Сортировка - `brand` — по бренду - `nmId` — по артикулу WB - `title` — по наименованию товара - `vendorCode` — по артикулу продавца - `reason` — по причине блокировки |
| `order` | query | string; enum: ["desc", "asc"]; пример: `asc` | да | Порядок выдачи - `desc` — от наибольшего числового значения к наименьшему, от последнего по алфавиту значения к первому - `asc` — от наименьшего числового значения к наибольшему, от первого по алфавиту значения к последнему |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `report` — array<object>. Отчёт
  - *(элементы)*
    - `brand` — string; пример: `Тест22`. Бренд
    - `nmId` — integer; пример: `82722944`. Артикул WB
    - `title` — string; пример: `Гуминовые кислоты - биоактивный противовирусный комплекс на`. Наименование товара
    - `vendorCode` — string; пример: `пкdeир76`. Артикул продавца
    - `reason` — string; пример: `Контактные данные Продавца и ссылки на иные сайты/группы/сообщества на фотографиях Товара`. Причина блокировки

```json
{
  "report": [
    {
      "brand": "Тест22",
      "nmId": 82722944,
      "title": "Гуминовые кислоты - биоактивный противовирусный комплекс на",
      "vendorCode": "пкdeир76",
      "reason": "Контактные данные Продавца и ссылки на иные сайты/группы/сообщества на фотографиях Товара"
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `status` — number. HTTP статус-код
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB

```json
{
  "title": "bad request",
  "status": 400,
  "detail": "missing sort",
  "requestId": "94b52fca-8403-49fb-85dd-95dfb73160ad",
  "origin": "banreportsvc-api"
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
