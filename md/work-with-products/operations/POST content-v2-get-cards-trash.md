# POST /content/v2/get/cards/trash

**Список карточек товаров в корзине{{ /content/v2/get/cards/trash }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/get/cards/trash`

## Описание

<div class='description-title'><span>Описание метода</span></div>

<div class="description_auth">
  Метод доступен по <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токену</a> с категорией <strong>Контент</strong> или <strong>Продвижение</strong>
</div>

Метод возвращает список карточек товаров в корзине.<br><br>

Чтобы получить **больше 100** карточек товаров, используйте пагинацию.
  1. Сделайте первый запрос: <br>
      <pre style="background-color: rgb(38 50 56 / 5%); color: #e53935">
        {
          "settings": {
            "sort": {
              "ascending": true
            },
            "cursor": {
              "limit": 100
            }
          }
        }</pre>
     Чтобы получать только карточки товаров, которые были перенесены в корзину после выгрузки, используйте сортировку по возрастанию: `"sort":{"ascending":true}`.
  2. Скопируйте `"trashedAt":"***","nmID":***` из `cursor` ответа и вставьте в `cursor` запроса.
  3. Повторите запрос.
  4. Повторяйте пункты 2 и 3, пока значение `total` в ответе не станет меньше, чем значение `limit` в запросе. Это будет означать, что вы получили все карточки.

Чтобы получать только карточки товаров, которые были перенесены в корзину после предыдущей выгрузки данных:
  1. Сохраните поля `"cursor":{"trashedAt":"***","nmID":***}` из последнего ответа предыдущей выгрузки. При выгрузке используйте сортировку по возрастанию: `"sort":{"ascending":true}`.
  2. Укажите в первом запросе сохранённые поля `"cursor":{"trashedAt":"***","nmID":"***"}`. Продолжайте использовать сортировку по возрастанию.
  3. Сохраните поля `"cursor":{"trashedAt":"***","nmID":***}` из последнего ответа текущей выгрузки.

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
| `locale` | query | string; enum: ["ru", "en", "zh"] | нет | Язык полей ответа `name`, `value` и `object`:   - `ru` — русский   - `en` — английский   - `zh` — китайский  Не используется в песочнице |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `settings` — object. Настройки
  - `sort` — object. Параметр сортировки
    - `ascending` — boolean. Сортировать по `trashedAt`:
  - `cursor` — object. Пагинатор
    - `limit` — integer. Сколько карточек товаров выдать в ответе
    - `trashedAt` — string. Дата и время помещения в корзину
    - `nmID` — integer. Артикул WB, с которого надо запрашивать следующий список карточек товаров
  - `filter` — object. Параметры фильтрации
    - `textSearch` — string. Поиск по артикулу продавца, артикулу WB, баркоду

**Пример:**

```json
{
  "settings": {
    "sort": {
      "ascending": false
    },
    "filter": {
      "textSearch": "4603743187500888"
    },
    "cursor": {
      "trashedAt": "2023-12-06T11:17:00.96577Z",
      "nmID": 370870300,
      "limit": 11
    }
  }
}
```

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `cards` — array<object>. Массив карточек товаров
  - *(элементы)*
    - `nmID` — integer. Артикул WB
    - `vendorCode` — string. Артикул продавца
    - `kizMarked` — boolean. Есть ли подтверждение от продавца, что обязательный код маркировки [Честного знака](https://честныйзнак.рф/) нанесён на товар:
    - `subjectID` — integer. ID предмета
    - `subjectName` — string. Название предмета
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
    - `sizes` — array<object>. Массив размеров
      - *(элементы)*
        - `chrtID` — integer. ID размера
        - `techSize` — string. Размер товара
        - `wbSize` — string. Российский размер товара
        - `skus` — array<string; пример: `12345Ejf5`>. Массив баркодов
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
    - `createdAt` — string. Date and time the card was created
    - `trashedAt` — string. Дата и время помещения в корзину
- `cursor` — object. Пагинатор
  - `trashedAt` — string. Дата и время, с которых надо запрашивать следующий список карточек товаров
  - `nmID` — integer. Артикул WB, с которого надо запрашивать следующий список карточек товаров
  - `total` — integer. Количество возвращённых карточек товаров

```json
{
  "cards": [
    {
      "nmID": 1234567,
      "vendorCode": "wb5xsy5ftj",
      "kizMarked": true,
      "subjectID": 1436,
      "subjectName": "Ведра хозяйственные",
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
        "quantum": 114
      },
      "sizes": [
        {
          "chrtID": 111111111,
          "techSize": "0",
          "skus": [
            "xxxxxxxxxxxx"
          ]
        }
      ],
      "dimensions": {
        "length": 35,
        "width": 40,
        "height": 15,
        "weightBrutto": 2.9,
        "isValid": false
      },
      "createdAt": "2023-12-05T14:55:09.323462Z",
      "trashedAt": "2023-12-06T10:57:42.193028Z"
    }
  ],
  "cursor": {
    "trashedAt": "2023-12-06T10:57:42.193028Z",
    "nmID": 194128521,
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
