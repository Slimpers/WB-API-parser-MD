# analytics

**Аналитика и данные** — версия `analytics`

Узнать больше об аналитике и данных можно в <a href="https://seller.wildberries.ru/instructions/ru/ru/subcategory/seller-analytics">справочном центре</a>

В разделе описаны методы получения:
  1. [Воронки продаж](./analytics#tag/Voronka-prodazh)
  2. [Поисковых запросов по вашим товарам](./analytics#tag/Poiskovye-zaprosy-po-vashim-tovaram)
  3. [Истории остатков](./analytics#tag/Istoriya-ostatkov)
  4. [Аналитики продавца в формате CSV](./analytics#tag/Analitika-prodavca-CSV)

## Разделы (tags)
- [Аналитика и данные](tags/Аналитика и данные.md)
- [Воронка продаж](tags/Воронка продаж.md)
- [Поисковые запросы по вашим товарам](tags/Поисковые запросы по вашим товарам.md)
- [История остатков](tags/История остатков.md)
- [Аналитика продавца CSV](tags/Аналитика продавца CSV.md)

## Эндпоинты
- [`POST /api/analytics/v3/sales-funnel/products` — Статистика карточек товаров за период{{ /api/analytics/v3/sales-funnel/products }}](operations/POST api-analytics-v3-sales-funnel-products.md)
- [`POST /api/analytics/v3/sales-funnel/products/history` — Статистика карточек товаров по дням{{ /api/analytics/v3/sales-funnel/products/history }}](operations/POST api-analytics-v3-sales-funnel-products-history.md)
- [`POST /api/analytics/v3/sales-funnel/grouped/history` — Статистика групп карточек товаров по дням{{ /api/analytics/v3/sales-funnel/grouped/history }}](operations/POST api-analytics-v3-sales-funnel-grouped-history.md)
- [`POST /api/v2/nm-report/downloads` — Создать отчёт{{ /api/v2/nm-report/downloads }}](operations/POST api-v2-nm-report-downloads.md)
- [`GET /api/v2/nm-report/downloads` — Получить список отчётов{{ /api/v2/nm-report/downloads }}](operations/GET api-v2-nm-report-downloads.md)
- [`POST /api/v2/nm-report/downloads/retry` — Сгенерировать отчёт повторно{{ /api/v2/nm-report/downloads/retry }}](operations/POST api-v2-nm-report-downloads-retry.md)
- [`GET /api/v2/nm-report/downloads/file/{downloadId}` — Получить отчёт{{ /api/v2/nm-report/downloads/file/{downloadId} }}](operations/GET api-v2-nm-report-downloads-file-{downloadId}.md)
- [`POST /api/v2/search-report/report` — Основная страница{{ /api/v2/search-report/report }}](operations/POST api-v2-search-report-report.md)
- [`POST /api/v2/search-report/table/groups` — Пагинация по группам{{ /api/v2/search-report/table/groups }}](operations/POST api-v2-search-report-table-groups.md)
- [`POST /api/v2/search-report/table/details` — Пагинация по товарам в группе{{ /api/v2/search-report/table/details }}](operations/POST api-v2-search-report-table-details.md)
- [`POST /api/v2/search-report/product/search-texts` — Поисковые запросы по товару{{ /api/v2/search-report/product/search-texts }}](operations/POST api-v2-search-report-product-search-texts.md)
- [`POST /api/v2/search-report/product/orders` — Заказы и позиции по поисковым запросам товара{{ /api/v2/search-report/product/orders }}](operations/POST api-v2-search-report-product-orders.md)
- [`POST /api/analytics/v1/stocks-report/wb-warehouses` — Остатки на складах WB{{ /api/analytics/v1/stocks-report/wb-warehouses }}](operations/POST api-analytics-v1-stocks-report-wb-warehouses.md)
- [`POST /api/v2/stocks-report/products/groups` — Данные по группам{{ /api/v2/stocks-report/products/groups }}](operations/POST api-v2-stocks-report-products-groups.md)
- [`POST /api/v2/stocks-report/products/products` — Данные по товарам{{ /api/v2/stocks-report/products/products }}](operations/POST api-v2-stocks-report-products-products.md)
- [`POST /api/v2/stocks-report/products/sizes` — Данные по размерам{{ /api/v2/stocks-report/products/sizes }}](operations/POST api-v2-stocks-report-products-sizes.md)
- [`POST /api/v2/stocks-report/offices` — Данные по складам{{ /api/v2/stocks-report/offices }}](operations/POST api-v2-stocks-report-offices.md)
