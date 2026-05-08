# GET /api/v1/feedback

**Получить отзыв по ID{{ /api/v1/feedback }}**

теги: `Отзывы`

**Полный путь:** `GET /api/v1/feedback`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает данные [отзыва](./user-communication#tag/Otzyvy/paths/~1api~1v1~1feedbacks/get) по его ID.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца для всех методов категории <strong>Вопросы и отзывы</strong>:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Сервисный | 1 сек | 3 запроса | 333 мс | 6 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `id` | query | string; пример: `G7Y9Y1kBAtKOitoBT_lV` | да | ID отзыва |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - `id` — string. ID отзыва
  - `text` — string. Текст отзыва
  - `pros` — string. Достоинства товара
  - `cons` — string. Недостатки товара
  - `matchingSize` — string. Соответствие заявленного размера реальному.
  - `productValuation` — integer. Оценка товара
  - `createdDate` — string (date-time). Дата и время создания отзыва
  - `answer` — object. Структура ответа
    - `text` — string. Текст ответа
    - `state` — string. Статус:
    - `editable` — boolean. Можно ли отредактировать ответ:
  - `state` — string. Статус отзыва:
  - `productDetails` — object. Product information
    - `nmId` — integer. Артикул WB
    - `imtId` — integer. ID для [объединённых](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточек товаров
    - `productName` — string. Название товара
    - `supplierArticle` — string. Артикул продавца
    - `supplierName` — string. Имя продавца
    - `brandName` — string. Бренд товара
    - `size` — string. Размер товара (`techSize` в КТ)
  - `photoLinks` — array<object>. Массив структур фотографий
    - *(элементы)*
      - `fullSize` — string. Адрес фотографии полного размера
      - `miniSize` — string. Адрес фотографии маленького размера
  - `userName` — string. Имя автора отзыва
  - `orderStatus` — string. Статус заказа.
  - `video` — object. Структура видео
    - `previewImage` — string. Ссылка на обложку видео
    - `link` — string. Ссылка на файл плейлиста видео (доступно по протоколу hls)
    - `durationSec` — integer. Общая продолжительность видео
  - `wasViewed` — boolean. Просмотрен ли отзыв
  - `isAbleSupplierFeedbackValuation` — boolean. Доступна ли продавцу возможность оставить жалобу на отзыв:
  - `supplierFeedbackValuation` — integer. Ключ причины жалобы на отзыв
  - `isAbleSupplierProductValuation` — boolean. Доступна ли продавцу возможность сообщить о проблеме с товаром  (`true` - доступна, `false` - не доступна)
  - `supplierProductValuation` — integer. Ключ проблемы с товаром
  - `isAbleReturnProductOrders` — boolean. Опция возврата товара:
  - `returnProductOrdersDate` — string. Дата и время, когда на запрос возврата был получен ответ со статус-кодом 200.
  - `bables` — array<string>. Список тегов покупателя
  - `lastOrderShkId` — integer. Штрихкод единицы товара
  - `lastOrderCreatedAt` — string. Дата покупки
  - `color` — string. Цвет товара
  - `subjectId` — integer. ID предмета
  - `subjectName` — string. Название предмета
  - `parentFeedbackId` — string. ID начального отзыва (`null`, если этот отзыв начальный)
  - `childFeedbackId` — string. ID дополненного отзыва (`null`, если этот отзыв дополненный)
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки

```json
{
  "data": {
    "id": "YX52RZEBhH9mrcYdEJuD",
    "text": "Спасибо, всё подошло",
    "pros": "Удобный",
    "cons": "Нет",
    "productValuation": 5,
    "createdDate": "2024-09-26T10:20:48+03:00",
    "answer": {
      "text": "Пожалуйста. Ждём вас снова!",
      "state": "wbRu",
      "editable": false
    },
    "state": "wbRu",
    "productDetails": {
      "imtId": 123456789,
      "nmId": 987654321,
      "productName": "ВАЗ",
      "supplierArticle": "DP02/черный",
      "supplierName": "ГП Реклама и услуги",
      "brandName": "Бест Трикотаж",
      "size": "0"
    },
    "video": {
      "previewImage": "https://videofeedback01.wbbasket.ru/8defc853-7f62-4d6d-b236-8a16cfb63128/preview.webp",
      "link": "https://videofeedback01.wbbasket.ru/8defc853-7f62-4d6d-b236-8a16cfb63128/index.m3u8",
      "durationSec": 10
    },
    "wasViewed": true,
    "photoLinks": [
      {
        "fullSize": "https://feedback04.wbbasket.ru/vol1333/part133337/123456789/photos/fs.webp",
        "miniSize": "https://feedback04.wbbasket.ru/vol1333/part133337/123456789/photos/ms.webp"
      },
      {
        "fullSize": "https://feedback04.wbbasket.ru/vol1508/part150887/123456789/photos/fs.webp",
        "miniSize": "https://feedback04.wbbasket.ru/vol1508/part150887/123456789/photos/ms.webp"
      },
      {
        "fullSize": "https://feedback04.wbbasket.ru/vol1486/part148682/123456789/photos/fs.webp",
        "miniSize": "https://feedback04.wbbasket.ru/vol1486/part148682/123456789/photos/ms.webp"
      }
    ],
    "userName": "Николай",
    "orderStatus": "returned",
    "matchingSize": "ok",
    "isAbleSupplierFeedbackValuation": false,
    "supplierFeedbackValuation": 1,
    "isAbleSupplierProductValuation": false,
    "supplierProductValuation": 2,
    "isAbleReturnProductOrders": false,
    "returnProductOrdersDate": "2024-08-20T16:39:49Z",
    "bables": [
      "цена"
    ],
    "lastOrderShkId": 123456789,
    "lastOrderCreatedAt": "2024-08-12T10:20:48+03:00",
    "color": "colorless",
    "subjectId": 219,
    "subjectName": "Футболки-поло",
    "parentFeedbackId": null,
    "childFeedbackId": "bIjTCZDvJni7NGnLbUlf"
  },
  "error": false,
  "errorText": "",
  "additionalErrors": null
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

#### 422 — Ошибка обработки параметров запроса

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Есть ли ошибка
- `errorText` — string. Описание ошибки
- `additionalErrors` — array<string>. Дополнительные ошибки
- `requestId` — string

*ResponseGetFeedbackByIdErrEx:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Невозможно получить отзыв по id",
  "additionalErrors": null,
  "requestId": "87a2fe4d-d28b-4bae-b824-c0f498c72702"
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
