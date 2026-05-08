# PATCH /adv/v0/auction/nms

**Изменение списка карточек товаров в кампаниях{{ /adv/v0/auction/nms }}**

теги: `Управление кампаниями`

**Полный путь:** `PATCH /adv/v0/auction/nms`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод добавляет и удаляет карточки товаров в кампаниях.
<br><br>
Для кампаний в статусах `4`, `9` и `11`.
<br><br>
Для добавляемых товаров устанавливается текущая минимальная ставка.

 <div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 1 запрос | 1 сек | 1 запрос |
| Сервисный | 1 сек | 1 запрос | 1 сек | 1 запрос |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `nms` **(required)** — array<object>. Карточки товаров в кампаниях
  - *(элементы)*
    - `advert_id` **(required)** — integer (int64). ID кампании
    - `nms` **(required)** — object. Карточки товаров. Максимум 50 товаров для одной кампании
      - `add`. Карточки товаров, которые необходимо добавить
      - `delete` — array<integer>. Карточки товаров, которые необходимо удалить

**Пример:**

```json
{
  "nms": [
    {
      "advert_id": 12345,
      "nms": {
        "add": [
          11111111,
          44444444
        ],
        "delete": [
          55555555
        ]
      }
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `nms` **(required)** — array<object>. Результат отработки запроса
  - *(элементы)*
    - `advert_id` **(required)** — integer (int64). ID кампании
    - `nms` **(required)** — object. Карточки товаров
      - `added` **(required)** — array<integer>. Добавленные карточки товаров
      - `deleted` **(required)** — array<integer>. Удалённые карточки товаров

```json
{
  "nms": [
    {
      "advert_id": 12345,
      "nms": {
        "added": [
          11111111,
          44444444
        ],
        "deleted": [
          55555555
        ]
      }
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `6023d2950af564838f9b44a279d2140c`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `invalid payload`. Заголовок ошибки

```json
{
  "detail": "nomenclature 13335157 cannot be both added and deleted for advert 27247695",
  "origin": "camp-api-public-cache",
  "request_id": "6023d2950af564838f9b44a279d2140c",
  "status": 400,
  "title": "invalid payload"
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
