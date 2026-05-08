# GET /content/v2/object/charcs/{subjectId}

**Характеристики предмета{{ /content/v2/object/charcs/{subjectId} }}**

теги: `Категории, предметы и характеристики`

**Полный путь:** `GET /content/v2/object/charcs/{subjectId}`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает параметры характеристик предмета: названия, типы данных, единицы измерения и так далее. В запросе необходимо указать ID [предмета](./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1object~1all/get).

<div class="description_important">
  Для получения значений характеристик <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1colors/get">Цвет</a>, <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1kinds/get">Пол</a>, <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1countries/get">Страна производства</a>, <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1seasons/get">Сезон</a>, <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1vat/get">Ставка НДС</a> и <a href="./work-with-products#tag/Kategorii-predmety-i-harakteristiki/paths/~1content~1v2~1directory~1tnved/get">ТНВЭД-код</a> используйте отдельные методы
</div>

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
| `subjectId` | path | integer; пример: `105` | да | ID предмета |
| `locale` | query | string; пример: `en` | нет | Язык полей ответа `subjectName` и `name`:   - `ru` — русский   - `en` — английский   - `zh` — китайский  Не используется в песочнице |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — array<object>. Данные
  - *(элементы)*
    - `charcID` — integer. ID характеристики
    - `subjectName` — string. Название предмета
    - `subjectID` — integer. ID предмета
    - `name` — string. Название характеристики
    - `required` — boolean. - `true` — характеристику необходимо обязательно указать в карточке товара
    - `unitName` — string. Единица измерения
    - `maxCount` — integer. Максимальное количество значений, которое можно присвоить характеристике при [создании](./work-with-products#tag/Sozdanie-kartochek-tovarov) или [редактировании](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1update/post) карточек товаров.
    - `popular` — boolean. Характеристика популярна у пользователей (true - да, false - нет)
    - `charcType` — integer. Тип данных характеристики, который необходимо использовать при [создании](./work-with-products#tag/Sozdanie-kartochek-tovarov) или [редактировании](./work-with-products#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1update/post) карточек товаров:
    - `hasFilter` — boolean. Ключевая характеристика. Является ли характеристика значимой для покупателей:
    - `isVariable` — boolean. Признак меняющейся характеристики. Значение размечает характеристики, по которым варианты отличаются друг от друга:
    - `existNamedField` — boolean. Как передать характеристику в запросах на [cоздание](./work-with-products#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload/post), [создание с присоединением](./work-with-products/#tag/Sozdanie-kartochek-tovarov/paths/~1content~1v2~1cards~1upload~1add/post) и [редактирование](./work-with-products/#tag/Kartochki-tovarov/paths/~1content~1v2~1cards~1update/post) карточек товара:
- `error` — boolean. Флаг наличия ошибки
- `errorText` — string. Текст ошибки
- `additionalErrors` — string. Дополнительные ошибки

```json
{
  "data": [
    {
      "charcID": 54337,
      "subjectName": "Кроссовки",
      "subjectID": 105,
      "name": "Размер",
      "required": false,
      "unitName": "см",
      "maxCount": 0,
      "popular": false,
      "charcType": 4,
      "hasFilter": true,
      "isVariable": true,
      "existNamedField": true
    }
  ],
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
