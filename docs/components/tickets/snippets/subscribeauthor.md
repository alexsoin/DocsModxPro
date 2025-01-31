# subscribeAuthor

Выводит форму подписки на автора. Подписка доступна только для авторизованных пользователей.

## Параметры

| Название         | По умолчанию                   | Описание                                                                                                                                                                                           |
| ---------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **&createdby**   | `0`                            | Обязательный параметр, ID автора (user), на которого будет осуществляться подписка через форму                                                                                                     |
| **&tpl**         | `tpl.Tickets.author.subscribe` | Чанк с формой подписки                                                                                                                                                                             |
| **&TicketsInit** | `0`                            | Параметр использовать со значением «1» для подключения формы подписки и инциализации frontend-скриптов Tickets на произвольных страницах сайта (например, карточка автора, личный кабинет и т.п.). |

## Примеры

- Вызов сниппета для каждого элемента в списке тикетов, например в чанке tpl.Tickets.list.row

    ```modx
    [[!subscribeAuthor? &createdby=`[[!+createdby]]`]]
    ```

- Вызов сниппета в карточке автора (в которой ID юзера передан в переменную +author.id )

    ```modx
    [[!subscribeAuthor? &createdby=`[[!+author.id]]` &TicketsInit=`1`]]
    ```
