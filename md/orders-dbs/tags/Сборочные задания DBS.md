# Сборочные задания DBS

<div class="description_auth">
  Для доступа к методам используйте <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токен</a> для категории <strong>Маркетплейс</strong>
</div>

<div class="description_ref">
  Узнать, как использовать методы в бизнес-кейсах, можно в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a3-ff7d-70ba-a872-828430b24ea1/zakazy-dbs">инструкции</a> по работе с <strong>заказами DBS</strong>
</div>

<div class="description_important">
  Узнать больше о сборочных заданиях DBS можно в <a href="https://seller.wildberries.ru/instructions/material/A-108?goBackOption=prevRoute&categoryId=0fc94a39-22b1-4a54-8ef2-06dac1d8137b">справочном центре</a>
</div>

Для работы со сборочными заданиями DBS:
1. [Получите новое сборочное задание](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1v3~1dbs~1orders~1new/get) и сохраните его до перевода на сборку. Если вы не сохраните информацию о сборочном задании заранее, вы сможете получить ее только после завершения задания (отмены или продажи). Проверяйте [дату и время доставки](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1v3~1dbs~1orders~1delivery-date/post).
2. [Переведите его на сборку](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1confirm/post).
3. После перевода на сборку для заказа становится доступной [информация о покупателе](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1v3~1dbs~1orders~1client/post) (имя, телефон).
4. [Переведите в доставку](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1deliver/post).
5. После доставки задания покупателю вам необходимо сообщить на наш сервер, что [сборочное задание принято](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1receive/post) покупателем или, что [покупатель отказался от сборочного задания](./orders-dbs#tag/Sborochnye-zadaniya-DBS/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1reject/post).
