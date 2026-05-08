# Поставки FBS

Для доступа к методам используйте <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токен</a> для категории <strong>Маркетплейс</strong>

  Узнать больше о поставках FBS можно в <a href="https://seller.wildberries.ru/instructions/material/A-11?goBackOption=prevRoute&categoryId=6d85301c-719b-4145-9275-2ac8b793f345">справочном центре</a>

Для работы с поставками:

  Пункты 3-5 обязательны к выполнению при доставке поставки на пункт выдачи заказов (ПВЗ).

  1. [Создайте новую поставку](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies/post). В ответ вернется ID созданной поставки в формате `WB-GI-1234567`.
  2. В текущую новую поставку [добавьте сборочные задания](./orders-fbs#tag/Postavki-FBS/paths/~1api~1marketplace~1v3~1supplies~1%7BsupplyId%7D~1orders/patch), которые вы повезёте на склад или ПВЗ. После того, как сборочные задания будут добавлены к поставке, они будут переведены в статус `confirm` — на сборке.
  3. [Добавьте грузоместа в поставку](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1trbx/post).
  4. [Проверьте список грузомест](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1trbx/get).
  5. [Получите стикеры грузомест](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1trbx~1stickers/post). Распечатайте и наклейте стикеры на грузоместа.
  6. После того как поставка будет укомплектована нужными сборочными заданиями, необходимо [передать её в доставку](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1deliver/patch). Если поставка не была передана в доставку, то при сканировании её QR-кода или приёмке первого товара на ПВЗ поставка автоматически закроется. При передаче сборочных заданий в доставку они будут автоматически собраны и переведены в статус `complete` — в доставке.
  7. Если поставка была отсканирована в пункте приёмки, но при этом в ней всё ещё есть неотсканированные товары, спустя определённое время необходимо доставить их повторно. Проверьте все [сборочные задания, требующие повторной отгрузки на данный момент](./orders-fbs#tag/Sborochnye-zadaniya-FBS/paths/~1api~1v3~1supplies~1orders~1reshipment/get). Данные сборочные задания можно перевести в [другую активную поставку](./orders-fbs#tag/Postavki-FBS/paths/~1api~1marketplace~1v3~1supplies~1%7BsupplyId%7D~1orders/patch). Сборочное задание также будет переведено в статус `confirm` — на сборке.

  Также вы можете:
  1. [Удалить грузоместа из поставки](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1trbx/delete), но только пока поставка находится на сборке.
  2. Получить [список всех сборочных заданий, добавленных к поставке](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1orders/get).
  3. Получить информацию [обо всех поставках продавца](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies/get) или [о конкретной поставке](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D/get).
  4. [Удалить поставку](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D/delete) при условии, что она активна и за ней не закреплены сборочные задания.
  5. [Перемещать сборочные задания между активными поставками](./orders-fbs#tag/Postavki-FBS/paths/~1api~1marketplace~1v3~1supplies~1%7BsupplyId%7D~1orders/patch). Нельзя перемещать сборочное задание из уже закрытой поставки, только если оно не требует повторной отгрузки.
  6. Получить [QR-код поставки](./orders-fbs#tag/Postavki-FBS/paths/~1api~1v3~1supplies~1%7BsupplyId%7D~1barcode/get) в форматах SVG, ZPL или PNG. Доступно только после передачи поставки в доставку.
