# GET /api/v2/nm-report/downloads/file/{downloadId}

**Получить отчёт{{ /api/v2/nm-report/downloads/file/{downloadId} }}**

теги: `Аналитика продавца CSV`

**Полный путь:** `GET /api/v2/nm-report/downloads/file/{downloadId}`

## Описание

<div class='description-title'><span>Описание метода</span></div>

Метод возвращает отчёт с расширенной аналитикой продавца по ID [задания на генерацию](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads/post).
<br><br>
Можно получить отчёт, который сгенерирован за последние 48 часов.<br>Отчёт будет загружен внутри архива ZIP в формате CSV.

<div class="description_limit">
<a href='./api-information#tag/Vvedenie/Limity-zaprosov'>Лимит запросов</a> на один аккаунт продавца:


| Тип | Период | Лимит | Интервал | Всплеск |
| --- | --- | --- | --- | --- |
| Персональный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Сервисный | 1 мин | 3 запроса | 20 сек | 3 запроса |
| Базовый | 1 ч | 1 запрос | 1 ч | 1 запрос |
</div>

## Авторизация

- `HeaderApiKey` (scopes: —)

## Параметры

| Имя | В | Тип | Обязательный | Описание |
|---|---|---|---|---|
| `downloadId` | path | string (uuid) | да | ID отчёта |

## Ответы


#### 200 — Успешно

**Content-Type:** `application/zip`

Описание полей в файле CSV:
<br>
<br>
**Воронка продаж**

| Имя | Тип | Формат | Описание |
|-----------------| --- | --- | --- |
| nmID (только для `DETAIL_HISTORY_REPORT`) | integer | int32 | Артикул WB |
| dt | string | date | Дата |
| openCardCount | integer | int32 | Переходы в карточку товара |
| addToCartCount | integer | int32 | Положили в корзину, шт. |
| ordersCount | integer | int32 | Заказали товаров, шт. |
| ordersSumRub | integer | int32 | Заказали на сумму |
| buyoutsCount | integer | int32 | Выкупили товаров, шт. |
| buyoutsSumRub | integer | int32 | Выкупили на сумму |
| cancelCount | integer | int32 | Отменили и вернули товаров, шт. |
| cancelSumRub | integer | int32 | Отменили и вернули на сумму |
| addToCartConversion | number | int32 | Конверсия в корзину, % (Какой процент посетителей, открывших карточку товара, добавили товар в корзину) |
| cartToOrderConversion | integer | int32 | Конверсия в заказ, % (Какой процент посетителей, добавивших товар в корзину, сделали заказ) |
| buyoutPercent | integer | int32 | Процент выкупа, % (Какой процент посетителей, заказавших товар, его выкупили. Без учёта товаров, которые еще доставляются покупателю) |
| addToWishlist | integer | int32 | Добавили в **Отложенные**|
| currency | string | string | Валюта отчёта |


**Отчёт по параметрам поиска. По предметам, брендам и ярлыкам**

| Имя | Поле | Формат | Описание |
|-----------------| --- | --- | --- |
| SubjectName |	string | string | Название предмета |
| SubjectID | integer | int32 | ID предмета |
| BrandName | string | string  | Бренд |
| TagID | integer | int64 | ID ярлыка |
| AveragePosition | integer | uint64 | Средняя позиция в поиске в текущий период |
| OpenCard | integer | uint64 | Количество переходов в карточку товара из поиска в текущий период |
| AddToCart | integer | uint64 | Количество добавлений товара в корзину из поиска в текущий период |
| OpenToCart | integer | uint64 |	Конверсия в корзину из поиска в текущий период |
| Orders | integer | uint64 | Заказали товар из поиска в текущий период |
| CartToOrder | integer | uint64 | Конверсия в заказ из поиска в текущий период |
| Visibility | integer | uint64 | Видимость товара в поиске в текущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции |
| AveragePositionPast | integer | uint64 | Средняя позиция в поиске в предыдущий период (заполняется, если указан прошлый период) |
| OpenCardPast | integer | uint64 | Количество переходов в карточку товара из поиска в предыдущий период (заполняется, если указан прошлый период) |
| AddToCartPast | integer | uint64 | Количество добавлений товара в корзину из поиска в предыдущий период (заполняется, если указан прошлый период) |
| OpenToCartPast | integer | uint64 | Конверсия в корзину из поиска в предыдущий период (заполняется, если указан прошлый период) |
| OrdersPast | integer | uint64 | Заказали товар из поиска в предыдущий период (заполняется, если указан прошлый период) |
| CartToOrderPast | integer | uint64 | Конверсия в заказ из поиска в предыдущий период (заполняется, если указан прошлый период) |
| VisibilityPast | integer | uint64 | Видимость товара в поиске в предыдущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции (заполняется, если указан прошлый период), % |


