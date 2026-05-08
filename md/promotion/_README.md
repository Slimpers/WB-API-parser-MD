# promotion

**Маркетинг и продвижение** — версия `promotion`

<div class="description_important">
  Узнать больше о маркетинге и продвижении можно в <a href="https://seller.wildberries.ru/instructions/category/59d92bd3-6ea0-40f2-b762-ca8835d7d42e?goBackOption=prevRoute&categoryId=479385c6-de01-4b4d-ad4e-ed941e65582e">справочном центре</a>
</div>

Методы маркетинга и продвижения позволяют:
  1. Получать информацию о кампаниях [продвижения](./promotion#tag/Kampanii) и [медиакампаниях](./promotion#tag/Media).
  2. [Создавать](./promotion#tag/Sozdanie-kampanij) и [управлять](./promotion#tag/Upravlenie-kampaniyami) кампаниями.
  3. Управлять [финансами](./promotion#tag/Finansy) кампаний.
  4. Выгружать [статистику](./promotion#tag/Statistika) кампаний продвижения и медиакампаний.
  5. Работать с [календарём акций](./promotion#tag/Kalendar-akcij).

Данные синхронизируются с базой раз в 3 минуты. Статусы кампаний меняются раз в минуту. Ставки кампаний меняются раз в 30 секунд.

## Разделы (tags)
- [Маркетинг и продвижение](tags/Маркетинг и продвижение.md)
- [Кампании](tags/Кампании.md)
- [Создание кампаний](tags/Создание кампаний.md)
- [Управление кампаниями](tags/Управление кампаниями.md)
- [Поисковые кластеры](tags/Поисковые кластеры.md)
- [Финансы](tags/Финансы.md)
- [Медиа](tags/Медиа.md)
- [Статистика](tags/Статистика.md)
- [Календарь акций](tags/Календарь акций.md)

## Эндпоинты
- [`GET /adv/v1/promotion/count` — Списки кампаний{{ /adv/v1/promotion/count }}](operations/GET adv-v1-promotion-count.md)
- [`GET /api/advert/v2/adverts` — Информация о кампаниях{{ /api/advert/v2/adverts }}](operations/GET api-advert-v2-adverts.md)
- [`POST /api/advert/v1/bids/min` — Минимальные ставки для карточек товаров{{ /api/advert/v1/bids/min }}](operations/POST api-advert-v1-bids-min.md)
- [`POST /adv/v2/seacat/save-ad` — Создать кампанию{{ /adv/v2/seacat/save-ad }}](operations/POST adv-v2-seacat-save-ad.md)
- [`GET /adv/v1/supplier/subjects` — Предметы для кампаний{{ /adv/v1/supplier/subjects }}](operations/GET adv-v1-supplier-subjects.md)
- [`POST /adv/v2/supplier/nms` — Карточки товаров для кампаний{{ /adv/v2/supplier/nms }}](operations/POST adv-v2-supplier-nms.md)
- [`GET /adv/v0/delete` — Удаление кампании{{ /adv/v0/delete }}](operations/GET adv-v0-delete.md)
- [`POST /adv/v0/rename` — Переименование кампании{{ /adv/v0/rename }}](operations/POST adv-v0-rename.md)
- [`GET /adv/v0/start` — Запуск кампании{{ /adv/v0/start }}](operations/GET adv-v0-start.md)
- [`GET /adv/v0/pause` — Пауза кампании{{ /adv/v0/pause }}](operations/GET adv-v0-pause.md)
- [`GET /adv/v0/stop` — Завершение кампании{{ /adv/v0/stop }}](operations/GET adv-v0-stop.md)
- [`PUT /adv/v0/auction/placements` — Изменение мест размещения в кампаниях с ручной ставкой{{ /adv/v0/auction/placements }}](operations/PUT adv-v0-auction-placements.md)
- [`PATCH /api/advert/v1/bids` — Изменение ставок в кампаниях{{ /api/advert/v1/bids }}](operations/PATCH api-advert-v1-bids.md)
- [`GET /adv/v1/balance` — Баланс{{ /adv/v1/balance }}](operations/GET adv-v1-balance.md)
- [`GET /adv/v1/budget` — Бюджет кампании{{ /adv/v1/budget }}](operations/GET adv-v1-budget.md)
- [`POST /adv/v1/budget/deposit` — Пополнение бюджета кампании{{ /adv/v1/budget/deposit }}](operations/POST adv-v1-budget-deposit.md)
- [`GET /adv/v1/upd` — Получение истории затрат{{ /adv/v1/upd }}](operations/GET adv-v1-upd.md)
- [`GET /adv/v1/payments` — Получение истории пополнений счёта{{ /adv/v1/payments }}](operations/GET adv-v1-payments.md)
- [`PATCH /adv/v0/auction/nms` — Изменение списка карточек товаров в кампаниях{{ /adv/v0/auction/nms }}](operations/PATCH adv-v0-auction-nms.md)
- [`GET /api/advert/v0/bids/recommendations` — Рекомендуемые ставки для карточек товаров и поисковых кластеров{{ /api/advert/v0/bids/recommendations }}](operations/GET api-advert-v0-bids-recommendations.md)
- [`POST /adv/v0/normquery/stats` — Статистика поисковых кластеров{{ /adv/v0/normquery/stats }}](operations/POST adv-v0-normquery-stats.md)
- [`POST /adv/v0/normquery/get-bids` — Список ставок поисковых кластеров{{ /adv/v0/normquery/get-bids }}](operations/POST adv-v0-normquery-get-bids.md)
- [`POST /adv/v0/normquery/bids` — Установить ставки для поисковых кластеров{{ /adv/v0/normquery/bids }}](operations/POST adv-v0-normquery-bids.md)
- [`DELETE /adv/v0/normquery/bids` — Удалить ставки поисковых кластеров{{ /adv/v0/normquery/bids }}](operations/DELETE adv-v0-normquery-bids.md)
- [`POST /adv/v0/normquery/get-minus` — Список минус-фраз кампаний{{ /adv/v0/normquery/get-minus }}](operations/POST adv-v0-normquery-get-minus.md)
- [`POST /adv/v0/normquery/set-minus` — Установка и удаление минус-фраз{{ /adv/v0/normquery/set-minus }}](operations/POST adv-v0-normquery-set-minus.md)
- [`GET /adv/v1/count` — Количество медиакампаний{{ /adv/v1/count }}](operations/GET adv-v1-count.md)
- [`GET /adv/v1/adverts` — Список медиакампаний{{ /adv/v1/adverts }}](operations/GET adv-v1-adverts.md)
- [`GET /adv/v1/advert` — Информация о медиакампании{{ /adv/v1/advert }}](operations/GET adv-v1-advert.md)
- [`GET /adv/v3/fullstats` — Статистика кампаний{{ /adv/v3/fullstats }}](operations/GET adv-v3-fullstats.md)
- [`POST /adv/v1/stats` — Статистика медиакампаний{{ /adv/v1/stats }}](operations/POST adv-v1-stats.md)
- [`GET /api/v1/calendar/promotions` — Список акций{{ /api/v1/calendar/promotions }}](operations/GET api-v1-calendar-promotions.md)
- [`GET /api/v1/calendar/promotions/details` — Детальная информация об акциях{{ /api/v1/calendar/promotions/details }}](operations/GET api-v1-calendar-promotions-details.md)
- [`GET /api/v1/calendar/promotions/nomenclatures` — Список товаров для участия в акции{{ /api/v1/calendar/promotions/nomenclatures }}](operations/GET api-v1-calendar-promotions-nomenclatures.md)
- [`POST /api/v1/calendar/promotions/upload` — Добавить товар в акцию{{ /api/v1/calendar/promotions/upload }}](operations/POST api-v1-calendar-promotions-upload.md)
- [`POST /adv/v0/normquery/list` — Списки активных и неактивных поисковых кластеров{{ /adv/v0/normquery/list }}](operations/POST adv-v0-normquery-list.md)
- [`POST /adv/v1/normquery/stats` — Статистика по поисковым кластерам с детализацией по дням{{ /adv/v1/normquery/stats }}](operations/POST adv-v1-normquery-stats.md)
