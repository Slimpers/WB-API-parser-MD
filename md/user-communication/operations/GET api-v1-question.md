# GET /api/v1/question

**Получить вопрос по ID{{ /api/v1/question }}**

теги: `Вопросы`

**Полный путь:** `GET /api/v1/question`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает данные [вопроса](./user-communication#tag/Voprosy/paths/~1api~1v1~1questions/get) по его ID. Далее вы можете [работать с этим вопросом](./user-communication#tag/Voprosy/paths/~1api~1v1~1questions/patch).

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
| `id` | query | string; пример: `ljAVapEBL38RyMdRln61` | да | ID вопроса |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `id` — string. ID вопроса
  - `text` — string. Текст вопроса
  - `createdDate` — string (date-time). Дата и время создания вопроса
  - `state` — string. Статус вопроса:
  - `answer` — object. Ответ
    - `text` — string. Текст ответа
    - `editable` — boolean. Можно ли отредактировать ответ (`false` - нельзя, `true` - можно)
    - `createDate` — string (date-time). Дата и время создания ответа
  - `productDetails` — object. Product information
    - `nmId` — integer. Артикул WB
    - `imtId` — integer. ID для [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров
    - `productName` — string. Название товара
    - `supplierArticle` — string. Артикул продавца
    - `supplierName` — string. Имя продавца
    - `brandName` — string. Название бренда
  - `wasViewed` — boolean. Просмотрен ли вопрос
  - `isWarned` — boolean. Признак подозрительного вопроса.<br>
- `error` — boolean; пример: `False`. Есть ли ошибка
- `errorText` — string; пример: ``. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки

```json
{
  "data": {
    "id": "TfWOp5QBfEYrrd0AMJau",
    "text": "Хороший карандаш? Когда еще поставите?",
    "createdDate": "2025-01-27T11:38:21.202143857Z",
    "state": "wbRu",
    "answer": {
      "text": "На следующей неделе",
      "editable": true,
      "createDate": "2025-07-28T08:24:37.187113704Z"
    },
    "productDetails": {
      "imtId": 202306781,
      "nmId": 224747484,
      "productName": "Карандаш с ластиком",
      "supplierArticle": "12113156uw",
      "supplierName": "",
      "brandName": "Brand"
    },
    "wasViewed": true,
    "isWarned": false
  },
  "error": false,
  "errorText": "",
  "additionalErrors": null
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

#### 422 — Ошибка обработки параметров запроса

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*responseGetQuestionByIdErrEx:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Невозможно получить вопрос по id",
  "additionalErrors": null,
  "requestId": "87a2fe4d-d28b-4bae-b824-c0f498c72702"
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
