# POST /content/v2/cards/upload

**Создание карточек товаров{{ /content/v2/cards/upload }}**

теги: `Создание карточек товаров`

**Полный путь:** `POST /content/v2/cards/upload`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод создаёт карточки товаров c указанием описаний и характеристик товаров.<br>

<div class="description_important">
  Есть две формы запроса: для создания отдельных и объединённых карточек товаров
</div>

Габариты товаров можно указать только в `сантиметрах`, вес товара с упаковкой — в `килограммах`.
<br><br>
Создание карточки товара происходит асинхронно. Синхронизация новой карточки с сервисами может занимать до 30 минут. В течение этого времени невозможно добавить остатки на склады и настроить цены. <br>
Одним запросом можно создать максимум 100 отдельных карточек товаров или 100 групп [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров по 30 карточек в каждой. Максимальный размер запроса 10 Мб.<br>
Если ответ `Успешно` (`200`), но какие-то карточки не создались, проверьте [список несозданных карточек товаров](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1error~1list/post).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 10 запросов | 6 сек | 5 запросов |
</div>

## Запрос

### Тело запроса

**Content-Type:** `application/json`

Отдельные карточки товаров или группы объединённых карточек товаров
- array of: object
  - `subjectID` **(required)** — integer. ID предмета
  - `variants` **(required)** — array<object>. [Объединённые](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточки товаров.<br>Чтобы создать отдельную карточку, передайте только один объект
    - *(элементы)*
      - `brand` — string. Бренд
      - `title` — string. Наименование товара
      - `description` — string. Описание товара.<br>
      - `vendorCode` **(required)** — string. Артикул продавца
      - `kizMarked` — boolean. Подтверждение, что на товар нанесён обязательный код маркировки [Честного знака](https://честныйзнак.рф/):
      - `wholesale` — object. Оптовая продажа
      - `dimensions` — object. Габариты и вес товара `c упаковкой`.<br>
      - `sizes` — array<object>. Массив размеров.<br>
      - `characteristics` — array<object>. Характеристики товара.

**Пример «creatingOneCard»:**

```json
[
  {
    "subjectID": 105,
    "variants": [
      {
        "vendorCode": "АртикулПродавца",
        "kizMarked": true,
        "wholesale": {
          "enabled": true,
          "quantum": 211
        },
        "title": "Наименование товара",
        "description": "Описание товара",
        "brand": "Бренд",
        "dimensions": {
          "length": 12,
          "width": 7,
          "height": 5,
          "weightBrutto": 1.242
        },
        "characteristics": [
          {
            "id": 12,
            "value": [
              "Turkish flag"
            ]
          },
          {
            "id": 25471,
            "value": 1200
          },
          {
            "id": 14177449,
            "value": [
              "red"
            ]
          }
        ],
        "sizes": [
          {
            "techSize": "S",
            "wbSize": "42",
            "price": 5000,
            "skus": [
              "88005553535"
            ]
          }
        ]
      }
    ]
  }
]
```

**Пример «creatingMergedCards»:**

```json
[
  {
    "subjectID": 3091,
    "variants": [
      {
        "vendorCode": "АртикулПродавца11",
        "kizMarked": true,
        "wholesale": {
          "enabled": true,
          "quantum": 211
        },
        "title": "Наименование товара 1",
        "description": "Описание товара 1",
        "brand": "Бренд",
        "dimensions": {
          "length": 55,
          "width": 40,
          "height": 15,
          "weightBrutto": 6.24
        },
        "characteristics": [
          {
            "id": 12,
            "value": [
              "Turkish flag"
            ]
          },
          {
            "id": 25471,
            "value": 1200
          },
          {
            "id": 14177449,
            "value": [
              "red"
            ]
          }
        ],
        "sizes": [
          {
            "skus": [
              "111111111133111"
            ]
          }
        ]
      },
      {
        "vendorCode": "АртикулПродавца22",
        "title": "Наименование товара 2",
        "description": "Описание товара 2",
        "brand": "БрендДругой",
        "dimensions": {
          "length": 55,
          "width": 40,
          "height": 15,
          "weightBrutto": 6.241
        },
        "characteristics": [
          {
            "id": 12,
            "value": [
              "Turkish flag"
            ]
          },
          {
            "id": 25471,
            "value": 1200
          },
          {
            "id": 14177449,
            "value": [
              "red"
            ]
          }
        ],
        "sizes": [
          {
            "skus": [
              "111111111441111"
            ]
          }
        ]
      }
    ]
  }
]
```

**Пример «creatingGroupOfIndividualCards»:**

```json
[
  {
    "subjectID": 3091,
    "variants": [
      {
        "vendorCode": "АртикулПродавца1",
        "kizMarked": true,
        "wholesale": {
          "enabled": true,
          "quantum": 211
        },
        "title": "Наименование товара 1",
        "description": "Описание товара 1",
        "brand": "Бренд",
        "dimensions": {
          "length": 55,
          "width": 40,
          "height": 15,
          "weightBrutto": 6
        },
        "characteristics": [
          {
            "id": 12,
            "value": [
              "Turkish flag"
            ]
          },
          {
            "id": 25471,
            "value": 1200
          },
          {
            "id": 14177449,
            "value": [
              "red"
            ]
          }
        ],
        "sizes": [
          {
            "skus": [
              "1111111111111"
            ]
          }
        ]
      }
    ]
  },
  {
    "subjectID": 105,
    "variants": [
      {
        "vendorCode": "Артикул продавца 2",
        "title": "Наименование товара 2",
        "description": "Описание товара 2",
        "brand": "Бренд",
        "dimensions": {
          "length": 14,
          "width": 5,
          "height": 4,
          "weightBrutto": 0.94
        },
        "characteristics": [
          {
            "id": 12,
            "value": [
              "Turkish flag"
            ]
          },
          {
            "id": 25471,
            "value": 1200
          },
          {
            "id": 14177449,
            "value": [
              "red"
            ]
          }
        ],
        "sizes": [
          {
            "techSize": "S",
            "wbSize": "42",
            "price": 5000,
            "skus": [
              "2222222222222"
            ]
          }
        ]
      }
    ]
  }
]
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

*NonUniqueCharacteristicsInOneGroupCreate:*

```json
{
  "data": null,
  "error": true,
  "errorText": "non unique characteristics in one group",
  "additionalErrors": {
    "vendor_code_1": "non unique characteristics in group with ids: {1}, {2}"
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
