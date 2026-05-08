# POST /content/v3/media/file

**Загрузить медиафайл{{ /content/v3/media/file }}**

теги: `Медиафайлы`

**Полный путь:** `POST /content/v3/media/file`

## Описание

<span>Описание метода</span>

Метод загружает и добавляет один медиафайл к карточке товара.

Требования к изображениям:
  * максимум изображений для одной карточки товара — 30
  * минимальное разрешение — 700x900 px
  * максимальный размер — 32 Мб
  * минимальное качество — 65%
  * форматы — JPG, PNG, BMP, GIF (статичные), WebP

Требования к видео:
  * максимум одно видео для одной карточки товара
  * максимальный размер — 50 Мб
  * форматы — MOV, MP4

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

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `X-Nm-Id` | header | string; пример: `213864079` | да | Артикул WB |
| `X-Photo-Number` | header | integer; пример: `2` | да | Номер медиафайла на загрузку, начинается с `1`. При загрузке видео всегда указывайте `1`.  Чтобы добавить изображение к уже загруженным, номер медиафайла должен быть больше количества уже загруженных медиафайлов. |

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `multipart/form-data`

- `uploadfile` — string (binary)

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `data` — object
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Описание ошибки
- `additionalErrors` — object. Дополнительные ошибки
  - *(пустой object)*

```json
{
  "data": {},
  "error": false,
  "errorText": "",
  "additionalErrors": null
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `additionalErrors` — object. Дополнительные ошибки
  - *(пустой object)*
- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

```json
{
  "additionalErrors": null,
  "data": null,
  "error": true,
  "errorText": "Error text"
}
```
**Content-Type:** `plain/text`


```json
"Invalid 'boundary' for 'multipart/form-data' request"
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

- `additionalErrors` — object. Дополнительные ошибки
  - *(пустой object)*
- `data` — object. Данные ошибки
  - *(пустой object)*
- `error` — boolean. Флаг ошибки
- `errorText` — string. Текст ошибки

```json
{
  "additionalErrors": null,
  "data": null,
  "error": true,
  "errorText": "Error text"
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
