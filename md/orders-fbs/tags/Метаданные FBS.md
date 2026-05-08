# Метаданные FBS

<div class="description_auth">
  Для доступа к методам используйте <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токен</a> для категории <strong>Маркетплейс</strong>
</div>

<div class="description_important">
  Узнать больше о метаданных можно в <a href="https://seller.wildberries.ru/instructions/material/A-305?goBackOption=prevRoute&categoryId=6d85301c-719b-4145-9275-2ac8b793f345">справочном центре</a>
</div>

С помощью этих методов вы можете [получать](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1marketplace~1v3~1orders~1meta/post), [удалять](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta/delete) и редактировать метаданные [сборочных заданий](./orders-fbs#tag/Sborochnye-zadaniya-FBS):
  - [Код маркировки Честного знака](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1sgtin/put)
  - [УИН](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1uin/put)
  - [IMEI](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1imei/put)
  - [GTIN](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1gtin/put)
  - [Срок годности товара](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1v3~1orders~1%7BorderId%7D~1meta~1expiration/put)
  - [Номер ГТД](./orders-fbs#tag/Metadannye-FBS/paths/~1api~1marketplace~1v3~1orders~1%7BorderId%7D~1meta~1customs-declaration/put)
