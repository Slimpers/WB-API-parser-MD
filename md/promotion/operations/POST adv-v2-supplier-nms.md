# POST /adv/v2/supplier/nms

**Карточки товаров для кампаний{{ /adv/v2/supplier/nms }}**

теги: `Создание кампаний`

**Полный путь:** `POST /adv/v2/supplier/nms`

## Описание

<span>Описание метода</span>

Метод возвращает список [карточек товаров](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1get~1cards~1list/post), которые можно добавить в рекламную [кампанию](./promotion#tag/Kampanii/paths/~1api~1advert~1v2~1adverts/get). Для получения карточек необходимы ID [предметов](./promotion#tag/Sozdanie-kampanij/paths/~1adv~1v1~1supplier~1subjects/get), также доступных для добавления в кампанию.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 5 запросов | 12 сек | 5 запросов |
| Сервисный | 1 мин | 5 запросов | 12 сек | 5 запросов |
| Базовый | 1 ч | 2 запроса | 30 мин | 1 запрос |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
ID предметов, для которых нужно получить карточки товаров

**Content-Type:** `application/json`

- array of: integer

**Пример:**

```json
[
  123,
  456,
  765,
  321
]
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

Карточки товаров для кампаний
- array of: object
  - `title` — string; пример: `Плед`. Название товара
  - `nm` — integer; пример: `146168367`. Артикул WB
  - `subjectId` — integer; пример: `765`. ID предмета

```json
[
  {
    "title": "Плед",
    "nm": 146168367,
    "subjectId": 765
  }
]
```

#### 400 — Неправильный запрос

**Content-Type:** `text/plain`

- string

```json
"Ошибка обработки тела запроса"
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
