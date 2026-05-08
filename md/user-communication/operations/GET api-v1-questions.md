# GET /api/v1/questions

**Список вопросов{{ /api/v1/questions }}**

теги: `Вопросы`

**Полный путь:** `GET /api/v1/questions`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает список вопросов по заданным фильтрам. Вы можете:
  - получить данные отвеченных и неотвеченных вопросов
  - сортировать вопросы по дате
  - настроить пагинацию и количество вопросов в ответе

<div class="description_important">
  Можно получить максимум 10 000 вопросов в одном ответе
</div>

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Вопросы и отзывы</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Сервисный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `isAnswered` | query | boolean | да | Есть ли ответ на вопрос:   - `true` — да   - `false` — нет |
| `nmId` | query | integer | нет | Артикул WB |
| `take` | query | integer | да | Количество запрашиваемых вопросов (максимально допустимое значение для параметра - 10 000, при этом сумма значений параметров `take` и `skip` не должна превышать 10 000) |
| `skip` | query | integer | да | Количество вопросов для пропуска (максимально допустимое значение для параметра - 10 000, при этом сумма значений параметров `take` и `skip` не должна превышать 10 000) |
| `order` | query | string | нет | Сортировка вопросов по дате (`dateAsc`/`dateDesc`) |
| `dateFrom` | query | integer; пример: `1688465092` | нет | Дата начала периода в формате Unix timestamp |
| `dateTo` | query | integer; пример: `1688465092` | нет | Дата конца периода в формате Unix timestamp |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `countUnanswered` — integer. Количество неотвеченных вопросов
  - `countArchive` — integer. Количество отвеченных вопросов
  - `questions` — array<object>. Вопросы
    - *(элементы)*
      - `id` — string. id вопроса
      - `text` — string. Текст вопроса
      - `createdDate` — string (date-time). Дата и время создания вопроса
      - `state` — string. Статус вопроса:
      - `answer` — object. Структура ответа
      - `productDetails` — object. Информация о товаре
      - `wasViewed` — boolean. Просмотрен ли вопрос
      - `isWarned` — boolean. Признак подозрительного вопроса.<br>
- `error` — boolean; пример: `False`. Есть ли ошибка
- `errorText` — string; пример: ``. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки

```json
{
  "data": {
    "countUnanswered": 24,
    "countArchive": 508,
    "questions": [
      {
        "id": "2ncBtX4B9I0UHoornoqG",
        "text": "Question text",
        "createdDate": "2022-02-01T11:18:08.769513469Z",
        "state": "suppliersPortalSynch",
        "answer": null,
        "productDetails": {
          "imtId": 11157265,
          "nmId": 14917842,
          "productName": "Coffee",
          "supplierArticle": "123401",
          "supplierName": " ГП Реклама и услуги",
          "brandName": "Nescafe"
        },
        "wasViewed": false,
        "isWarned": false
      }
    ]
  },
  "error": false,
  "errorText": "",
  "additionalErrors": null
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*FeedbackErr400:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Something went wrong",
  "additionalErrors": null,
  "requestId": "734c9ea8-39e5-45c9-8cad-f03c13f733e9"
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

#### 403 — Доступ запрещён

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*FeedbackErr403:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Ошибка авторизации",
  "additionalErrors": null,
  "requestId": "734c9ea8-39e5-45c9-8cad-f03c13f733e9"
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
