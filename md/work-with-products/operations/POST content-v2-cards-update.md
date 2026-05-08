# POST /content/v2/cards/update

**Редактирование карточек товаров{{ /content/v2/cards/update }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/cards/update`

## Описание

<span>Описание метода</span>

Метод обновляет данные карточек товаров. Также используйте его, чтобы добавлять новые размеры.

  Карточка товара перезаписывается при обновлении. Поэтому в запросе нужно передать в том числе те параметры карточки, которые вы не собираетесь обновлять. Их значения можно получить в <a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1get~1cards~1list/post">списке карточек товаров</a> и <a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1get~1cards~1trash/post">списке карточек товаров в корзине</a>.

С помощью этого метода нельзя обновлять или удалять:
  - баркоды размеров товара. Можно только добавить дополнительные баркоды
  - параметры `photos`, `video` и `tags`
  - цены товаров. Цену можно задать, только если вы добавляете новые размеры

При добавлении нового размера укажите его цену через параметр `price`. Если в запросе не указан `price`, цена размера будет `0` — в этом случае изменить её можно будет с помощью методов:
  - [Установить цены и скидки](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task/post), если у [товара](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1list~1goods~1filter/get) `"editablePriceSize":false`
  - [Установить цены для размеров](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task~1size/post), если у [товара](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1list~1goods~1filter/get) `"editablePriceSize":true`

Габариты товаров можно указать только в `сантиметрах`, вес товара с упаковкой — в `килограммах`.

Одним запросом можно отредактировать максимум 3000 карточек товаров (`nmID`). Максимальный размер запроса 10 Мб.

Если ответ `Успешно` (`200`), но какие-то карточки не обновились, проверьте [список несозданных карточек товаров](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1error~1list/post).

Синхронизация данных с сервисами может занимать до 30 минут. В течение этого времени невозможно добавить остатки на склады и настроить цены.

<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:

| Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- |
| 1 мин | 10 запросов | 6 сек | 5 запросов |

## Запрос

### Тело запроса

**Content-Type:** `application/json`

- array of: object
  - `nmID` **(required)** — integer. Артикул WB
  - `vendorCode` **(required)** — string. Артикул продавца
  - `kizMarked` — boolean. Подтверждение, что на товар нанесён обязательный код маркировки [Честного знака](https://честныйзнак.рф/):
  - `brand` — string. Бренд
  - `title` — string. Наименование товара
  - `description` — string. Описание товара
  - `dimensions` — object. Габариты и вес товара `c упаковкой`.
    - `length` — integer. Длина, см
    - `width` — integer. Ширина, см
    - `height` — integer. Высота, см
    - `weightBrutto` — number. Вес, кг
  - `characteristics` — array<object>. Характеристики товара.
    - *(элементы)*
      - `id` **(required)** — integer. ID характеристики
      - `value` **(required)**. Значения характеристики.
  - `sizes` **(required)** — array<object>. Массив размеров
    - *(элементы)*
      - `chrtID` — integer. ID размера для данного артикула WB
      - `techSize` — string. Размер товара (например, XL, S, 45)
      - `wbSize` — string. Российский размер товара
      - `price` — integer. Цена товара, ₽
      - `skus` — array<string>. Баркоды

**Пример:**

```json
[
  {
    "nmID": 11111111,
    "vendorCode": "wbiz72wmro",
    "kizMarked": true,
    "brand": "",
    "title": "Свитер женский оверсайз с горлом",
    "description": "12345",
    "dimensions": {
      "length": 35,
      "width": 40,
      "height": 15,
      "weightBrutto": 3
    },
    "characteristics": [
      {
        "id": 14177450,
        "value": [
          "хлопок 50% акрил 50%"
        ]
      },
      {
        "id": 50,
        "value": [
          "свободный крой"
        ]
      }
    ],
    "sizes": [
      {
        "chrtID": 12345678,
        "techSize": "ONE SIZE",
        "wbSize": "78-90",
        "skus": [
          "123487653460134"
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
