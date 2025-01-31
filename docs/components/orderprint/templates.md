# orderPrint

У каждого документа может быть 2 шаблона, шаблон всего документа и шаблон строки таблицы с информацией по отдельному товару из заказа. Шаблон всего документа обязателен, если он не указан ничего работать не будет, шаблон строки таблицы не обязателен, если он не указан просто не будет самой таблицы, которая не обязательно нужна в каждом документе.

Так как для формирования документов используются обычные элементы MODX Вы смело можете в шаблонах использовать системные настройки, сниппеты, фильтры, другие чанки и так далее.

::: warning
Класс используемый для преобразования html в pdf, далек по своим возможностям от интерпретаторов в браузерах. Так что не нужно стеснятся использовать атрибут style прямо в тегах, стоит избегать применять html5 и css3 а также лучше предпочтение отдать табличной вёрстке при подготовке шаблонов.
:::

## Плейсхолдеры доступные в шаблоне изначально

Шаблон всего документа (MiniShop2)

| Плейсхлолдер                   | Значение                                                                |
| ------------------------------ | ----------------------------------------------------------------------- |
| `[[+id]]`                      | id заказа                                                               |
| `[[+num]]`                     | номер заказа                                                            |
| `[[+createdon]]`               | дата создания                                                           |
| `[[+status]]`                  | название статуса заказа (новый, оплочен и т.д.)                         |
| `[[+weight]]`                  | общий вес товаров в заказе                                              |
| `[[+comment]]`                 | комментарий к заказу                                                    |
| `[[+delivery_cost]]`           | стоимость доставки                                                      |
| `[[+cart_cost]]`               | стоимость без доставки                                                  |
| `[[+payment_price]]`           | комиссия при использовании выбранного способа оплаты                    |
| `[[+cost]]`                    | стоимость с доставкой                                                   |
| `[[+delivery]]`                | название способа доставки                                               |
| `[[+payment]]`                 | название способа оплаты                                                 |
| `[[+payment_description]]`     | описание способа оплаты                                                 |
| `[[+cart]]`                    | УЖЕ СФОРМИРОВАННЫЙ html таблицы с товарами                              |
| `[[+manager]]`                 | полное имя пользователя, который печатает документ                      |
| `[[+print_date]]`              | текущая дата                                                            |
| `[[+properties.ключ]]`         | дополнительные опции заказа                                             |
| `[[+address]]`                 | id адреса                                                               |
| `[[+address.receiver]]`        | имя покупателя указанное при оформлении заказа                          |
| `[[+address.phone]]`           | телефон покупателя указанный при оформлении заказа                      |
| `[[+address.room]]`            | номер квартиры/офиса покупателя указанный при оформлении заказа         |
| `[[+address.building]]`        | номер дома покупателя указанный при оформлении заказа                   |
| `[[+address.street]]`          | улица покупателя указанная при оформлении заказа                        |
| `[[+address.metro]]`           | станция метро покупателя указанная при оформлении заказа                |
| `[[+address.city]]`            | город покупателя указанный при оформлении заказа                        |
| `[[+address.region]]`          | регион указанный при оформлении заказа                                  |
| `[[+address.index]]`           | почтовый индекс покупателя указанный при оформлении заказа              |
| `[[+address.country]]`         | страна покупателя указанная при оформлении заказа                       |
| `[[+address.comment]]`         | комментарий указанный при оформлении заказа                             |
| `[[+address.properties.ключ]]` | дополнительные опции записанные при оформлении заказа в поле properties |
| `[[+user.id]]`                 | id покупателя                                                           |
| `[[+user.fullname]]`           | полное имя покупателя из профиля                                        |
| `[[+user.username]]`           | имя пользователя покупателя из профиля                                  |
| `[[+user.email]]`              | email покупателя из профиля                                             |
| `[[+user.phone]]`              | телефон покупателя из профиля                                           |
| `[[+user.mobilephone]]`        | мобильный телефон покупателя из профиля                                 |
| `[[+user.fax]]`                | номер факса покупателя из профиля                                       |
| `[[+user.gender]]`             | пол покупателя из профиля                                               |
| `[[+user.address]]`            | адрес покупателя из профиля                                             |
| `[[+user.zip]]`                | почтовый индекс покупателя из профиля                                   |
| `[[+user.state]]`              | регион покупателя из профиля                                            |
| `[[+user.city]]`               | город покупателя из профиля                                             |
| `[[+user.country]]`            | страна покупателя из профиля                                            |
| `[[+user.photo]]`              | фото\\аватар покупателя из профиля                                      |
| `[[+user.comment]]`            | комментарий к учетной записи покупателя                                 |
| `[[+user.website]]`            | url сайта покупателя из профиля                                         |
| `[[+user.extended.ключ]]`      | дополнительные поля профиля пользователя                                |
| `[[+settings.ключ]]`           | дополнительные параметры компонента, указанные на вкладке "Параметры"   |

Шаблон строки с информацией об отдельном товаре из заказа (MiniShop2)

