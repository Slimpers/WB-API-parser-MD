# GET /api/v1/claims

**Заявки покупателей на возврат{{ /api/v1/claims }}**

теги: `Возвраты покупателями`

**Полный путь:** `GET /api/v1/claims`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает заявки покупателей на возврат товаров за последние 14 дней. Вы можете [отвечать на эти заявки](./user-communication#tag/Vozvraty-pokupatelyami/paths/~1api~1v1~1claim/patch).

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 20 запросов | 3 сек | 10 запросов |
| Сервисный | 1 мин | 20 запросов | 3 сек | 10 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |
| `` |  |  | нет |  |

## Ответы


#### 200

**Content-Type:** `application/json`

- `claims` — array<object>. Заявки
  - *(элементы)*
    - `id` — string (UUID). ID заявки
    - `claim_type` — integer. Источник заявки:
    - `status` — integer. Решение по возврату покупателю:
    - `status_ex` — integer. Статус товара:
    - `nm_id` — integer. Артикул WB
    - `user_comment` — string. Комментарий покупателя
    - `wb_comment` — string. Ответ покупателю
    - `dt` — string. Дата и время оформления заявки покупателем. UTC+3
    - `imt_name` — string. Название товара
    - `order_dt` — string. Дата и время заказа
    - `dt_update` — string. Дата и время рассмотрения заявки. Для нерассмотренной заявки — дата и время оформления. UTC+3
    - `photos` — array<string (WEBP)>. Фотографии из заявки покупателя
    - `video_paths` — array<string (MP4)>. Видео из заявки покупателя
    - `actions` — array<string>. Варианты [ответа продавца на заявку](./user-communication#tag/Vozvraty-pokupatelyami/paths/~1api~1v1~1claim/patch).<br>Отклонённые заявки можно пересмотреть. Если массив пуст, с заявкой работать нельзя.
    - `price` — number. Фактическая цена с учетом всех скидок. Взимается с покупателя
    - `currency_code` — string. Код валюты цены
    - `srid` — string. Уникальный ID заказа, по товару которого создана заявка
    - `origin_id_info` — string. Результат сверки [IMEI](https://seller.wildberries.ru/instructions/ru/ru/material/items-labeling-in-fbs#imei) для возврата через ПВЗ Wildberries.<br>Значение показывает, совпадает ли IMEI, который был указан продавцом или отсканирован при приёмке на складе Wildberries, с IMEI из заявки покупателя, что позволяет эффективнее [обрабатывать заявки](./user-communication#tag/Vozvraty-pokupatelyami/paths/~1api~1v1~1claim/patch).<br>Применимо только для товаров **Apple** предмета `Смартфоны` (`"subjectId":515`) с ценой от 40000 рублей, учитывая скидку продавца ([только](./work-with-products#tag/Ceny-i-skidki/paths/~1api~1v2~1upload~1task/post) параметры и поля `price` и `discount`)
    - `delivery_dt` — string. Дата и время получения заказа покупателем
- `total` — integer. Количество заявок, соответствующих параметрам запроса. Без учёта `limit` и `offset`

```json
{
  "claims": [
    {
      "id": "fe3e9337-e9f9-423c-8930-946a8ebef80",
      "claim_type": 1,
      "status": 2,
      "status_ex": 8,
      "nm_id": 196320101,
      "user_comment": "Длина провода не соответствует описанию",
      "wb_comment": "Продавец одобрил вашу заявку. Для возврата средств необходимо вернуть товар продавцу. Укажите дату, когда вам удобно принять курьера.",
      "dt": "2025-03-26T17:06:12.245611",
      "imt_name": "Кабель 0.5 м, 3797",
      "order_dt": "2024-10-27T05:18:56",
      "dt_update": "2025-05-10T18:01:06.999613",
      "photos": [
        "//photos.wbstatic.net/claim/fe3e9337-e9f9-423c-8930-946a8ebef80/1.webp",
        "//photos.wbstatic.net/claim/fe3e9337-e9f9-423c-8930-946a8ebef80/2.webp"
      ],
      "video_paths": [
        "//video.wbstatic.net/claim/fe3e9337-e9f9-423c-8930-946a8ebef80/1.mp4"
      ],
      "actions": [
        "autorefund1",
        "approve1"
      ],
      "price": 157,
      "currency_code": "643",
      "srid": "v5o_7143225816503318733.0.0",
      "origin_id_info": "IMEI 359889346153011, указанный покупателем в  заявке на возврат, не совпадает с IMEI 359889346238986, указанным продавцом или отсканированным на складе Wildberries",
      "delivery_dt": "2025-04-09T14:36:07"
    }
  ],
  "total": 31
}
```

#### 400

**Content-Type:** `application/problem+json`

- `title` — string; пример: `Invalid query params`. ID ошибки
- `detail` — string; пример: `Failed to deserialize query string: missing field `is_archive``. Описание ошибки
- `requestId` — string; пример: `e0aedc10-9789-49c1-9a83-d8422b4703dc`. ID запроса

```json
{
  "title": "Invalid query params",
  "detail": "Failed to deserialize query string: missing field `is_archive`",
  "requestId": "e0aedc10-9789-49c1-9a83-d8422b4703dc"
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
