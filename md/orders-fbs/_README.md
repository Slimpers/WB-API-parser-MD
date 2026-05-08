# orders-fbs

**Заказы FBS** — версия `order`

С помощью методов раздела Заказы FBS (Fulfillment by Seller) вы можете:
  - получать информацию о [сборочных заданиях](./orders-fbs#tag/Sborochnye-zadaniya-FBS) и их статусах, отменять сборочные задания, получать стикеры
  - добавлять, редактировать и удалять [метаданные](./orders-fbs#tag/Metadannye-FBS) сборочных заданий
  - управлять [поставками](./orders-fbs#tag/Postavki-FBS)
  - создавать, редактировать и удалять [пропуска](./orders-fbs#tag/Propuska-FBS) на склады WB

  Узнать, как использовать методы в бизнес-кейсах, можно в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a4-0771-7571-aea9-11d5b597f34c/zakazy-fbs">инструкции</a> по работе с <strong>заказами FBS</strong>

  Узнать больше о заказах FBS можно в <a href="https://seller.wildberries.ru/instructions/ru/ru/category/b3e60238-fd4c-49ce-8668-ff688725a12d">справочном центре</a>

## Разделы (tags)
- [Заказы FBS](tags/Заказы FBS.md)
- [Сборочные задания FBS](tags/Сборочные задания FBS.md)
- [Метаданные FBS](tags/Метаданные FBS.md)
- [Поставки FBS](tags/Поставки FBS.md)
- [Пропуска FBS](tags/Пропуска FBS.md)

## Эндпоинты
- [`GET /api/v3/passes/offices` — Получить список складов, для которых требуется пропуск{{ /api/v3/passes/offices }}](operations/GET api-v3-passes-offices.md)
- [`GET /api/v3/passes` — Получить список пропусков{{ /api/v3/passes }}](operations/GET api-v3-passes.md)
- [`POST /api/v3/passes` — Создать пропуск{{ /api/v3/passes }}](operations/POST api-v3-passes.md)
- [`PUT /api/v3/passes/{passId}` — Обновить пропуск{{ /api/v3/passes/{passId} }}](operations/PUT api-v3-passes-{passId}.md)
- [`DELETE /api/v3/passes/{passId}` — Удалить пропуск{{ /api/v3/passes/{passId} }}](operations/DELETE api-v3-passes-{passId}.md)
- [`GET /api/v3/orders/new` — Получить список новых сборочных заданий{{ /api/v3/orders/new }}](operations/GET api-v3-orders-new.md)
- [`GET /api/v3/orders` — Получить информацию о сборочных заданиях{{ /api/v3/orders }}](operations/GET api-v3-orders.md)
- [`POST /api/v3/orders/status` — Получить статусы сборочных заданий{{ /api/v3/orders/status }}](operations/POST api-v3-orders-status.md)
- [`GET /api/v3/supplies/orders/reshipment` — Получить все сборочные задания для повторной отгрузки{{ /api/v3/supplies/orders/reshipment }}](operations/GET api-v3-supplies-orders-reshipment.md)
- [`PATCH /api/v3/orders/{orderId}/cancel` — Отменить сборочное задание{{ /api/v3/orders/{orderId}/cancel }}](operations/PATCH api-v3-orders-{orderId}-cancel.md)
- [`POST /api/v3/orders/stickers` — Получить стикеры сборочных заданий{{ /api/v3/orders/stickers }}](operations/POST api-v3-orders-stickers.md)
- [`POST /api/marketplace/v3/orders/meta` — Получить метаданные сборочных заданий{{ /api/marketplace/v3/orders/meta }}](operations/POST api-marketplace-v3-orders-meta.md)
- [`DELETE /api/v3/orders/{orderId}/meta` — Удалить метаданные сборочного задания{{ /api/v3/orders/{orderId}/meta }}](operations/DELETE api-v3-orders-{orderId}-meta.md)
- [`PUT /api/v3/orders/{orderId}/meta/sgtin` — Закрепить за сборочным заданием код маркировки Честного знака{{ /api/v3/orders/{orderId}/meta/sgtin }}](operations/PUT api-v3-orders-{orderId}-meta-sgtin.md)
- [`PUT /api/v3/orders/{orderId}/meta/uin` — Закрепить за сборочным заданием УИН{{ /api/v3/orders/{orderId}/meta/uin }}](operations/PUT api-v3-orders-{orderId}-meta-uin.md)
- [`PUT /api/v3/orders/{orderId}/meta/imei` — Закрепить за сборочным заданием IMEI{{ /api/v3/orders/{orderId}/meta/imei }}](operations/PUT api-v3-orders-{orderId}-meta-imei.md)
- [`PUT /api/v3/orders/{orderId}/meta/gtin` — Закрепить за сборочным заданием GTIN{{ /api/v3/orders/{orderId}/meta/gtin }}](operations/PUT api-v3-orders-{orderId}-meta-gtin.md)
- [`PUT /api/v3/orders/{orderId}/meta/expiration` — Закрепить за сборочным заданием срок годности товара{{ /api/v3/orders/{orderId}/meta/expiration }}](operations/PUT api-v3-orders-{orderId}-meta-expiration.md)
- [`PUT /api/marketplace/v3/orders/{orderId}/meta/customs-declaration` — Закрепить за сборочным заданием номер ГТД{{ /api/marketplace/v3/orders/{orderId}/meta/customs-declaration }}](operations/PUT api-marketplace-v3-orders-{orderId}-meta-customs-declaration.md)
- [`POST /api/v3/orders/stickers/cross-border` — Получить стикеры сборочных заданий трансграничных поставок{{ /api/v3/orders/stickers/cross-border }}](operations/POST api-v3-orders-stickers-cross-border.md)
- [`POST /api/v3/orders/status/history` — История статусов для сборочных заданий трансграничных поставок{{ /api/v3/orders/status/history }}](operations/POST api-v3-orders-status-history.md)
- [`POST /api/v3/orders/client` — Заказы с информацией по клиенту{{ /api/v3/orders/client }}](operations/POST api-v3-orders-client.md)
- [`POST /api/v3/supplies` — Создать новую поставку{{ /api/v3/supplies }}](operations/POST api-v3-supplies.md)
- [`GET /api/v3/supplies` — Получить список поставок{{ /api/v3/supplies }}](operations/GET api-v3-supplies.md)
- [`PATCH /api/marketplace/v3/supplies/{supplyId}/orders` — Добавить сборочные задания к поставке{{ /api/marketplace/v3/supplies/{supplyId}/orders }}](operations/PATCH api-marketplace-v3-supplies-{supplyId}-orders.md)
- [`GET /api/v3/supplies/{supplyId}` — Получить информацию о поставке{{ /api/v3/supplies/{supplyId} }}](operations/GET api-v3-supplies-{supplyId}.md)
- [`DELETE /api/v3/supplies/{supplyId}` — Удалить поставку{{ /api/v3/supplies/{supplyId} }}](operations/DELETE api-v3-supplies-{supplyId}.md)
- [`GET /api/marketplace/v3/supplies/{supplyId}/order-ids` — Получить ID сборочных заданий поставки{{ /api/marketplace/v3/supplies/{supplyId}/order-ids }}](operations/GET api-marketplace-v3-supplies-{supplyId}-order-ids.md)
- [`PATCH /api/v3/supplies/{supplyId}/deliver` — Передать поставку в доставку{{ /api/v3/supplies/{supplyId}/deliver }}](operations/PATCH api-v3-supplies-{supplyId}-deliver.md)
- [`GET /api/v3/supplies/{supplyId}/barcode` — Получить QR-код поставки{{ /api/v3/supplies/{supplyId}/barcode }}](operations/GET api-v3-supplies-{supplyId}-barcode.md)
- [`GET /api/v3/supplies/{supplyId}/trbx` — Получить список грузомест поставки{{ /api/v3/supplies/{supplyId}/trbx }}](operations/GET api-v3-supplies-{supplyId}-trbx.md)
- [`POST /api/v3/supplies/{supplyId}/trbx` — Добавить грузоместа к поставке{{ /api/v3/supplies/{supplyId}/trbx }}](operations/POST api-v3-supplies-{supplyId}-trbx.md)
- [`DELETE /api/v3/supplies/{supplyId}/trbx` — Удалить грузоместа из поставки{{ /api/v3/supplies/{supplyId}/trbx }}](operations/DELETE api-v3-supplies-{supplyId}-trbx.md)
- [`POST /api/v3/supplies/{supplyId}/trbx/stickers` — Получить стикеры грузомест поставки{{ /api/v3/supplies/{supplyId}/trbx/stickers }}](operations/POST api-v3-supplies-{supplyId}-trbx-stickers.md)
- [`GET /api/marketplace/v3/fbs/orders/archive` — Получить список архивных сборочных заданий{{ /api/marketplace/v3/fbs/orders/archive }}](operations/GET api-marketplace-v3-fbs-orders-archive.md)
