# api-information

**Общее** — версия `general`

В этом разделе:
  - [общая информация о WB API](./api-information#tag/Vvedenie)
  - как [начать работу с WB API](./api-information#tag/Vvedenie/Kak-nachat-rabotu-s-API)
  - как [авторизоваться](./api-information#tag/Avtorizaciya) и [создавать токены](./api-information#tag/Avtorizaciya/Kak-sozdat-personalnyj-bazovyj-ili-testovyj-token)
  - основные [статус-коды ответов](./api-information#tag/Vvedenie/Status-kody-HTTP)
  - [лимиты запросов](./api-information#tag/Vvedenie/Limity-zaprosov)
  - как обратиться в [поддержку](./api-information#tag/Vvedenie/Podderzhka)

С помощью методов этого раздела вы можете:
  - проверить [подключение к WB API](./api-information#tag/Proverka-podklyucheniya-k-WB-API/paths/~1ping/get)
  - получить [новости портала продавцов](./api-information#tag/API-novostej/paths/~1api~1communications~1v2~1news/get)
  - получить [информацию о продавце](./api-information#tag/Informaciya-o-prodavce/paths/~1api~1v1~1seller-info/get)
  - [управлять пользователями продавца](./api-information#tag/Upravlenie-polzovatelyami-prodavca)

## Разделы (tags)
- [Общее](tags/Общее.md)
- [Введение](tags/Введение.md)
- [Авторизация](tags/Авторизация.md)
- [Проверка подключения к WB API](tags/Проверка подключения к WB API.md)
- [API новостей](tags/API новостей.md)
- [Информация о продавце](tags/Информация о продавце.md)
- [Управление пользователями продавца](tags/Управление пользователями продавца.md)

## Эндпоинты
- [`GET /ping` — Проверка подключения{{ /ping }}](operations/GET ping.md)
- [`GET /api/communications/v2/news` — Получение новостей портала продавцов{{ /api/communications/v2/news }}](operations/GET api-communications-v2-news.md)
- [`GET /api/v1/seller-info` — Получить информацию о продавце{{ /api/v1/seller-info }}](operations/GET api-v1-seller-info.md)
- [`GET /api/common/v1/rating` — Получить рейтинг продавца{{ /api/common/v1/rating }}](operations/GET api-common-v1-rating.md)
- [`GET /api/common/v1/subscriptions` — Получить информацию о подписке Джем{{ /api/common/v1/subscriptions }}](operations/GET api-common-v1-subscriptions.md)
- [`POST /api/v1/invite` — Создать приглашение для нового пользователя{{ /api/v1/invite }}](operations/POST api-v1-invite.md)
- [`GET /api/v1/users` — Получить список активных или приглашённых пользователей продавца{{ /api/v1/users }}](operations/GET api-v1-users.md)
- [`PUT /api/v1/users/access` — Изменить права доступа пользователей{{ /api/v1/users/access }}](operations/PUT api-v1-users-access.md)
- [`DELETE /api/v1/user` — Удалить пользователя{{ /api/v1/user }}](operations/DELETE api-v1-user.md)