**Отчёт по параметрам поиска. По артикулам WB**

| Имя | Поле | Формат | Описание |
|-----------------| --- | --- | --- |
| NmID | integer | int64 | Артикул WB |
| VendorCode | string | string | Артикул продавца |
| Name | string	| string | Название товара |
| SubjectName | string	| string | Название предмета |
| BrandName | string | string  | Бренд |
| IsAdvertised | boolean | bool	| Рекламируется ли товар |
| IsRated | boolean | bool | Есть ли возможность оценить качество карточки товара |
| Rating | float | float64 | Рейтинг карточки товара |
| FeedbackRating | float | float64 | Рейтинг по отзывам |
| MinPrice | integer | uint64 | Минимальная цена продавца со скидкой продавца (без учёта скидки WB Клуба |
| MaxPrice | integer | uint64 | Максимальная цена продавца со скидкой продавца (без учёта скидки WB Клуба) |
| AveragePosition | integer | uint64 | Средняя позиция товара в поиске в текущий период |
| OpenCard | integer | uint64 | Количество переходов в карточку товара из поиска в текущий период |
| AddToCart | integer | uint64 | Количество добавлений товара в корзину из поиска в текущий период |
| OpenToCart | integer | uint64 | Конверсия в корзину из поиска в текущий период |
| Orders | integer | uint64 | Заказали товар из поиска в текущий период |
| CartToOrder | integer | uint64 | Конверсия в заказ из поиска в текущий период |
| Visibility | integer | uint64 | Видимость товара в поиске в текущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции |
| AveragePositionPast | integer | uint64 | Средняя позиция товара в поиске в предыдущий период (заполняется, если указан прошлый период) |
| OpenCardPast | integer | uint64 | Количество переходов в карточку товара из поиска в предыдущий период (заполняется, если указан прошлый период) |
| AddToCartPast | integer | uint64 | Количество добавлений товара в корзину из поиска в предыдущий период (заполняется, если указан прошлый период) |
| OpenToCartPast | integer | uint64 | Конверсия в корзину из поиска в предыдущий период (заполняется, если указан прошлый период) |
| OrdersPast | integer | uint64 | Заказали товар из поиска в предыдущий период (заполняется, если указан прошлый период) |
| CartToOrderPast | integer | uint64 | Конверсия в заказ из поиска в предыдущий период (заполняется, если указан прошлый период) |
| VisibilityPast | integer | uint64 | Видимость товара в поиске в предыдущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции (заполняется, если указан прошлый период), % |
| IsSubstitutedSKU | boolean | bool | Искали ли товар по подменному артикулу. Будет в ответе при наличии в запросе `includeSubstitutedSKUs` и/или `includeSearchTexts` |
| Currency | string | string | Валюта отчёта |


**Отчёт по текстам поисковых запросов по вашим товарам**

| Имя | Поле | Формат | Описание |
|-----------------| --- | --- | --- |
| Text | string	| string | Текст поискового запроса |
| NmID | integer | int64 | Артикул WB |
| SubjectName | string	| string | Название предмета |
| BrandName | string | string  | Бренд |
| VendorCode | string | string | Артикул продавца |
| Name | string	| string | Название товара |
| Rating | float | float64 | Рейтинг карточки товара. Если рейтинг отсутствует, то значение будет `no rating` |
| FeedbackRating | float | float64 | Рейтинг по отзывам |
| MinPrice | integer | uint64 | Минимальная цена продавца со скидкой продавца (без учёта скидки WB Клуба) |
| MaxPrice | integer | uint64 | Максимальная цена продавца со скидкой продавца (без учёта скидки WB Клуба) |
| Frequency | integer | uint64 | Количество обращений с поисковым запросом в текущий период |
| MedianPosition | float | float64 | Медианная позиция товара в поиске в текущий период. Учитываются только те позиции, из которых пользователи добавляли товар в корзину или переходили в его карточку. Серединное значение позиции в поисковой выдаче, которое исключает сильные отклонения данных от среднего значения |
| AveragePosition | integer | uint64 | Средняя позиция товара в поиске в текущий период. Учитываются только те позиции, из которых пользователи добавляли товар в корзину или переходили в его карточку |
| OpenCard | integer | uint64 | Количество открытий карточки товара из поисковой выдачи в текущий период |
| OpenCardPercentile | float | float64 | Процент, на который показатель количества открытий карточки товара выше, чем у карточек конкурентов по поисковому запросу |
| AddToCart | integer | uint64 | Количество добавлений товара в корзину из поисковой выдачи в текущий период |
| AddToCartPercentile | float | float64 | Процент, на который показатель добавлений в корзину выше, чем у карточек конкурентов по поисковому запросу |
| OpenToCart | integer | uint64 | Конверсия в корзину из поиска в текущий период, % |
| OpenToCartPercentile	| float	| float64	| Процент, на который показатель конверсии в корзину выше, чем у карточек конкурентов по поисковому запросу |
| Orders | integer | uint64 | Заказали товар из поиска в текущий период |
| OrdersPercentile | float | float64 | Процент, на который показатель заказов выше, чем у карточек конкурентов по поисковому запросу |
| CartToOrder | integer | uint64 | Конверсия в заказ из поиска в текущий период, % |
| CartToOrderPercentile | float | float64 | Процент, на который показатель конверсии в заказ выше, чем у карточек конкурентов по поисковому запросу |
| Visibility | integer | uint64 | Видимость товара в поиске в текущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции |
| FrequencyPast | integer | uint64 | Количество обращений с поисковым запросом за предыдущий период (заполняется, если указан прошлый период) |
| MedianPositionPast | float | float64 | Медианная позиция товара в поиске за предыдущий период (заполняется, если указан прошлый период) |
| AveragePositionPast | integer | uint64 | Средняя позиция товара в поиске в предыдущий период (заполняется, если указан прошлый период) |
| OpenCardPast | integer | uint64 | Количество открытий карточки товара из поисковой выдачи в предыдущий период (заполняется, если указан прошлый период) |
| AddToCartPast | integer | uint64 | Количество добавлений товара в корзину в предыдущий период (заполняется, если указан прошлый период) |
| OpenToCartPast | integer | uint64 | Конверсия в корзину из поиска в предыдущий период (заполняется, если указан прошлый период) |
| OrdersPast | integer | uint64 | Заказали товар из поиска в предыдущий период (заполняется, если указан прошлый период) |
| CartToOrderPast | integer | uint64 | Конверсия в заказ из поиска в предыдущий период (заполняется, если указан прошлый период), % |
| VisibilityPast | integer | uint64 | Видимость товара в поиске в предыдущий период. Процент вероятности, что пользователь увидит карточку товара. Зависит от средней позиции (заполняется, если указан прошлый период), % |
| Currency | string | string | Валюта отчёта |


**Отчёт по статистике остатков**

| Имя | Поле | Формат | Описание |
|-----------------| --- | --- | --- |
| VendorCode | string | string | Артикул продавца |
| Name | string	| string | Название товара |
| NmID | integer | int64 | Артикул WB |
| SubjectName | string	| string | Название предмета |
| BrandName | string | string  | Бренд |
| SizeName | string	| string | Название размера |
| ChrtID | integer | int64 | ID размера |
| RegionName | string	| string | Регион отгрузки. Для складов продавца значение в строках будет `Маркетплейс`, так как данные по складам продавца приходят в агрегированном виде — по всем сразу, без детализации по конкретным складам |
| OfficeName | string	| string | Название склада. Для складов продавца значение в строках будет `Маркетплейс`, так как данные по складам продавца приходят в агрегированном виде — по всем сразу, без детализации по конкретным складам |
| Availability | string	| enum | Доступность товара |
| OrdersCount | integer	| uint64 | Заказы, шт. |
| OrdersSum | integer	| uint64 | Заказы, сумма |
| BuyoutCount | integer	| uint64 | Выкупы, шт. |
| BuyoutSum | integer	| uint64 | Выкупы, сумма |
| BuyoutPercent | integer	| uint32 | Процент выкупа |
| AvgOrders | number	| float64 | Среднее количество заказов в день |
| StockCount | integer	| uint64 | Остатки на текущий день, шт. |
| StockSum | integer	| uint64 | Стоимость остатков на текущий день |
| SaleRate | integer	| int32 | Оборачиваемость текущих остатков в часах |
| AvgStockTurnover | integer	| int32 | Оборачиваемость средних остатков в часах |
| ToClientCount | integer	| uint64 | В пути к клиенту, шт. |
| FromClientCount | integer	| uint64 | В пути от клиента, шт. |
| Price | integer	| uint64 | Текущая цена продавца со скидкой продавца (без учёта скидки WB Клуба) |
| OfficeMissingTime | integer	| int32 | Время отсутствия товара на складе в часах |
| LostOrdersCount | number	| float64 | Упущенные заказы, шт. |
| LostOrdersSum | number	| float64 | Упущенные заказы, сумма |
| LostBuyoutsCount | number	| float64 | Упущенные выкупы, шт. |
| LostBuyoutsSum | number	| float64 | Упущенные выкупы, сумма |
| AvgOrdersByMonth_MM.YYYY | number	| float64 | Среднее количество заказов по месяцам. Столбцы формируются динамически в зависимости от переданного текущего периода. Каждому месяцу текущего периода соответствует один столбец. В случае, если товар не существовал на момент конкретного месяца, то значение будет пропущено |
| Currency | string | string | Валюта отчёта |


**Отчёт по истории остатков**

| Имя | Поле | Формат | Описание |
|-----------------| --- | --- | --- |
| VendorCode | string | string | Артикул продавца |
| Name | string	| string | Название товара |
| NmID | integer | int64 | Артикул WB |
| SubjectName | string	| string | Название предмета |
| BrandName | string | string  | Бренд |
| SizeName | string	| string | Название размера |
| ChrtID | integer | int64 | ID размера |
| OfficeName | string	| string | Название склада. Для складов продавца значение в строках будет `Маркетплейс`, так как данные по складам продавца приходят в агрегированном виде — по всем сразу, без детализации по конкретным складам |
| DD.MM.YYYY | integer| uint64 | Остаток по состоянию на 23:59 дня в заголовке. Столбцы формируются динамически в зависимости от переданного в запросе периода. Каждому дню периода соответствует один столбец. Если товара не было в конкретный день, значение будет пропущено |
- string (binary)

*SalesFunnelProductRes:*

```json
"nmID, dt, openCardCount, addToCartCount, ordersCount, ordersSumRub, buyoutsCount, buyoutsSumRub, cancelCount, cancelSumRub, addToCartConversion, cartToOrderConversion, buyoutPercent, addToWishlist, currency\n70027655,2024-11-21,1,0,0,0,0,0,0,0,0,0,0,0,RUB\n...\n...\n150317666,2024-11-21,2,0,0,0,0,0,0,0,0,0,0,0,RUB\n"
```

*SalesFunnelGroupRes:*

```json
"dt, openCardCount, addToCartCount, ordersCount, ordersSumRub, buyoutsCount, buyoutsSumRub, cancelCount, cancelSumRub, addToCartConversion, cartToOrderConversion, buyoutPercent, addToWishlist, currency\n2024-11-21,1,0,0,0,0,0,0,0,0,0,0,0,RUB\n...\n...\n2024-11-21,2,0,0,0,0,0,0,0,0,0,0,0,RUB\n"
```

*SearchReportGroupRes:*

```json
"SubjectName,SubjectID,BrandName,TagID,AveragePosition,OpenCard,AddToCart,OpenToCart,Orders,CartToOrder,Visibility,AveragePositionPast,OpenCardPast,AddToCartPast,OpenToCartPast,OrdersPast,CartToOrderPast,VisibilityPast\nСмартфоны,0,Abble,0,1,4,0,0,0,0,100,1,8,0,0,0,0,100\nСмартфоны,0,abble,0,1,63,0,0,0,0,100,1,91,0,0,0,0,100\n"
```

*SearchReportProductRes:*

```json
"NmID,VendorCode,Name,Subject,Brand,IsAdvertised,IsRated,Rating,FeedbackRating,MinPrice,MaxPrice,AveragePosition,OpenCard,AddToCart,OpenToCart,Orders,CartToOrder,Visibility,AveragePositionPast,OpenCardPast,AddToCartPast,OpenToCartPast,OrdersPast,CartToOrderPast,VisibilityPast,IsSubstitutedSKU,Currency\n268913787,wb3ha2668w,iPhone 13 256 ГБ Серебристый,Смартфоны,abble,false,true,10,0,140000,140000,1,51,0,0,0,0,100,1,91,0,0,0,0,100,true,RUB\n246935327,wb729wy604,,Бирки для ключей,,false,true,1.5,0,89,89,1,37,19,51,6,32,100,1,14,21,150,3,14,100,true,RUB\n"
```

*SearchReportTextRes:*

```json
"Text,NmID,SubjectName,BrandName,VendorCode,Name,Rating,FeedbackRating,MinPrice,MaxPrice,Frequency,MedianPosition,AveragePosition,OpenCard,OpenCardPercentile,AddToCart,AddToCartPercentile,OpenToCart,OpenToCartPercentile,Orders,OrdersPercentile,CartToOrder,CartToOrderPercentile,Visibility,FrequencyPast,MedianPositionPast,AveragePositionPast,OpenCardPast,AddToCartPast,OpenToCartPast,OrdersPast,CartToOrderPast,VisibilityPast,Currency\n267945415,267945415,Термокомплекты для малышей,Lopsa,wb44h5ku68,1,5.5,0.0,47,47,156,1,1,235,100,98,100,42,100,0,100,0,100,100,15,1,1,19,16,84,0,0,100,RUB\nтермобелье мужское,267945415,Термокомплекты для малышей,Lopsa,wb44h5ku68,1,5.5,0.0,47,47,52633,2,2,5,0,0,0,0,0,0,0,0,0,100,49975,0,0,0,0,0,0,0,0,RUB\n267945415,296070764,Термокомплекты для малышей,Lopsa,wb51k31eyg,2,1.5,0.0,88,88,156,1,1,82,100,22,100,27,100,0,100,0,100,100,15,5,5,1,1,100,0,0,100,RUB\nтермобелье мужское,296070764,Термокомплекты для малышей,Lopsa,wb51k31eyg,2,1.5,0.0,88,88,52633,3,3,2,0,0,0,0,0,0,0,0,0,100,49975,0,0,0,0,0,0,0,0,RUB\n211131895,211131895,Костюмы,H&M,wb51k31eyg!!!,костюм,10.0,5.0,102,102,36,1,1,44,100,6,100,14,0,5,100,83,100,100,0,0,0,0,0,0,0,0,0,RUB\n221411786,211131895,Костюмы,H&M,wb51k31eyg!!!,костюм,10.0,5.0,102,102,19,1,1,2,11,0,0,0,0,0,0,0,0,100,3,0,0,0,0,0,0,0,0\nженские блузки,211131895,Костюмы,H&M,wb51k31eyg!!!,костюм,10.0,5.0,102,102,38383,14,14,1,0,0,0,0,0,0,0,0,0,79,29764,0,0,0,0,0,0,0,0,RUB\n"
```

*InventoryMetricsReportRes:*

```json
"VendorCode,Name,NmID,SubjectName,BrandName,SizeName,ChrtID,RegionName,OfficeName,Availability,OrdersCount,OrdersSum,BuyoutCount,BuyoutSum,BuyoutPercent,AvgOrders,StockCount,StockSum,SaleRate,AvgStockTurnover,ToClientCount,FromClientCount,Price,OfficeMissingTime,LostOrdersCount,LostOrdersSum,LostBuyoutsCount,LostBuyoutsSum,AvgOrdersByMonth_11.2013,AvgOrdersByMonth_12.2013,AvgOrdersByMonth_01.2014,AvgOrdersByMonth_02.2014,AvgOrdersByMonth_03.2014,AvgOrdersByMonth_04.2014,AvgOrdersByMonth_05.2014,AvgOrdersByMonth_06.2014,AvgOrdersByMonth_07.2014,Currency\n037456337500,Robust High-Performance Robot,1031126854494603033,Термокомплекты,Amazon Web Services,67-69,987654321,Central,Office1,nonLiquid,521124,521124000,123,123000,10,0.57,20,20000,-3,5,111,222,14008,-3,0.71,0.77,0.93,0.68,74067.12,29935.79,8895.27,37019.65,37934.89,62412.64,29857.97,0.00,72465.85,RUB\n089201683406,Luxe Blender Nexus,8904325039176595105,Термокомплекты,iRecycle,54-56,987654071,North,Office2,nonLiquid,1231,1231000,456,456000,20,0.71,30,30000,2,-3,333,444,85162,-2,0.90,0.96,0.31,0.93,,,,,,2628.77,0.00,70534.86,0.00,RUB\n059509746730,Pure Quartz Speaker,6780550382946145952,Термокомплекты,Next Step Living,60-62,984574321,South,Office3,balanced,3214,3214000,789,789000,30,0.30,40,40000,1,11,555,666,66484,-3,0.03,0.08,0.71,0.48,,,47297.22,55308.71,6463.43,48664.95,0.00,0.00,74502.72,RUB\n058266400986,Modular Stainless Monitor,3475827302459171321,Термокомплекты,TagniFi,65-67,926554321,East,Office4,nonActual,312,312000,123,123000,40,0.71,50,50000,13,-2,666,888,53254,-3,0.96,0.01,0.97,0.92,,67227.50,4608.98,90300.06,15890.52,0.00,0.00,41891.11,0.00,RUB\n070198970053,Microwave Quick Eco-Friendly,4734922922328623947,Термокомплекты,Boston Consulting Group,46-48,983234321,West,Office5,nonLiquid,343,343000,456,456000,50,0.92,60,60000,17,-2,777,101010,43823,-1,0.84,0.14,0.26,0.75,30463.57,8073.43,26678.35,0.00,339.99,56237.24,2172.75,74665.30,14296.76,RUB\n"
```

*InventoryHistoryReportRes:*

```json
"VendorCode,Name,NmID,SubjectName,BrandName,SizeName,ChrtID,OfficeName,13.12.2025,14.12.2025,15.12.2025\n41058/прозрачный,Чехол для телефона прозрачный111,5870243,Чехлы для телефонов,Arizona.kz,-,20964883,Коледино,1,1,1\n41058/прозрачный,Чехол для телефона прозрачный111,5870243,Чехлы для телефонов,Arizona.kz,-,20964883,Маркетплейс,1000,997,923\nwb59toaotq,Брюки,12862180,Болеро,,O,39533928,Маркетплейс,6,8,4\n451263124,Брюки 123,12862181,Брюки,DUB,A,39533929,Маркетплейс,11,10,11\nwb33q6504x,ПАЗЛ,13088345,Пазлы,CoolPuzzles,-,40030565,Маркетплейс,2,28,54\n4854554654/0,Альбом,13480414,Альбомы для коллекционирования,Эконом,-,40873579,Маркетплейс,25,20,19\n14053651Черный,Дубленка 333334,14652473,Дубленки,SARTORI DODICI,48,43253666,Маркетплейс,30,30,30\nHGF56X,Чай,14986284,Чай,Lipton,-,43804848,Коледино,154,254,223\n123401,Кроссовки,14917832,Кофе молотый,,-,43807552,Казань,0,0,0\n123401,Кроссовки,14917832,Кофе молотый,,-,43807552,Подольск,4,0,23\n"
```

#### 400 — Неправильный запрос

**Content-Type:** `application/json`

- `title` **(required)** — string. Заголовок ошибки
- `detail` **(required)** — string. Детали ошибки
- `requestId` **(required)** — string. Уникальный ID запроса
- `origin` **(required)** — string. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Invalid request body",
  "detail": "check correctness of download id",
  "requestId": "51b7828b-e298-4dfa-b7cd-45ab179921d3",
  "origin": "analytics-open-api"
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

- `title` — string. Заголовок ошибки
- `detail` — string. Детали ошибки
- `requestId` — string. Уникальный ID запроса
- `origin` — string. ID внутреннего сервиса WB

*errorExample:*

```json
{
  "title": "Authorization error",
  "detail": "Authorization error",
  "requestId": "51b7828b-e298-4dfa-b7cd-45ab179921d3",
  "origin": "analytics-open-api"
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
