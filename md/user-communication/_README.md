# user-communication

**Общение с покупателями** — версия `communication`

<div class="description_important">
  Узнать больше об общении с покупателями можно в <a href="https://seller.wildberries.ru/instructions/category/f7f6c465-dd12-422d-80a0-a6d9562115d5?goBackOption=prevRoute&categoryId=30817062-14cc-4a82-bc78-3600c2b0685b">справочном центре</a>
</div>

С помощью методов общения с покупателями вы можете работать с:
  1. [Вопросами](./user-communication#tag/Voprosy) и [отзывами](./user-communication#tag/Otzyvy) покупателей
  2. [Закреплёнными отзывами](./user-communication#tag/Zakreplyonnye-otzyvy)
  3. [Чатами с покупателями](./user-communication#tag/Chat-s-pokupatelyami)
  4. [Заявками покупателей на возврат](./user-communication#tag/Vozvraty-pokupatelyami)

  <div class="description_ref">
    Узнать, как использовать методы в бизнес-кейсах, можно в <a href="https://dev.wildberries.ru/knowledge-base/articles/019d49a4-0b26-7620-8d0b-e3050b7cd01d/obshchenie-s-pokupateliami">инструкции</a> по работе с разделом <strong>Общение с покупателями</strong>
  </div>

## Разделы (tags)
- [Общение с покупателями](tags/Общение с покупателями.md)
- [Вопросы](tags/Вопросы.md)
- [Отзывы](tags/Отзывы.md)
- [Закреплённые отзывы](tags/Закреплённые отзывы.md)
- [Чат с покупателями](tags/Чат с покупателями.md)
- [Возвраты покупателями](tags/Возвраты покупателями.md)

## Эндпоинты
- [`GET /api/v1/new-feedbacks-questions` — Непросмотренные отзывы и вопросы{{ /api/v1/new-feedbacks-questions }}](operations/GET api-v1-new-feedbacks-questions.md)
- [`GET /api/v1/questions/count-unanswered` — Неотвеченные вопросы{{ /api/v1/questions/count-unanswered }}](operations/GET api-v1-questions-count-unanswered.md)
- [`GET /api/v1/questions/count` — Количество вопросов{{ /api/v1/questions/count }}](operations/GET api-v1-questions-count.md)
- [`GET /api/v1/questions` — Список вопросов{{ /api/v1/questions }}](operations/GET api-v1-questions.md)
- [`PATCH /api/v1/questions` — Работа с вопросами{{ /api/v1/questions }}](operations/PATCH api-v1-questions.md)
- [`GET /api/v1/question` — Получить вопрос по ID{{ /api/v1/question }}](operations/GET api-v1-question.md)
- [`GET /api/v1/feedbacks/count-unanswered` — Необработанные отзывы{{ /api/v1/feedbacks/count-unanswered }}](operations/GET api-v1-feedbacks-count-unanswered.md)
- [`GET /api/v1/feedbacks/count` — Количество отзывов{{ /api/v1/feedbacks/count }}](operations/GET api-v1-feedbacks-count.md)
- [`GET /api/v1/feedbacks` — Список отзывов{{ /api/v1/feedbacks }}](operations/GET api-v1-feedbacks.md)
- [`POST /api/v1/feedbacks/answer` — Ответить на отзыв{{ /api/v1/feedbacks/answer }}](operations/POST api-v1-feedbacks-answer.md)
- [`PATCH /api/v1/feedbacks/answer` — Отредактировать ответ на отзыв{{ /api/v1/feedbacks/answer }}](operations/PATCH api-v1-feedbacks-answer.md)
- [`POST /api/v1/feedbacks/order/return` — Возврат товара по ID отзыва{{ /api/v1/feedbacks/order/return }}](operations/POST api-v1-feedbacks-order-return.md)
- [`GET /api/v1/feedback` — Получить отзыв по ID{{ /api/v1/feedback }}](operations/GET api-v1-feedback.md)
- [`GET /api/v1/feedbacks/archive` — Список архивных отзывов{{ /api/v1/feedbacks/archive }}](operations/GET api-v1-feedbacks-archive.md)
- [`GET /api/feedbacks/v1/pins` — Список закреплённых и откреплённых отзывов{{ /api/feedbacks/v1/pins }}](operations/GET api-feedbacks-v1-pins.md)
- [`POST /api/feedbacks/v1/pins` — Закрепить отзывы{{ /api/feedbacks/v1/pins }}](operations/POST api-feedbacks-v1-pins.md)
- [`DELETE /api/feedbacks/v1/pins` — Открепить отзывы{{ /api/feedbacks/v1/pins }}](operations/DELETE api-feedbacks-v1-pins.md)
- [`GET /api/feedbacks/v1/pins/count` — Количество закреплённых и откреплённых отзывов{{ /api/feedbacks/v1/pins/count }}](operations/GET api-feedbacks-v1-pins-count.md)
- [`GET /api/feedbacks/v1/pins/limits` — Лимиты закреплённых отзывов{{ /api/feedbacks/v1/pins/limits }}](operations/GET api-feedbacks-v1-pins-limits.md)
- [`GET /api/v1/seller/chats` — Список чатов{{ /api/v1/seller/chats }}](operations/GET api-v1-seller-chats.md)
- [`GET /api/v1/seller/events` — События чатов{{ /api/v1/seller/events }}](operations/GET api-v1-seller-events.md)
- [`POST /api/v1/seller/message` — Отправить сообщение{{ /api/v1/seller/message }}](operations/POST api-v1-seller-message.md)
- [`GET /api/v1/seller/download/{id}` — Получить файл из сообщения{{ /api/v1/seller/download/{id} }}](operations/GET api-v1-seller-download-{id}.md)
- [`GET /api/v1/claims` — Заявки покупателей на возврат{{ /api/v1/claims }}](operations/GET api-v1-claims.md)
- [`PATCH /api/v1/claim` — Ответ на заявку покупателя{{ /api/v1/claim }}](operations/PATCH api-v1-claim.md)
