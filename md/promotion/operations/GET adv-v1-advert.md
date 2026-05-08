# GET /adv/v1/advert

**Информация о медиакампании{{ /adv/v1/advert }}**

теги: `Медиа`

**Полный путь:** `GET /adv/v1/advert`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о кампании [WB Медиа](https://cmp.wildberries.ru/cmpf/list). Вместо карточек товаров в медиакампаниях продвигаются рекламные баннеры продавца на сайте и в приложении WB.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Сервисный | 1 сек | 10 запросов | 100 мс | 10 запросов |
| Базовый | 1 ч | 5 запросов | 12 мин | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `id` | query | integer; пример: `23569` | да | ID медиакампании |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `advertId` — integer. ID медиакампании
- `name` — string. Название медиакампании
- `brand` — string. Название бренда
- `type` — integer. Тип медиакампании:
- `status` — integer. Статус медиакампании:
- `createTime` — string (date-time). Время создания медиакампании
- `extended` — object
  - `reason` — string. Комментарий модератора
  - `expenses` — integer. Затраты
  - `from` — string (date-time). Дата и время начала показа медиакампании
  - `to` — string (date-time). Дата и время окончания показа медиакампании
  - `updated_at` — string (date-time). Дата и время изменения кампании
  - `price` — integer. Стоимость размещения по дням для типа `1`
  - `budget` — integer. Остаток бюджета для типа `2`
  - `operation` — integer. Источник списания:
  - `contract_id` — integer. ID контракта, для продавцов на контракте
- `items` — array<object>. Информация о баннере.
  - *(элементы)*
    - `id` — integer. ID баннера
    - `name` — string. Бренд
    - `status` — integer. Статус (такой же как у медиакампании)
    - `place` — integer. Позиция на странице размещения
    - `budget` — integer. Бюджет
    - `daily_limit` — integer. Дневной лимит (для баннеров по показам)
    - `category_name` — string. Название категории размещения
    - `cpm` — integer. Ставка
    - `url` — string. URL страницы, на которую попадает пользователь при клике по баннеру
    - `advert_type` — integer. Тип продвижения:
    - `created_at` — string (date-time). Дата создания баннера
    - `updated_at` — string (date-time). Дата и время обновления баннера
    - `date_from` — string (date-time). Дата начала работы баннера
    - `date_to` — string (date-time). Дата завершения работы баннера
    - `nms` — array<integer>. Подборка артикулов WB
    - `bottomText1` — string. Текст под плашкой баннера
    - `bottomText2` — string. 2-я строка с текстом под плашкой баннера
    - `message` — string. Текст push-уведомления или рассылки
    - `additionalSettings` — integer. Дополнительные настройки.
    - `receiversCount` — integer. Кол-во получателей push-уведомлений
    - `subject_id` — integer. ID родительской категории товара
    - `subject_name` — string. Название родительской категории товара
    - `action_name` — string. Название акции
    - `show_hours` — array<object>. Часы показа
      - *(элементы)*
        - `From` — integer. Начало показа
        - `To` — integer. Конец показа
    - `Erid` — string. Уникальный ID медиакампании для работы с ОРД

```json
{
  "advertId": 23569,
  "name": "Реклама денег принеси",
  "brand": "Plank",
  "type": 2,
  "status": 11,
  "createTime": "2023-07-19T11:13:41.195138+03:00",
  "extended": {
    "reason": "Для возобновления показов пополните бюджет медиакампании",
    "expenses": 10000,
    "from": "2023-07-19T12:05:35.847348Z",
    "to": "2123-07-20T08:14:13.079176+03:00",
    "updated_at": "2023-07-21T13:25:31.129766+03:00",
    "price": 0,
    "budget": 0,
    "operation": 1,
    "contract_id": 0
  },
  "items": [
    {
      "id": 68080,
      "name": "Унисон",
      "status": 7,
      "place": 2,
      "budget": 650000,
      "daily_limit": 500,
      "category_name": "Главная",
      "cpm": 351,
      "url": "https://www.wildberries.ru/promotions/ssylka-na-akciyou",
      "advert_type": 1,
      "created_at": "2023-11-01T15:40:46.86165+03:00",
      "updated_at": "2023-11-08T23:44:33.248229+03:00",
      "date_from": "2023-11-01T16:05:22.286002Z",
      "date_to": "2023-11-09T17:27:32.745869+03:00",
      "nms": [
        123456,
        11111111
      ],
      "bottomText1": "string",
      "bottomText2": "string",
      "message": "string",
      "additionalSettings": 1,
      "receiversCount": 1,
      "subject_id": 6945,
      "subject_name": "Бельё",
      "action_name": "Распродажа! Создай себе домашний уют!",
      "show_hours": [
        {
          "From": 7,
          "To": 8
        }
      ],
      "Erid": "string"
    }
  ]
}
```

#### 204 — Медиакампания не найдена


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
