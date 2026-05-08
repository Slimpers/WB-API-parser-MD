# POST /content/v3/media/save

**Загрузить медиафайлы по ссылкам{{ /content/v3/media/save }}**

теги: `Медиафайлы`

**Полный путь:** `POST /content/v3/media/save`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод загружает набор медиафайлов в карточку товара через указание ссылок в запросе.

<div class="description_important">
  Новые медиафайлы полностью заменяют старые. Чтобы добавить новые медиафайлы, укажите в запросе ссылки одновременно на новые и старые медиафайлы.
</div>

Требования к ссылкам:
  * ссылка должна вести прямо на файл. Убедитесь, что ссылка не ведёт на страницу предпросмотра или авторизации, например. Если по ссылке открывается текстовая страница TXT или HTML, ссылка считается некорректной
  * для доступа к файлу по ссылке не нужна авторизация

Требования к изображениям:
  * максимум изображений для одной карточки товара — 30
  * минимальное разрешение — 700×900 px
  * максимальный размер — 32 Мб
  * минимальное качество — 65%
  * форматы — JPG, PNG, BMP, GIF (статичные), WebP

Требования к видео:
  * максимум одно видео для одной карточки товара
  * максимальный размер — 50 Мб
  * форматы — MOV, MP4

Если видео или хотя бы одно изображение в запросе не соответствует требованиям, то даже при успешном ответе (`200`) ни одно изображение/видео не загрузится.

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

## Запрос

### Тело запроса
*Обязательное.*

**Content-Type:** `application/json`

- `nmId` — integer. Артикул WB
- `data` — array<string>. Ссылки на изображения в том порядке, в котором они будут в карточке товара, и на видео, на любой позиции массива

**Пример:**

```json
{
  "nmId": 213864079,
  "data": [
    "https://basket-stage-02.dasec.ru/vol669/part66964/66964260/images/big/2.jpg",
    "https://sample-videos.com/video321/mp4/720/big_buck_bunny_720p_mb.mp4"
  ]
}
```

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

#### 409 — Ошибка сохранения части ссылок

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

#### 422 — Отсутствует параметр nmId

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
