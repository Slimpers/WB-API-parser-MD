# POST /api/v3/dbw/orders/delivery-date

**Дата и время доставки{{ /api/v3/dbw/orders/delivery-date }}**

теги: `Сборочные задания DBW`

**Полный путь:** `POST /api/v3/dbw/orders/delivery-date`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о выбранных покупателем дате и времени доставки сборочных заданий.
<br>

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
    1234567890
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `orders` — array<object>
  - *(элементы)*
    - `dTimeFrom` — string; пример: `11:11`. Актуальное время доставки "с"
    - `dTimeTo` — string; пример: `22:22`. Актуальное время доставки "по"
    - `dTimeFromOld` — string; пример: `12:30`. Прежнее время доставки "с". Доступно первые сутки после изменения
    - `dTimeToOld` — string; пример: `22:30`. Прежнее время доставки "по". Доступно первые сутки после изменения
    - `dDateOld` — string; пример: `2025-01-28`. Прежняя дата доставки. Доступна первые сутки после изменения
    - `dDate` — string; пример: `2025-02-20`. Актуальная дата доставки
    - `id` — integer; пример: `1234567890`. ID сборочного задания

```json
{
  "orders": [
    {
      "dTimeFrom": "11:11",
      "dTimeTo": "22:22",
      "dTimeFromOld": "12:30",
      "dTimeToOld": "22:30",
      "dDateOld": "2025-01-28",
      "dDate": "2025-02-20",
      "id": 1234567890
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
