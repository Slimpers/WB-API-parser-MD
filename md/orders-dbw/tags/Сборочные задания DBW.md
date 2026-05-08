# Сборочные задания DBW

<div class="description_auth">
  Для доступа к методам используйте <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токен</a> для категории <strong>Маркетплейс</strong>
</div>

Для работы со сборочными заданиями DBW:
1. [Получите новое сборочное задание](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1new/get).
2. [Переведите его на сборку](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1confirm/patch).
3. После перевода на сборку для заказа становится доступной [информация о курьере](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1courier/post) (телефон, номер автомобиля).
<br>Чтобы курьер мог связаться с вами [привяжите](./work-with-products#tag/Sklady-prodavca/paths/~1api~1v3~1dbw~1warehouses~1%7BwarehouseId%7D~1contacts/put) свои контакты к складу. Вы так же можете [получить](./work-with-products#tag/Sklady-prodavca/paths/~1api~1v3~1dbw~1warehouses~1%7BwarehouseId%7D~1contacts/get) текущий список своих контактов.
4. [Получите](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1v3~1dbw~1orders~1stickers/post), распечатайте и прикрепите стикеры.
5. [Переведите сборочное задание в доставку](./orders-dbw#tag/Sborochnye-zadaniya-DBW/paths/~1api~1marketplace~1v3~1dbw~1orders~1status~1deliver/post).
6. Дождитесь курьера.
7. Курьер забирает заказ и отвозит клиенту.
8. Клиент принимает заказ или отказывается от него.
9. Если клиент принимает заказ, курьер переводит сборочное задание в статус `receive`. Если отказывается — в `reject`.

  <div class="description_important">
    Узнать больше о сборочных заданиях DBW можно в <a href="https://seller.wildberries.ru/help-center/category/01956ff5-e134-74f3-a798-24b6b49a403b">справочном центре</a>
  </div>
