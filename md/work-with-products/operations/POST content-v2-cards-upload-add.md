# POST /content/v2/cards/upload/add

**Создание карточек товаров с присоединением{{ /content/v2/cards/upload/add }}**

теги: `Создание карточек товаров`

**Полный путь:** `POST /content/v2/cards/upload/add`

## Описание

<span>Описание метода</span>

Метод создаёт карточки товаров, присоединяя их к существующим отдельным карточкам и группам [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек. В одной группе объединённых карточек товаров может быть не более 30 карточек, соответственно, создать с присоединением можно не более 29 карточек товаров за один запрос.

Габариты товаров можно указать только в `сантиметрах`, вес товара с упаковкой — в `килограммах`.

Если ответ `Успешно` (`200`), но какие-то карточки не создались, проверьте [список несозданных карточек товаров](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1error~1list/post).

Создание карточки товара происходит асинхронно. Синхронизация новой карточки с сервисами может занимать до 30 минут. В течение этого времени невозможно добавить остатки на склады и настроить цены.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 10 запросов | 6 сек | 5 запросов |
| Сервисный | 1 мин | 10 запросов | 6 сек | 5 запросов |
| Базовый | 2 ч | 1 запрос | 2 ч | 1 запрос |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- `imtID` — integer. `imtID` отдельной карточки товара или группы [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров, к которой присоединяются создаваемые карточки
- `cardsToAdd` — array<object>. Добавляемые карточки товаров
  - *(элементы)*
    - `brand` — string. Бренд
    - `vendorCode` **(required)** — string. Артикул продавца
    - `kizMarked` — boolean. Подтверждение, что на товар нанесён обязательный код маркировки [Честного знака](https://честныйзнак.рф/):
    - `wholesale` — object. Оптовая продажа
      - `enabled` — boolean. Предназначена ли карточка товара для оптовой продажи
      - `quantum` — number (uint64). Количество единиц товара в упаковке
    - `title` — string. Наименование товара
    - `description` — string. Описание товара.
    - `dimensions` — object. Габариты и вес товара `c упаковкой`.
      - `length` — integer. Длина, см
      - `width` — integer. Ширина, см
      - `height` — integer. Высота, см
      - `weightBrutto` — number. Вес, кг
    - `sizes` — array<object>. Массив размеров.
      - *(элементы)*
        - `techSize` — string. Размер товара (например, XL, 45)
        - `wbSize` — string. Российский размер товара
        - `price` — integer. Цена товара
        - `skus` — array<string>. Баркод. Если не указать, сгенерируется автоматически
    - `characteristics` — array<object>. Характеристики товара.
      - *(элементы)*
        - `id` **(required)** — integer. ID характеристики
        - `value` **(required)**. Значения характеристики.

**Пример:**

```json
{
  "imtID": 987654321,
  "cardsToAdd": [
    {
      "vendorCode": "myVariant1",
      "kizMarked": true,
      "wholesale": {
        "enabled": true,
        "quantum": 243
      },
      "title": "Наименование товара",
      "description": "Описание товара",
      "brand": "Бренд",
      "dimensions": {
        "length": 9,
        "width": 6,
        "height": 3,
        "weightBrutto": 0.893
      },
      "characteristics": [
        {
          "id": 12,
          "value": [
            "Russian flag"
          ]
        },
        {
          "id": 25471,
          "value": 1300
        },
        {
          "id": 14177449,
          "value": [
            "blue"
          ]
        }
      ],
      "sizes": [
        {
          "skus": [
            "12345678"
          ]
        }
      ]
    },
    {
      "vendorCode": "myVariant2",
      "title": "Наименование товара",
      "description": "Описание товаров",
      "brand": "Бренд",
      "dimensions": {
        "length": 8,
        "width": 8,
        "height": 8,
        "weightBrutto": 1.04
      },
      "characteristics": [
        {
          "id": 12,
          "value": [
            "Russian flag"
          ]
        },
        {
          "id": 25471,
          "value": 1300
        },
        {
          "id": 14177449,
          "value": [
            "blue"
          ]
        }
      ],
      "sizes": [
        {
          "skus": [
            "222222222222"
          ]
        }
      ]
    }
  ]
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object. Данные ответа
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Описание ошибки
- `additionalErrors`. Дополнительные ошибки

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

*InvalidRequestFormatContent:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Invalid request format",
  "additionalErrors": {}
}
```

*CardCreatedWithoutVendorCode:*

```json
{
  "data": null,
  "error": true,
  "errorText": "A card cannot be created without a vendorCode",
  "additionalErrors": {}
}
```

*CardsVendorCodeUsedInOtherCards:*

```json
{
  "data": null,
  "error": true,
  "errorText": "bad request; Unexpected the specified card's vendor code is used in other cards",
  "additionalErrors": {}
}
```

*ThisCategoryDoesNotExist:*

```json
{
  "data": null,
  "error": true,
  "errorText": "This category does not exist",
  "additionalErrors": {
    "id": "342342"
  }
}
```

*MissingRequiredCharacteristics:*

```json
{
  "data": null,
  "error": true,
  "errorText": "some products lacks required characteristics. please fill them and try again.",
  "additionalErrors": {
    "vendor_code_1": "missing required characteristics with ids: {1}, {2}",
    "vendor_code_2": "missing required characteristics with ids: {1}, {2}"
  }
}
```

*NonUniqueCharacteristicsInOneGroupAdd:*

```json
{
  "data": null,
  "error": true,
  "errorText": "non unique characteristics in one group",
  "additionalErrors": {
    "vendor_code_1": "non unique characteristics in group id: {imt_id} with characteristic ids: {1}, {2}"
  }
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

#### 413 — Превышен лимит объёма данных в запросе

**Content-Type:** `application/json`

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки
- `code` — string. Внутренний код ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB
- `status` — number. HTTP статус-код
- `statusText` — string. Расшифровка HTTP статус-кода

```json
{
  "title": "request body too long",
  "detail": "https://openapi.wildberries.ru/content/api/ru/",
  "code": "71d3de1b-001e-488f-bbf5-55c31254fbeb",
  "requestId": "MN8usr6RfrzWHZfucSvNgb",
  "origin": "s2s-api-auth-content",
  "status": 413,
  "statusText": "Request Entity Too Large"
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
