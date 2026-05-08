# GET /api/advert/v2/adverts

**Информация о кампаниях{{ /api/advert/v2/adverts }}**

теги: `Кампании`

**Полный путь:** `GET /api/advert/v2/adverts`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает информацию о рекламных кампаниях с единой или ручной ставкой по их статусам, типам оплаты и ID.

 <div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Сервисный | 1 сек | 5 запросов | 200 мс | 5 запросов |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `ids` | query | string; пример: `12345,23456,34567,45678,56789` | нет | ID кампаний, максимум 50 |
| `statuses` | query | string; пример: `-1,4,8` | нет | Статусы кампаний: - `-1` — удалена, процесс удаления будет завершён в течение 10 минут - `4` — готова к запуску - `7` — завершена - `8` — отменена - `9` — активна - `11` — на паузе |
| `payment_type` | query | string; enum: ["cpm", "cpc"] | нет | Тип оплаты: - `cpm` — за показы - `cpc` — за клик |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/json`

- `adverts` **(required)** — array<object>. Кампании
  - *(элементы)*
    - `bid_type` **(required)** — string. Тип ставки:
    - `id` **(required)** — integer (int64). ID кампании
    - `nm_settings` **(required)** — array<$ref: AdvertNMsSettings>. Настройки товаров
    - `settings` **(required)** — $ref: AdvertSettings
    - `status` **(required)** — integer; enum: [-1, 4, 7, 8, 9, 11]. Статус кампании:
    - `timestamps` **(required)** — $ref: Timestamps

```json
{
  "adverts": [
    {
      "bid_type": "manual",
      "id": 567456457,
      "nm_settings": [
        {
          "bids_kopecks": {
            "recommendations": 0,
            "search": 0
          },
          "nm_id": 123456789,
          "subject": {
            "id": 52,
            "name": "кошельки"
          }
        },
        {
          "bids_kopecks": {
            "recommendations": 11200,
            "search": 11200
          },
          "nm_id": 987654321,
          "subject": {
            "id": 54,
            "name": "ювелирные кольца"
          }
        }
      ],
      "settings": {
        "name": "Кампания от 01.02.2024",
        "payment_type": "cpm",
        "placements": {
          "recommendations": false,
          "search": true
        }
      },
      "status": 7,
      "timestamps": {
        "created": "2024-02-01T09:57:38.500606+03:00",
        "deleted": "2024-02-05T14:29:32.633968+03:00",
        "started": "2024-02-05T12:38:10.212086+03:00",
        "updated": "2024-02-05T14:29:32.633968+03:00"
      }
    },
    {
      "bid_type": "manual",
      "id": 28150154,
      "nm_settings": [
        {
          "bids_kopecks": {
            "recommendations": 0,
            "search": 1100
          },
          "nm_id": 5764746785,
          "subject": {
            "id": 69,
            "name": "платья"
          }
        }
      ],
      "settings": {
        "name": "Кампания от 28.08.2025 ",
        "payment_type": "cpc",
        "placements": {
          "recommendations": false,
          "search": true
        }
      },
      "status": 11,
      "timestamps": {
        "created": "2025-08-28T09:50:57.611559+03:00",
        "deleted": "2100-01-01T00:00:00+03:00",
        "started": null,
        "updated": "2025-09-10T10:14:58.475499+03:00"
      }
    }
  ]
}
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `detail` **(required)** — string. Детали ошибки
- `origin` **(required)** — string; пример: `camp-api-public-cache`. ID внутреннего сервиса WB
- `request_id` **(required)** — string; пример: `6023d2950af564838f9b44a279d2140c`. Уникальный ID запроса
- `status` **(required)** — integer; пример: `400`. HTTP статус-код
- `title` **(required)** — string; пример: `invalid payload`. Заголовок ошибки

```json
{
  "detail": "invalid payment_type value",
  "origin": "camp-api-public-cache",
  "request_id": "7e5cb1f106cc6e85b5b29eb2e8815da2",
  "status": 400,
  "title": "invalid payload"
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
