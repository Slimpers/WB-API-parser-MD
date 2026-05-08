# GET /api/v1/calendar/promotions/details

**Детальная информация об акциях{{ /api/v1/calendar/promotions/details }}**

теги: `Календарь акций`

**Полный путь:** `GET /api/v1/calendar/promotions/details`

## Описание

<span>Описание метода</span>

Метод возвращает подробную информацию об [акции](./promotion#tag/Kalendar-akcij/paths/~1api~1v1~1calendar~1promotions~1details/get) по ID.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Календарь акций</strong>:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Сервисный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - `promotions` — array<object>. Список акций
    - *(элементы)*
      - `id` — integer; пример: `123`. ID акции
      - `name` — string; пример: `ХИТЫ ГОДА`. Название акции
      - `description` — string; пример: `В акции принимают участие самые популярные товары 2023 года. Карточки товаров будут выделены плашкой «ХИТ ГОДА», чтобы покупатели замечали эти товары среди других. Также они будут размещены под баннерами на главной странице и примут участие в PUSH-уведомлениях. С ценами для вступления в акцию вы можете ознакомиться ниже.`. Описание акции
      - `advantages` — array<string>. Преимущества акции
      - `startDateTime` — string; пример: `2023-06-05T21:00:00Z`. Начало акции
      - `endDateTime` — string; пример: `2023-06-05T21:00:00Z`. Конец акции
      - `inPromoActionLeftovers` — integer; пример: `45`. Количество товаров с остатками, участвующих в акции
      - `inPromoActionTotal` — integer; пример: `123`. Общее количество товаров, участвующих в акции
      - `notInPromoActionLeftovers` — integer; пример: `3`. Количество товаров с остатками, не участвующих в акции
      - `notInPromoActionTotal` — integer; пример: `10`. Общее количество товаров, не участвующих в акции
      - `participationPercentage` — integer; пример: `10`. Уже участвующие в акции товары, %. Рассчитывается по товарам в акции и с остатком
      - `type` — string; enum: ["regular", "auto"]; пример: `auto`. Тип акции:
      - `exceptionProductsCount` — integer (uint); пример: `10`. Количество товаров, исключенных из автоакции до её старта. Только при `"type": "auto"`.
      - `ranging` — array<object>. Ранжирование (если подключено)

```json
{
  "data": {
    "promotions": [
      {
        "id": 123,
        "name": "ХИТЫ ГОДА",
        "description": "В акции принимают участие самые популярные товары 2023 года. Карточки товаров будут выделены плашкой «ХИТ ГОДА», чтобы покупатели замечали эти товары среди других. Также они будут размещены под баннерами на главной странице и примут участие в PUSH-уведомлениях. С ценами для вступления в акцию вы можете ознакомиться ниже.",
        "advantages": [
          "Плашка",
          "Баннер",
          "Топ выдачи товаров"
        ],
        "startDateTime": "2023-06-05T21:00:00Z",
        "endDateTime": "2023-06-05T21:00:00Z",
        "inPromoActionLeftovers": 45,
        "inPromoActionTotal": 123,
        "notInPromoActionLeftovers": 3,
        "notInPromoActionTotal": 10,
        "participationPercentage": 10,
        "type": "auto",
        "exceptionProductsCount": 10,
        "ranging": [
          {
            "condition": "productsInPromotion",
            "participationRate": 10,
            "boost": 7
          },
          {
            "condition": "calculateProducts",
            "participationRate": 20,
            "boost": 17
          },
          {
            "condition": "allProducts",
            "participationRate": 35,
            "boost": 30
          }
        ]
      }
    ]
  }
}
```

#### 400

**Content-Type:** `application/json`

- `errorText` — string; пример: `Failed to parse data`. Текст ошибки

```json
{
  "errorText": "Failed to parse data"
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
