# POST /content/v2/cards/delete/trash

**Перенос карточек товаров в корзину{{ /content/v2/cards/delete/trash }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/cards/delete/trash`

## Описание

<span>Описание метода</span>

Метод переносит [карточки товаров в корзину](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1get~1cards~1trash/post). При этом карточки товаров не удаляются, их можно [восстановить](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1recover/post).

  После переноса в корзину карточке товара присваивается новый <code>imtID</code> — ID для <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov">объединённых</a> карточек товаров

Карточки товаров удаляются автоматически, если лежат в корзине больше 30 дней, и на них нет остатков. Очистка корзины происходит каждую ночь по московскому времени.

Карточки товаров можно удалить в любое время в [личном кабинете](https://seller.wildberries.ru/new-goods/basket-cards).

Карточка будет продаваться, пока по ней есть остатки на складе, даже если её переместили в корзину. Чтобы полностью снять карточку с продажи, обнулите остатки.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 3 запроса | 20 сек | 5 запросов |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `nmIDs` — array<integer>. Артикулы WB

**Пример:**

```json
{
  "nmIDs": [
    123456789,
    987654321
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Описание ошибки
- `additionalErrors` — object. Дополнительные ошибки
  - *(пустой object)*

```json
{
  "data": null,
  "error": false,
  "errorText": "",
  "additionalErrors": {}
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки
- `additionalErrors` — object. Дополнительные ошибки
  - *(пустой object)*

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

- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки
- `additionalErrors` — string. Дополнительные ошибки

```json
{
  "data": null,
  "error": true,
  "errorText": "Access denied",
  "additionalErrors": "Access denied"
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
