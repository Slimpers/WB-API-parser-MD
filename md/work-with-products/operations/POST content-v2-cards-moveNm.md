# POST /content/v2/cards/moveNm

**Объединение и разъединение карточек товаров{{ /content/v2/cards/moveNm }}**

теги: `Карточки товаров`

**Полный путь:** `POST /content/v2/cards/moveNm`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод [объединяет и разъединяет](https://dev.wildberries.ru/knowledge-base/articles/019d49a4-1320-71bb-9dac-8ba07e7177ce/rabota-s-tovarami#obuedinenie-i-razuedinenie-kartochek-tovarov) карточки товаров. Карточки товаров являются объединёнными, если у них одинаковый `imtID`.
<br><br>
Для объединения карточек товаров сделайте запрос **с указанием** `imtID`. Можно объединять не более 30 карточек товаров.<br>
Для разъединения карточек товаров сделайте запрос **без указания** `imtID`. Для разъединенных карточек будут сгенерированы новые `imtID`.
<br><br>
Если вы разъедините одновременно несколько карточек товаров, эти карточки объединятся в одну и получат новый `imtID`.<br>
Чтобы присвоить каждой карточке товара уникальный `imtID`, необходимо передавать по одной карточке товара за запрос.<br>
<br>
Максимальный размер запроса 10 Мб.

<div class="description_important">
  Объединить можно карточки товаров только в рамках одного предмета
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

## Запрос

### Тело запроса

**Content-Type:** `application/json`


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


*responseExceededLimit:*

```json
{
  "data": null,
  "error": true,
  "errorText": "В группу можно объединить не больше 30 карточек. В результате запроса будет превышен лимит",
  "additionalErrors": {
    "error": "В группу можно объединить не больше 30 карточек. В результате запроса будет превышен лимит"
  }
}
```

*responseCombining:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Объединение товаров с разными предметами невозможно",
  "additionalErrors": {
    "error": "Объединение товаров с разными предметами невозможно"
  }
}
```

*responseIncorrectRequestFormat:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Неправильный формат запроса",
  "additionalErrors": {
    "error": "Неправильный формат запроса"
  }
}
```

*responseNonExistentNmId:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Указан несуществующий nmID карточки товара",
  "additionalErrors": {
    "error": "Указан несуществующий nmID карточки товара"
  }
}
```

*responseNonExistentImt:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Указан несуществующий imt",
  "additionalErrors": {
    "error": "Указан несуществующий imt"
  }
}
```

*responseCardCreate1:*

```json
{
  "data": null,
  "error": true,
  "errorText": "string",
  "additionalErrors": {
    "string": "string"
  }
}
```

*responseDuplicateRequests:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Недопустимо отправлять дублирующиеся запросы!",
  "additionalErrors": {
    "error": "Недопустимо отправлять дублирующиеся запросы!"
  }
}
```

*responseAllCardsInSameGroup:*

```json
{
  "data": null,
  "error": true,
  "errorText": "Все карточки находятся в одной группе",
  "additionalErrors": {
    "error": "Все карточки находятся в одной группе"
  }
}
```

*responseIncorrectBeginDate:*

```json
{
  "error": "Некорректная дата начала"
}
```

*responseIncorrectEndDate:*

```json
{
  "error": "Некорректная дата конца"
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

- `data` — object. Данные ответа
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Описание ошибки
- `additionalErrors`. Дополнительные ошибки

#### 413 — Превышен лимит объёма данных в запросе

**Content-Type:** `application/json`

- string

*BodySizeExceedsTheGivenLimit:*

```json
"body size exceeds the given limit"
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
