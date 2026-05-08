# POST /content/v2/cards/error/list

**Список несозданных карточек товаров с ошибками{{ /content/v2/cards/error/list }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/cards/error/list`

## Описание

<span>Описание метода</span>

Метод возвращает список карточек товаров ([черновиков](https://seller.wildberries.ru/new-goods/error-cards)), при создании или редактировании которых произошли ошибки, с описанием этих ошибок.

Данные в ответе возвращаются пакетами `batch`. Один пакет содержит:
  - все ошибки по одному массиву `variants` одного запроса при [создании](./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload/post) карточек товаров
  - все ошибки одного запроса при [создании с присоединением](./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload~1add/post) или [редактировании](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1update/post) карточек товаров

Чтобы получить более 100 пакетов, используйте пагинацию:
  1. Сделайте первый запрос:

        {
          "cursor": {
            "limit": 100
          },
          "order": {
            "ascending": true
          }
        }
  2. Скопируйте `"updatedAt":"***","batchUUID":"***" `из `cursor` ответа и вставьте в `cursor` запроса.
  3. Повторите запрос.
  4. Повторяйте пункты 2 и 3, пока не получите в ответе `"next":false`. Это будет означать, что вы получили все пакеты.

  Чтобы удалить карточку товара из списка, сделайте ещё один запрос на создание, создание с присоединением или редактирование карточки товара с исправленными ошибками

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 10 запросов | 6 сек | 5 запросов |

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `locale` | query | string; пример: `en` | нет | Язык названий предметов:   - `ru` — русский   - `en` — английский   - `zh` — китайский |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `cursor` — $ref: swagger.PublicErrorsCursorInput
- `order` — $ref: swagger.PublicErrorsOrderV2

**Пример:**

```json
{
  "cursor": {
    "limit": 31,
    "updatedAt": "2025-08-05T17:54:40+08:00",
    "batchUUID": "bca3744c-1c8b-4588-b345-62af3b2899ae"
  },
  "order": {
    "ascending": true
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` **(required)** — $ref: models.ErrorTableListPublicRespV2
- `error` **(required)** — boolean. Флаг ошибки
- `errorText` **(required)** — string. Описание ошибки
- `additionalErrors` **(required)** — object. Дополнительные ошибки
  - *(пустой object)*

```json
{
  "data": {
    "items": [
      {
        "batchUUID": "b15fecaf-57fd-4b63-ab6f-18d630b8793e",
        "subjects": {
          "wb15j2kjk9": {
            "id": 8827,
            "name": "Автомобили с пробегом"
          },
          "wb3g6advyh": {
            "id": 8827,
            "name": "Автомобили с пробегом"
          },
          "wb3g7xx8g9": {
            "id": 8827,
            "name": "Автомобили с пробегом"
          },
          "wb4uphjn61": {
            "id": 8827,
            "name": "Автомобили с пробегом"
          },
          "wb64nayozt": {
            "id": 8827,
            "name": "Автомобили с пробегом"
          }
        },
        "brands": {},
        "vendorCodes": [
          "wb64nayozt",
          "wb15j2kjk9",
          "wb3g7xx8g9",
          "wb3g6advyh",
          "wb4uphjn61"
        ],
        "errors": {
          "wb15j2kjk9": [
            "Поле Наименование не должно содержать запрещенные символы: 😈 😊 🤨"
          ],
          "wb3g6advyh": [
            "Поле Наименование не должно содержать запрещенные символы: 😊 🤨 😈"
          ],
          "wb3g7xx8g9": [
            "Поле Наименование не должно содержать запрещенные символы: 🤯"
          ],
          "wb4uphjn61": [
            "Поле Наименование не должно содержать запрещенные символы: 😊 🤨 😈"
          ],
          "wb64nayozt": [
            "Поле Наименование не должно содержать запрещенные символы: 😈 😊 🤨"
          ]
        },
        "updatedAt": "2025-12-19T23:59:59Z"
      },
      {
        "batchUUID": "30aa42ec-fb49-45ec-86d5-ddf9911e7e3f",
        "subjects": {
          "test_pasha1": {
            "id": 184,
            "name": "Рубашки"
          }
        },
        "brands": {},
        "vendorCodes": [
          "test_pasha1"
        ],
        "errors": {
          "test_pasha1": [
            "Запрещено использовать E-Mail в поле Наименование",
            "Запрещено использовать E-Mail в поле Описание"
          ]
        },
        "updatedAt": "2025-12-20T23:59:59Z"
      }
    ],
    "cursor": {
      "next": true,
      "updatedAt": "2025-12-20T23:59:59Z",
      "batchUUID": "1cd79751-de1f-46c8-a444-a941d35dde56"
    }
  },
  "error": false,
  "errorText": "",
  "additionalErrors": null
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
