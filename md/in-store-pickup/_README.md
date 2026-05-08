# in-store-pickup

**Заказы Самовывоз** — версия `instorepickup`

Управление [сборочными заданиями](./in-store-pickup#tag/Sborochnye-zadaniya-Samovyvoz) и [метаданными](./in-store-pickup#tag/Metadannye-Samovyvoz) заказов модели Самовывоз.

## Серверы
- `https://marketplace-api.wildberries.ru`

## Разделы (tags)
- [Заказы Самовывоз](tags/Заказы Самовывоз.md)
- [Сборочные задания Самовывоз](tags/Сборочные задания Самовывоз.md)
- [Метаданные Самовывоз](tags/Метаданные Самовывоз.md)

## Эндпоинты
- [`GET /api/v3/click-collect/orders/new` — Получить список новых сборочных заданий{{ /api/v3/click-collect/orders/new }}](operations/GET api-v3-click-collect-orders-new.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/confirm` — Перевести сборочные задания на сборку{{ /api/marketplace/v3/click-collect/orders/status/confirm }}](operations/POST api-marketplace-v3-click-collect-orders-status-confirm.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/prepare` — Сообщить, что сборочные задания готовы к выдаче{{ /api/marketplace/v3/click-collect/orders/status/prepare }}](operations/POST api-marketplace-v3-click-collect-orders-status-prepare.md)
- [`PATCH /api/v3/click-collect/orders/{orderId}/confirm` — Перевести на сборку{{ /api/v3/click-collect/orders/{orderId}/confirm }}](operations/PATCH api-v3-click-collect-orders-{orderId}-confirm.md)
- [`PATCH /api/v3/click-collect/orders/{orderId}/prepare` — Сообщить, что сборочное задание готово к выдаче{{ /api/v3/click-collect/orders/{orderId}/prepare }}](operations/PATCH api-v3-click-collect-orders-{orderId}-prepare.md)
- [`POST /api/v3/click-collect/orders/client` — Информация о покупателе{{ /api/v3/click-collect/orders/client }}](operations/POST api-v3-click-collect-orders-client.md)
- [`POST /api/v3/click-collect/orders/client/identity` — Проверить, что заказ принадлежит покупателю{{ /api/v3/click-collect/orders/client/identity }}](operations/POST api-v3-click-collect-orders-client-identity.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/receive` — Сообщить, что заказы приняты покупателями{{ /api/marketplace/v3/click-collect/orders/status/receive }}](operations/POST api-marketplace-v3-click-collect-orders-status-receive.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/reject` — Сообщить об отказе от заказов{{ /api/marketplace/v3/click-collect/orders/status/reject }}](operations/POST api-marketplace-v3-click-collect-orders-status-reject.md)
- [`PATCH /api/v3/click-collect/orders/{orderId}/receive` — Сообщить, что заказ принят покупателем{{ /api/v3/click-collect/orders/{orderId}/receive }}](operations/PATCH api-v3-click-collect-orders-{orderId}-receive.md)
- [`PATCH /api/v3/click-collect/orders/{orderId}/reject` — Сообщить, что покупатель отказался от заказа{{ /api/v3/click-collect/orders/{orderId}/reject }}](operations/PATCH api-v3-click-collect-orders-{orderId}-reject.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/info` — Получить статусы сборочных заданий{{ /api/marketplace/v3/click-collect/orders/status/info }}](operations/POST api-marketplace-v3-click-collect-orders-status-info.md)
- [`POST /api/v3/click-collect/orders/status` — Получить статусы сборочных заданий{{ /api/v3/click-collect/orders/status }}](operations/POST api-v3-click-collect-orders-status.md)
- [`GET /api/v3/click-collect/orders` — Получить информацию о завершённых сборочных заданиях{{ /api/v3/click-collect/orders }}](operations/GET api-v3-click-collect-orders.md)
- [`POST /api/marketplace/v3/click-collect/orders/status/cancel` — Отменить сборочные задания{{ /api/marketplace/v3/click-collect/orders/status/cancel }}](operations/POST api-marketplace-v3-click-collect-orders-status-cancel.md)
- [`PATCH /api/v3/click-collect/orders/{orderId}/cancel` — Отменить сборочное задание{{ /api/v3/click-collect/orders/{orderId}/cancel }}](operations/PATCH api-v3-click-collect-orders-{orderId}-cancel.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/info` — Получить метаданные сборочных заданий{{ /api/marketplace/v3/click-collect/orders/meta/info }}](operations/POST api-marketplace-v3-click-collect-orders-meta-info.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/delete` — Удалить метаданные сборочных заданий{{ /api/marketplace/v3/click-collect/orders/meta/delete }}](operations/POST api-marketplace-v3-click-collect-orders-meta-delete.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/sgtin` — Закрепить коды маркировки Честного знака за сборочными заданиями{{ /api/marketplace/v3/click-collect/orders/meta/sgtin }}](operations/POST api-marketplace-v3-click-collect-orders-meta-sgtin.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/uin` — Закрепить УИН за сборочными заданиями{{ /api/marketplace/v3/click-collect/orders/meta/uin }}](operations/POST api-marketplace-v3-click-collect-orders-meta-uin.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/imei` — Закрепить IMEI за сборочными заданиями{{ /api/marketplace/v3/click-collect/orders/meta/imei }}](operations/POST api-marketplace-v3-click-collect-orders-meta-imei.md)
- [`POST /api/marketplace/v3/click-collect/orders/meta/gtin` — Закрепить GTIN за сборочными заданиями{{ /api/marketplace/v3/click-collect/orders/meta/gtin }}](operations/POST api-marketplace-v3-click-collect-orders-meta-gtin.md)
- [`GET /api/v3/click-collect/orders/{orderId}/meta` — Получить метаданные сборочного задания{{ /api/v3/click-collect/orders/{orderId}/meta }}](operations/GET api-v3-click-collect-orders-{orderId}-meta.md)
- [`DELETE /api/v3/click-collect/orders/{orderId}/meta` — Удалить метаданные сборочного задания{{ /api/v3/click-collect/orders/{orderId}/meta }}](operations/DELETE api-v3-click-collect-orders-{orderId}-meta.md)
- [`PUT /api/v3/click-collect/orders/{orderId}/meta/sgtin` — Закрепить за сборочным заданием код маркировки товара{{ /api/v3/click-collect/orders/{orderId}/meta/sgtin }}](operations/PUT api-v3-click-collect-orders-{orderId}-meta-sgtin.md)
- [`PUT /api/v3/click-collect/orders/{orderId}/meta/uin` — Закрепить за сборочным заданием УИН (уникальный идентификационный номер){{ /api/v3/click-collect/orders/{orderId}/meta/uin }}](operations/PUT api-v3-click-collect-orders-{orderId}-meta-uin.md)
- [`PUT /api/v3/click-collect/orders/{orderId}/meta/imei` — Закрепить за сборочным заданием IMEI{{ /api/v3/click-collect/orders/{orderId}/meta/imei }}](operations/PUT api-v3-click-collect-orders-{orderId}-meta-imei.md)
- [`PUT /api/v3/click-collect/orders/{orderId}/meta/gtin` — Закрепить за сборочным заданием GTIN{{ /api/v3/click-collect/orders/{orderId}/meta/gtin }}](operations/PUT api-v3-click-collect-orders-{orderId}-meta-gtin.md)
