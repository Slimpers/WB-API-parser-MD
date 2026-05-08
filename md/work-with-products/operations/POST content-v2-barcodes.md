# POST /content/v2/barcodes

**Генерация баркодов{{ /content/v2/barcodes }}**

теги: `Создание карточек товаров`

**Полный путь:** `POST /content/v2/barcodes`

## Описание

<span>Описание метода</span>

Метод генерирует массив уникальных баркодов для создания размера в [карточке товара](./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload/post). Можно использовать, если у вас нет собственных баркодов.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Контент</strong>:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 100 запросов | 600 мс | 5 запросов |

Исключение — методы:

<ul>
    <li><a href="./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload/post">создания карточек товаров</a></li>
    <li><a href="./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload~1add/post">создания карточек товаров с присоединением</a></li>
    <li><a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1update/post">редактирования карточек товаров</a></li>
    <li><a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1error~1list/post">получения несозданных карточек товаров с ошибками</a></li>
    <li><a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1delete~1trash/post">переноса карточек товаров в корзину</a></li>
    <li><a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1recover/post">восстановления карточек товаров из корзины</a></li>
</ul>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `count` — integer; пример: `100`. Кол-во баркодов которые надо сгенерировать, максимальное доступное количество баркодов для генерации - `5 000`

**Пример:**

```json
{
  "count": 100
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — array<string; пример: `5032781145187`>. Массив сгенерированных баркодов
- `error` — boolean; пример: `False`. Флаг ошибки
- `errorText` — string; пример: ``. Описание ошибки
- `additionalErrors` — string; пример: ``. Дополнительные ошибки

```json
{
  "data": [
    "5032781145187"
  ],
  "error": false,
  "errorText": "",
  "additionalErrors": ""
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
