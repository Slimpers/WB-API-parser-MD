# GET /api/v1/calendar/promotions

**Список акций{{ /api/v1/calendar/promotions }}**

теги: `Календарь акций`

**Полный путь:** `GET /api/v1/calendar/promotions`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список [акций](./promotion#tag/Kalendar-akcij/paths/~1api~1v1~1calendar~1promotions~1details/get) в WB с датами и временем проведения.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Календарь акций</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Сервисный | 6 сек | 10 запросов | 600 мс | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - `promotions` — array<object>. Список акций
    - *(элементы)*
      - `id` — integer; пример: `123`. ID акции
      - `name` — string; пример: `скидки`. Название акции
      - `startDateTime` — string (date-time); пример: `2023-06-05T21:00:00Z`. Начало акции
      - `endDateTime` — string (date-time); пример: `2023-06-05T21:00:00Z`. Конец акции
      - `type` — string; enum: ["regular", "auto"]. Тип акции:

```json
{
  "data": {
    "promotions": [
      {
        "id": 123,
        "name": "скидки",
        "startDateTime": "2023-06-05T21:00:00Z",
        "endDateTime": "2023-06-05T21:00:00Z",
        "type": "regular"
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
