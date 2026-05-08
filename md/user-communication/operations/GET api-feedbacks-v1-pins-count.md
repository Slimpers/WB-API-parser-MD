# GET /api/feedbacks/v1/pins/count

**Количество закреплённых и откреплённых отзывов{{ /api/feedbacks/v1/pins/count }}**

теги: `Закреплённые отзывы`

**Полный путь:** `GET /api/feedbacks/v1/pins/count`

## Описание

<span>Описание метода</span>

Метод возвращает количество закреплённых и откреплённых отзывов за заданный период.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Вопросы и отзывы</strong>:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Сервисный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `state` | query | string; enum: ["pinned", "unpinned"]; пример: `pinned` | нет | Закреплён ли отзыв:   - `pinned` — да   - `unpinned` — нет |
| `pinOn` | query | string; enum: ["nm", "imt"]; пример: `nm` | нет | Место закрепления отзыва:   - `nm` — карточка товара   - `imt` — группа [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров |
| `imtId` | query | integer; пример: `256971531` | нет | ID для [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров. Един для всех артикулов WB группы объединённых карточек. У каждой карточки товара есть `imtId`, даже если она не объединена с другими карточками |
| `nmId` | query | integer; пример: `177974151` | нет | Артикул WB |
| `feedbackId` | query | integer; пример: `789` | нет | ID отзыва |
| `dateFrom` | query | string (date-time); пример: `2020-01-01T15:04:05Z` | нет | Дата закрепления первого отзыва в списке |
| `dateTo` | query | string (date-time); пример: `2020-02-01T15:04:05Z` | нет | Дата закрепления последнего отзыва в списке |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`


#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` — string. Детали ошибки
- `origin` **(required)** — string. ID внутреннего сервиса WB
- `requestId` **(required)** — string. ID запроса
- `status` **(required)** — integer. HTTP статус-код
- `title` **(required)** — string. Заголовок ошибки

```json
{
  "status": 400,
  "title": "Bad Request",
  "detail": "state must be one of the values 'pinned', 'unpinned'",
  "requestId": "7b64у8ffc3523450d613723fwу61873e",
  "origin": "pin-open-api"
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
