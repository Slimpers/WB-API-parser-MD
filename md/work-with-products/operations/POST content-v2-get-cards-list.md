# POST /content/v2/get/cards/list

**Список карточек товаров{{ /content/v2/get/cards/list }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/get/cards/list`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_auth">
  Метод доступен по <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токену</a> с категорией <strong>Контент</strong> или <strong>Продвижение</strong>
</div>

Метод возвращает список созданных карточек товаров.

<div class="description_important">
  В ответе метода не будет карточек, находящихся в корзине. Получить такие карточки можно через <a href="./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1get~1cards~1trash/post">отдельный метод</a>
</div>

Чтобы получить **больше 100** карточек товаров, используйте пагинацию:
  1. Сделайте первый запрос: <br>
      <pre style="background-color: rgb(38 50 56 / 5%); color: #e53935">
        {
          "settings": {
            "sort": {
              "ascending": true
            },
            "cursor": {
              "limit": 100
            },
            "filter": {
              "withPhoto": -1
            }
          }
        }</pre>
     Чтобы после выгрузки получать только новые или обновлённые карточки товаров, используйте сортировку по возрастанию: `"sort":{"ascending":true}`.
  2. Скопируйте `"updatedAt":"***","nmID":"***"` из `cursor` ответа и вставьте в `cursor` запроса.
  3. Повторите запрос.
  4. Повторяйте пункты 2 и 3, пока значение `total` в ответе не станет меньше, чем значение `limit` в запросе. Это будет означать, что вы получили все карточки.

Чтобы получать только карточки товаров, которые были созданы или обновлены после предыдущей выгрузки данных:
  1. Сохраните поля `"cursor":{"updatedAt":"***","nmID":"***"}` из последнего ответа предыдущей выгрузки. При выгрузке используйте сортировку по возрастанию: `"sort":{"ascending":true}`.
  2. Укажите в первом запросе сохранённые поля `"cursor":{"updatedAt":"***","nmID":"***"}`. Продолжайте использовать сортировку по возрастанию.
  3. Сохраните поля `"cursor":{"updatedAt":"***","nmID":"***"}` из последнего ответа текущей выгрузки.

<div class="description_limit">
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
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `locale` | query | string; пример: `ru` | нет | Язык полей ответа `name`, `value` и `object`:   - `ru` — русский   - `en` — английский   - `zh` — китайский  Не используется в песочнице |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `settings` — object. Настройки
  - `sort` — object. Параметр сортировки
    - `ascending` — boolean. Сортировать по полю `updatedAt`:
  - `filter` — object. Параметры фильтрации
    - `withPhoto` — integer. Фильтр по фото:
    - `textSearch` — string. Поиск по артикулу продавца, артикулу WB, баркоду
    - `tagIDs` — array<integer>. Поиск по ID ярлыков
    - `allowedCategoriesOnly` — boolean. Фильтр по категории:
    - `objectIDs` — array<integer>. Поиск по id предметов
    - `brands` — array<string>. Поиск по брендам
    - `imtID` — integer. Поиск по [ID для объединённых карточек товаров](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov)
  - `cursor` — object. Курсор
    - `limit` — integer. Сколько карточек товаров выдать в ответе
    - `updatedAt` — string. Дата и время изменения
    - `nmID` — integer. Артикул WB, с которого надо запрашивать следующий список карточек товаров

**Пример:**

```json
{
  "settings": {
    "sort": {
      "ascending": false
    },
    "filter": {
      "textSearch": "4603743187500888",
      "allowedCategoriesOnly": true,
      "tagIDs": [
        345,
        415
      ],
      "objectIDs": [
        235,
        67
      ],
      "brands": [
        "уллу",
        "EkkE"
      ],
      "imtID": 328632,
      "withPhoto": -1
    },
    "cursor": {
      "updatedAt": "2023-12-06T11:17:00.96577Z",
      "nmID": 370870300,
      "limit": 11
    }
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `cards` — array<object>. Список карточек товаров
  - *(элементы)*
    - `nmID` — integer. Артикул WB
    - `imtID` — integer. ID для [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров.<br>Един для всех артикулов WB группы объединённых карточек.<br>У каждой карточки товара есть `imtID`, даже если она не объединена с другими карточками<br>
    - `nmUUID` — string (UUID). Внутренний технический ID карточки товара
    - `subjectID` — integer. ID предмета
    - `subjectName` — string. Название предмета
    - `vendorCode` — string. Артикул продавца
    - `brand` — string. Бренд
    - `title` — string. Наименование товара
    - `description` — string. Описание товара
    - `needKiz` — boolean. Требуется ли код маркировки [Честного знака](https://честныйзнак.рф/) для этого товара:
    - `kizMarked` — boolean. Есть ли подтверждение от продавца, что обязательный код маркировки [Честного знака](https://честныйзнак.рф/) нанесён на товар:
    - `photos` — array<object>. Массив фото
      - *(элементы)*
        - `big` — string. URL фото `900x1200`
        - `c246x328` — string. URL фото `248x328`
        - `c516x688` — string. URL фото `516x688`
        - `square` — string. URL фото `600x600`
        - `tm` — string. URL фото `75x100`
    - `video` — string. URL видео
    - `wholesale` — object. Оптовая продажа
      - `enabled` — boolean. Предназначена ли карточка товара для оптовой продажи
      - `quantum` — number (uint64). Количество единиц товара в упаковке
    - `dimensions` — object. Габариты и вес товара c упаковкой, см и кг
      - `length` — integer. Длина, см
      - `width` — integer. Ширина, см
      - `height` — integer. Высота, см
      - `weightBrutto` — number. Вес, кг<br>Количество знаков после запятой <=3
      - `isValid` — boolean. Потенциальная некорректность габаритов товара:
    - `characteristics` — array<object>. Характеристики
      - *(элементы)*
        - `id` — integer. ID характеристики
        - `name` — string. Название характеристики
        - `value`. Значение характеристики. Тип значения зависит от типа характеристики
    - `sizes` — array<object>. Размеры товара
      - *(элементы)*
        - `chrtID` — integer. Числовой ID размера для данного артикула WB
        - `techSize` — string. Размер товара (А, XXL, 57 и др.)
        - `wbSize` — string. Российский размер товара
        - `skus` — array<string; пример: `12345Ejf5`>. Баркод товара
    - `tags` — array<object>. Ярлыки
      - *(элементы)*
        - `id` — integer. ID ярлыка
        - `name` — string. Название ярлыка
        - `color` — string. Цвет ярлыка. <br>
    - `createdAt` — string. Дата и время создания
    - `updatedAt` — string. Дата и время изменения
- `cursor` — object. Пагинатор
  - `updatedAt` — string. Дата и время, с которых надо запрашивать следующий список карточек товаров
  - `nmID` — integer. Артикул WB, с которого надо запрашивать следующий список карточек товаров
  - `total` — integer. Количество возвращённых карточек товаров

```json
{
  "cards": [
    {
      "nmID": 12345678,
      "imtID": 123654789,
      "nmUUID": "01bda0b1-5c0b-736c-b2be-d0a6543e9be",
      "subjectID": 7771,
      "subjectName": "AKF системы",
      "vendorCode": "wb7f6mumjr1",
      "kizMarked": true,
      "brand": "Тест",
      "title": "Тест-система",
      "description": "Тестовое описание",
      "needKiz": false,
      "photos": [
        {
          "big": "https://basket-10.wbbasket.ru/vol1592/part159206/159206280/images/big/1.webp",
          "c246x328": "https://basket-10.wbbasket.ru/vol1592/part159206/159206280/images/c246x328/1.webp",
          "c516x688": "https://basket-10.wbbasket.ru/vol1592/part159206/159206280/images/c516x688/1.webp",
          "square": "https://basket-10.wbbasket.ru/vol1592/part159206/159206280/images/square/1.webp",
          "tm": "https://basket-10.wbbasket.ru/vol1592/part159206/159206280/images/tm/1.webp"
        }
      ],
      "video": "https://videonme-basket-12.wbbasket.ru/vol137/part22557/225577433/hls/1440p/index.m3u8",
      "wholesale": {
        "enabled": true,
        "quantum": 112
      },
      "dimensions": {
        "length": 55,
        "width": 40,
        "height": 15,
        "weightBrutto": 6.24,
        "isValid": false
      },
      "characteristics": [
        {
          "id": 14177449,
          "name": "Цвет",
          "value": [
            "красно-сиреневый"
          ]
        }
      ],
      "sizes": [
        {
          "chrtID": 316399238,
          "techSize": "0",
          "skus": [
            "987456321654"
          ]
        }
      ],
      "tags": [
        {
          "id": 592569,
          "name": "Популярный",
          "color": "D1CFD7"
        }
      ],
      "createdAt": "2023-12-06T11:17:00.96577Z",
      "updatedAt": "2023-12-06T11:17:00.96577Z"
    }
  ],
  "cursor": {
    "updatedAt": "2023-12-06T11:17:00.96577Z",
    "nmID": 123654123,
    "total": 1
  }
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
**Content-Type:** `plain/text`


```json
"Request body can not be decoded"
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
