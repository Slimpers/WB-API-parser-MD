# POST /api/marketplace/v3/dbw/orders/client

**Информация о покупателе{{ /api/marketplace/v3/dbw/orders/client }}**

теги: `Сборочные задания DBW`

**Полный путь:** `POST /api/marketplace/v3/dbw/orders/client`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о покупателях по ID сборочных заданий.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для следующих методов DBW:
<ul>
    <li>получение и обновление списка контактов</li>
    <li>получение и удаление метаданных</li>
    <li>методы сборочных заданий</li>
</ul> 

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 300 запросов | 200 мс | 20 запросов |

Один запрос с кодом ответа <code>409</code> учитывается как 10 запросов
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `orders` — array<integer>. Список ID сборочных заданий

**Пример:**

```json
{
  "orders": [
    987654321,
    123456789
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<$ref: ClientInfo>. Информация о покупателях

```json
{
  "orders": [
    {
      "replacementPhone": "79871234567",
      "phone": "+79871234567",
      "firstName": "Иван",
      "fullName": "Иванов Иван Иванович",
      "additionalPhones": [
        "1234554321"
      ],
      "additionalPhoneCodes": [
        12345
      ],
      "orderId": 1345678910,
      "phoneCode": 0
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

*IncorrectRequest:*

```json
{
  "code": "IncorrectRequest",
  "message": ""
}
```

*IncorrectRequestBody:*

```json
{
  "code": "IncorrectRequestBody",
  "message": ""
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

#### 403

**Content-Type:** `application/json`

- `code` — string. Код ошибки
- `message` — string. Описание ошибки
- `data` — object. Дополнительные данные ошибки
  - *(пустой object)*

```json
{
  "code": "AccessDenied",
  "message": ""
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