| Плейсхлолдер        | Значение                                                         |
| ------------------- | ---------------------------------------------------------------- |
| `[[+id]]`           | id товара                                                        |
| `[[+price]]`        | цена товара                                                      |
| `[[+count]]`        | количество купленного товара                                     |
| `[[+cost]]`         | общая стоимость позиции                                          |
| `[[+weight]]`       | вес                                                              |
| `[[+pagetitle]]`    | заголовок ресурса-товара                                         |
| `[[+thumb]]`        | превью фотографии товара                                         |
| `[[+article]]`      | артикул                                                          |
| `[[+options.ключ]]` | дополнительные параметры купленного товара (цвет, размер и т.д.) |

Шаблон всего документа (Shopkeeper)

| Плейсхлолдер                 | Значение                                                              |
| ---------------------------- | --------------------------------------------------------------------- |
| `[[+id]]`                    | id заказа                                                             |
| `[[+date]]`                  | дата создания                                                         |
| `[[+sentdate]]`              | дата отправки                                                         |
| `[[+status]]`                | название статуса заказа (новый, оплочен и т.д.)                       |
| `[[+delivery_cost]]`         | стоимость доставки                                                    |
| `[[+price]]`                 | стоимость с доставкой                                                 |
| `[[+currency]]`              | валюта                                                                |
| `[[+delivery]]`              | название способа доставки                                             |
| `[[+payment]]`               | название способа оплаты                                               |
| `[[+cart]]`                  | УЖЕ СФОРМИРОВАННЫЙ html таблицы с товарами                            |
| `[[+manager]]`               | полное имя пользователя, который печатает документ                    |
| `[[+print_date]]`            | текущая дата                                                          |
| `[[+email]]`                 | email покупателя                                                      |
| `[[+phone]]`                 | телефон покупателя                                                    |
| `[[+note]]`                  | комментарий к заказу                                                  |
| `[[+tracking_num]]`          | трекинг-номер (почтовый идентификатор, номер отслеживания)            |
| `[[+contacts.fullname]]`     | имя покупателя, указанное при оформлении заказа                       |
| `[[+contacts.zip]]`          | почтовый индекс покупателя, указанный при оформлении заказа           |
| `[[+contacts.phone]]`        | телефон покупателя, указанный при оформлении заказа                   |
| `[[+contacts.email]]`        | email покупателя, указанный при оформлении заказа                     |
| `[[+contacts.room]]`         | квартира/офис покупателя, указанный при оформлении заказа             |
| `[[+contacts.house]]`        | номер дома покупателя, указанный при оформлении заказа                |
| `[[+contacts.corpus]]`       | корпус указанный при оформлении заказа                                |
| `[[+contacts.street]]`       | улица, указанная при оформлении заказа                                |
| `[[+contacts.metro]]`        | станция метро, указанный при оформлении заказа                        |
| `[[+contacts.city]]`         | город покупателя, указанный при оформлении заказа                     |
| `[[+contacts.state]]`        | страна указанная при оформлении заказа                                |
| `[[+contacts.payment]]`      | название способа оплаты                                               |
| `[[+contacts.shk_delivery]]` | название способа оплаты                                               |
| `[[+contacts.message]]`      | комментарий пользователя к заказу                                     |
| `[[+contacts.ключ]]`         | любые данные записанные в поле contacts в таблице в БД                |
| `[[+user.fullname]]`         | полное имя покупателя из профиля                                      |
| `[[+user.username]]`         | имя пользователя покупателя из профиля                                |
| `[[+user.email]]`            | email покупателя из профиля                                           |
| `[[+user.phone]]`            | телефон покупателя из профиля                                         |
| `[[+user.mobilephone]]`      | мобильный телефон покупателя из профиля                               |
| `[[+user.fax]]`              | номер факса покупателя из профиля                                     |
| `[[+user.gender]]`           | пол покупателя из профиля                                             |
| `[[+user.address]]`          | адрес покупателя из профиля                                           |
| `[[+user.zip]]`              | почтовый индекс покупателя из профиля                                 |
| `[[+user.state]]`            | регион покупателя из профиля                                          |
| `[[+user.city]]`             | город покупателя из профиля                                           |
| `[[+user.country]]`          | страна покупателя из профиля                                          |
| `[[+user.photo]]`            | фото\\аватар покупателя из профиля                                    |
| `[[+user.comment]]`          | комментарий к учетной записи покупателя                               |
| `[[+user.website]]`          | url сайта покупателя из профиля                                       |
| `[[+user.extended.ключ]]`    | дополнительные поля профиля пользователя                              |
| `[[+settings.ключ]]`         | дополнительные параметры компонента, указанные на вкладке "Параметры" |

Шаблон строки с информацией об отдельном товаре из заказа (ShopKeeper)

| Плейсхлолдер                   | Значение                            |
| ------------------------------ | ----------------------------------- |
| `[[+id]]`                      | id товара                           |
| `[[+price]]` и `[[+tv.price]]` | цена товара                         |
| `[[+count]]`                   | количество купленного товара        |
| `[[+cost]]`                    | общая стоимость позиции             |
| `[[+link]]`                    | ссылка на товар                     |
| `[[+name]]`                    | заголовок ресурса-товара            |
| `[[+tv_add.имя TV]]`           | значения TV прикрепленных к ресурсу |
