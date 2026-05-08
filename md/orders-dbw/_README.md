# orders-dbw

**Заказы DBW** — версия `ordersdbw`

С помощью методов Заказы DBW (Доставка курьером WB) вы можете:
  - получать информацию о [сборочных заданиях](./orders-dbw#tag/Sborochnye-zadaniya-DBW), управлять статусами и отменять сборочные задания
  - получать, добавлять, редактировать и удалять [метаданные](./orders-dbw#tag/Metadannye-DBW) сборочных заданий

<div class="description_ref">
  Узнать, как использовать методы в бизнес-кейсах, можно в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a4-036a-7721-98e8-bed5f1a4f72d/zakazy-dbw">инструкции</a> по работе с <strong>заказами DBW</strong>
</div>

## Разделы (tags)
- [Заказы DBW](tags/Заказы DBW.md)
- [Сборочные задания DBW](tags/Сборочные задания DBW.md)
- [Метаданные DBW](tags/Метаданные DBW.md)

## Эндпоинты
- [`GET /api/v3/dbw/orders/new` — Получить список новых сборочных заданий{{ /api/v3/dbw/orders/new }}](operations/GET api-v3-dbw-orders-new.md)
- [`GET /api/v3/dbw/orders` — Получить информацию о завершенных сборочных заданиях{{ /api/v3/dbw/orders }}](operations/GET api-v3-dbw-orders.md)
- [`POST /api/v3/dbw/orders/delivery-date` — Дата и время доставки{{ /api/v3/dbw/orders/delivery-date }}](operations/POST api-v3-dbw-orders-delivery-date.md)
- [`POST /api/marketplace/v3/dbw/orders/client` — Информация о покупателе{{ /api/marketplace/v3/dbw/orders/client }}](operations/POST api-marketplace-v3-dbw-orders-client.md)
- [`POST /api/v3/dbw/orders/status` — Получить статусы сборочных заданий{{ /api/v3/dbw/orders/status }}](operations/POST api-v3-dbw-orders-status.md)
- [`PATCH /api/v3/dbw/orders/{orderId}/confirm` — Перевести на сборку{{ /api/v3/dbw/orders/{orderId}/confirm }}](operations/PATCH api-v3-dbw-orders-{orderId}-confirm.md)
- [`POST /api/v3/dbw/orders/stickers` — Получить стикеры сборочных заданий{{ /api/v3/dbw/orders/stickers }}](operations/POST api-v3-dbw-orders-stickers.md)
- [`POST /api/marketplace/v3/dbw/orders/status/deliver` — Перевести сборочные задания в доставку{{ /api/marketplace/v3/dbw/orders/status/deliver }}](operations/POST api-marketplace-v3-dbw-orders-status-deliver.md)
- [`POST /api/v3/dbw/orders/courier` — Информация о курьере{{ /api/v3/dbw/orders/courier }}](operations/POST api-v3-dbw-orders-courier.md)
- [`PATCH /api/v3/dbw/orders/{orderId}/cancel` — Отменить сборочное задание{{ /api/v3/dbw/orders/{orderId}/cancel }}](operations/PATCH api-v3-dbw-orders-{orderId}-cancel.md)
- [`PATCH /api/v3/dbw/orders/{orderId}/assemble` — Перевести в доставку{{ /api/v3/dbw/orders/{orderId}/assemble }}](operations/PATCH api-v3-dbw-orders-{orderId}-assemble.md)
- [`POST /api/marketplace/v3/dbw/orders/meta/details` — Получить метаданные сборочных заданий{{ /api/marketplace/v3/dbw/orders/meta/details }}](operations/POST api-marketplace-v3-dbw-orders-meta-details.md)
- [`POST /api/marketplace/v3/dbw/orders/meta/delete` — Удалить метаданные сборочных заданий{{ /api/marketplace/v3/dbw/orders/meta/delete }}](operations/POST api-marketplace-v3-dbw-orders-meta-delete.md)
- [`GET /api/v3/dbw/orders/{orderId}/meta` — Получить метаданные сборочного задания{{ /api/v3/dbw/orders/{orderId}/meta }}](operations/GET api-v3-dbw-orders-{orderId}-meta.md)
- [`DELETE /api/v3/dbw/orders/{orderId}/meta` — Удалить метаданные сборочного задания{{ /api/v3/dbw/orders/{orderId}/meta }}](operations/DELETE api-v3-dbw-orders-{orderId}-meta.md)
- [`POST /api/marketplace/v3/dbw/orders/meta/sgtin` — Закрепить коды маркировки Честного знака за сборочными заданиями{{ /api/marketplace/v3/dbw/orders/meta/sgtin }}](operations/POST api-marketplace-v3-dbw-orders-meta-sgtin.md)
- [`PUT /api/v3/dbw/orders/{orderId}/meta/sgtin` — Закрепить за сборочным заданием код маркировки товара{{ /api/v3/dbw/orders/{orderId}/meta/sgtin }}](operations/PUT api-v3-dbw-orders-{orderId}-meta-sgtin.md)
- [`PUT /api/v3/dbw/orders/{orderId}/meta/uin` — Закрепить за сборочным заданием УИН (уникальный идентификационный номер){{ /api/v3/dbw/orders/{orderId}/meta/uin }}](operations/PUT api-v3-dbw-orders-{orderId}-meta-uin.md)
- [`PUT /api/v3/dbw/orders/{orderId}/meta/imei` — Закрепить за сборочным заданием IMEI{{ /api/v3/dbw/orders/{orderId}/meta/imei }}](operations/PUT api-v3-dbw-orders-{orderId}-meta-imei.md)
- [`PUT /api/v3/dbw/orders/{orderId}/meta/gtin` — Закрепить за сборочным заданием GTIN{{ /api/v3/dbw/orders/{orderId}/meta/gtin }}](operations/PUT api-v3-dbw-orders-{orderId}-meta-gtin.md)
