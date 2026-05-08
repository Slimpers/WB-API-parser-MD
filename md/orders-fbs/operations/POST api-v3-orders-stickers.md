# POST /api/v3/orders/stickers

**Получить стикеры сборочных заданий{{ /api/v3/orders/stickers }}**

теги: `Сборочные задания FBS`

**Полный путь:** `POST /api/v3/orders/stickers`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список стикеров для [сборочных заданий](./orders-fbs#tag/Sborochnye-zadaniya-FBS).

Можно получить стикер в форматах:
  - SVG
  - ZPLV (вертикальный)
  - ZPLH (горизонтальный)
  - PNG

Ограничения:
  - За один запрос можно получить максимум 100 стикеров.
  - Стикеры можно получить только для сборочных заданий в [статусах](./orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1orders~1status/post) `confirm` — на сборке и `complete` — в доставке.

Доступны размеры:
  - 580x400 px при `width=58&height=40` в запросе
  - 400x300 px при `width=40&height=30` в запросе

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для методов <strong>сборочных заданий, поставок и пропусков FBS</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `type` | query | string; enum: ["svg", "zplv", "zplh", "png"] | да | Тип стикера |
| `width` | query | integer; enum: [58, 40] | да | Ширина стикера |
| `height` | query | integer; enum: [40, 30] | да | Высота стикера |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `orders` — array<integer (int64); пример: `5346346`>. Список ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    5346346
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `stickers` — array<object>
  - *(элементы)*
    - `orderId` — integer (int64); пример: `5346346`. ID сборочного задания
    - `partA` — string; пример: `231648`. Первая часть ID стикера для печати подписи
    - `partB` — string; пример: `9753`. Вторая часть ID стикера для печати подписи
    - `barcode` — string; пример: `!uKEtQZVx`. Закодированное значение стикера
    - `file` — string (byte); пример: `iVBORw0KGgoAAAANSUhEUgAAASIAAAEiAQAAAAB1xeIbAAABiElEQVR4nO2YUW6DMAyGbUDaI0g9wI4Sjg5H2Q3IeyZPthNKV03tNiVdtf9/cFvXAvRhkh+z0G2t3R1FRKgqAokikCgCiSKQeDQJzho8yXMsmfmh1/UvqoKoNrsLdgN6S8hzXP2TV8Xc47KMyTPnx+DvX/1zVg1Xmch1z9ih6gv2HLZTuqIPXjX7ftSlPRLJ+prXnONLF9hXZL96q/fE4W1Q+O8XvQ/29djL/lvWiTg/Bt89Voeqn/j7OQ4eTLJY7tz8oEoVSFC28aN9JqKwqbX3kP+VBewrsg/KedE3qmXUn3IMYF/d3zONm38TiqckFKeyEaDv6/W96Nus9b2tPrbw2LOAvq/Pfpfn/Fb4HoA1p9UcU3SHJTLHExk+p8VeK3JwN0Q2UNPmR9+3m2OyDzPjoOFFML9vOMcUin0iHahR2CaGz/mkmo6P5zHtQdD3TeeY5NY++/sKZ+xQdUliNZszqePRkFd+tfvHqhtC1S/nmOQh7eH+Y3WoygKJIpAoAokikChqT+IDIkbb8/8OLskAAAAASUVORK5CYII=`. Полное представление стикера в заданном формате (кодировка base64)

```json
{
  "stickers": [
    {
      "orderId": 5346346,
      "partA": "231648",
      "partB": "9753",
      "barcode": "!uKEtQZVx",
      "file": "iVBORw0KGgoAAAANSUhEUgAAASIAAAEiAQAAAAB1xeIbAAABiElEQVR4nO2YUW6DMAyGbUDaI0g9wI4Sjg5H2Q3IeyZPthNKV03tNiVdtf9/cFvXAvRhkh+z0G2t3R1FRKgqAokikCgCiSKQeDQJzho8yXMsmfmh1/UvqoKoNrsLdgN6S8hzXP2TV8Xc47KMyTPnx+DvX/1zVg1Xmch1z9ih6gv2HLZTuqIPXjX7ftSlPRLJ+prXnONLF9hXZL96q/fE4W1Q+O8XvQ/29djL/lvWiTg/Bt89Voeqn/j7OQ4eTLJY7tz8oEoVSFC28aN9JqKwqbX3kP+VBewrsg/KedE3qmXUn3IMYF/d3zONm38TiqckFKeyEaDv6/W96Nus9b2tPrbw2LOAvq/Pfpfn/Fb4HoA1p9UcU3SHJTLHExk+p8VeK3JwN0Q2UNPmR9+3m2OyDzPjoOFFML9vOMcUin0iHahR2CaGz/mkmo6P5zHtQdD3TeeY5NY++/sKZ+xQdUliNZszqePRkFd+tfvHqhtC1S/nmOQh7eH+Y3WoygKJIpAoAokikChqT+IDIkbb8/8OLskAAAAASUVORK5CYII="
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

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": "Некорректное тело запроса"
}
```

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": "Переданы некорректные данные"
}
```

*IncorrectParameter:*

```json
{
  "code": "IncorrectParameter",
  "message": "Передан некорректный параметр"
}
```

#### 401

**Content-Type:** `application/json`

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
  "message": "Доступ запрещён"
}
```

#### 429

**Content-Type:** `application/json`

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
