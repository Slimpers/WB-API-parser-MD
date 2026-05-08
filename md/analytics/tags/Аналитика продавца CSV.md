# Аналитика продавца CSV

Для доступа к методам используйте <a href="./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token">токен</a> для категории <strong>Аналитика</strong>

  Узнать, как использовать методы в бизнес-кейсах, можно в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a3-f76b-7f22-82f3-54930b8f59e8/analitika-prodavtsa-csv">инструкции</a> по работе с <strong>Аналитикой продавца CSV</strong>

Чтобы получить отчёт:
  1. Сгенерируйте его с помощью метода [создания отчёта](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads/post).
  2. Дождитесь, когда отчёт будет готов. Вы можете проверить статус готовности через [получение списка отчётов](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads/get). Готовый отчёт хранится 48 часов.

  Если вы получили статус `FAILED`, [сгенерируйте отчёт повторно](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads~1retry/post).
  3. [Получите отчёт](./analytics#tag/Analitika-prodavca-CSV/paths/~1api~1v2~1nm-report~1downloads~1file~1%7BdownloadId%7D/get).

Можно получить отчёт максимум за год. Отчёты по остаткам — за 3 месяца.

Максимальное количество отчётов, генерируемых в сутки — 20.

  Вы можете использовать эти методы — за исключением отчётов по остаткам — только с подпиской <a href='https://seller.wildberries.ru/monetization/jam'>Джем</a>
