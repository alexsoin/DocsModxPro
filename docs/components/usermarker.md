---
title: userMarker
description: Добавление меток и тегов к ресурсам
logo: https://modstore.pro/assets/extras/usermarker/logo-lg.png
author: webnitros
modstore: https://modstore.pro/packages/ecommerce/usermarker
---
# userMarker

Платный компонент предназначен для добавления меток к ресурсам.

- [Демо-версия](http://usermarker.bustep.ru/demo.html)
- [Видео с демонстрацией](https://www.youtube.com/watch?v=0nksuTp1spQ)
- [Купить](https://modstore.pro/packages/ecommerce/usermarker)

## Основные особенности

- Можно назначать метки не только ресурсам но и другим любым объектам. Для этого нужно задавать свой classKey для кнопки
- Так же учитывается контекст откуда был добавлен ресурс (можно отключить)
- Возможность вывода отмеченых ресурсов пользователя через сниппет ``[[!userMarker.Resource? &label=`Проверен`]]`` с указанием нужной метки
- Управление созданными метками через личный кабинет
- Управление правами приложения. Возможность назначить права управления метками только определенным группа и контектам. Шаблон политики доступа **userMarker**

## Быстрый старт

### Инициализация скриптов

Подключаем сниппет на страницу для инициализации скриптов js и css (вставить в верхнюю часть сайта)

```modx
[[!userMarker.Initialize]]
```

### Список меток

Вставляем сниппет с метками и кнопкой добавить метку

```modx
[[!userMarker.Label]]
```

#### Чанк для ресурса

пример **tpl.userMarker.resource.row**

```modx
<h3>[[+pagetitle]]</h3>
[[!userMarker.Record? &resource_id=`[[+id]]`]]
```

#### Вывод списка ресурсов

Добавить на страницу для вывода отмеченых ресурсов

```modx
[[!pdoPage?
  &element=`userMarker.Resource`
]]

[[!+page.nav]]
```

Или с помощью pdoResources

```modx
[[!pdoResources?
  &tpl=`tpl.userMarker.resource.row`
  &innerJoin=`{
    "Marker": {
      "class": "userMarkerResource",
      "on": "modResource.id=Marker.resource_id"
    }
  }`
]]
```

Вывод списка ресурсов с указанием метки

```modx
[[!pdoPage?
  &label=`Имя метки`
  &element=`userMarker.Resource`
]]

[[!+page.nav]]
```

### Управление метками

Вставить на страницу для авторизованного пользователя.

```modx
[[!userMarker.label?
  &tpl=`tpl.userMarker.manager.row`
  &tplOuter=`tpl.userMarker.manager.outer`
]]
```

### Переназначения js для модельного окна

Добавлены события для js modal

```js
// Событие для открытия модельного окна
userMarker.Modal.show = function () {
  // Сюда можно прописать свой скрипт запуска модельного окна
  $(userMarker.options.modal).modal('show');

  // После закрытия автоматически стерам данные
  $(userMarker.options.modal).on('hidden.bs.modal', function (e) {
    userMarker.removeModal();
  });
};

// Событие для закрытия модельного окна
userMarker.Modal.hide = function () {
  if ($(userMarker.options.modal).length) {
    // Сюда можно прописать свой скрипт закрытия модельного окна
    $(userMarker.options.modal).modal('hide');
  }
};
```

## Сниппеты

### Параметры userMarker.Initialize

для подключение скрипто и стилей

| Параметр     | По умолчанию | Описание                           |
| ------------ | ------------ | ---------------------------------- |
| **selector** | `userMarker` | Селектор для кнопки добавить метку |

### Параметры userMarker.Label

userMarker snippet для вывода блока с метками

| Параметр             | По умолчанию           | Описание                                               |
| -------------------- | ---------------------- | ------------------------------------------------------ |
| **tplOuter**         | `tpl.userMarker.outer` | Обёртка для вывода результатов работы сниппета.        |
| **tpl**              | `tpl.userMarker.row`   | Чанк оформления для каждого результата                 |
| **resource_markers** |                        | id страницы с результатами выборки отмеченных ресурсов |
| **defaultLabel**     | `all`                  | Метка для выборки ресурсов по умолчанию                |
| **user**             | `1`                    | Показывать метки только те что создал пользователь.    |

### Параметры userMarker.Resource

snippet вернет список ресурсов пользователя с метками

| Параметр                   | По умолчанию                  | Описание                                                                                                                                                                                                                                                                       |
| -------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **label**                  |                               | Название метки для выборки ресурсов пользователя. По умолчанию all, вернет все ресурсы авторизованного пользователя                                                                                                                                                            |
| **class**                  | `modResource`                 | Имя класса для выборки. По умолчанию, "modResource".                                                                                                                                                                                                                           |
| **user_id**                |                               | Индитификатор пользователя для вывода меток                                                                                                                                                                                                                                    |
| **tpl**                    | `tpl.userMarker.resource.row` | Чанк оформления для каждого результата                                                                                                                                                                                                                                         |
| **tplOuter**               | `@INLINE [[+output]]`         | Обёртка для вывода результатов работы сниппета.                                                                                                                                                                                                                                |
| **limit**                  | `10`                          | Лимит выборки результатов                                                                                                                                                                                                                                                      |
| **offset**                 | `0`                           | Пропуск результатов с начала выборки                                                                                                                                                                                                                                           |
| **sortby**                 | `id`                          | Сортировка выборки. Для сортировки по полям метки нужно добавить префикс "Resource.", например: "&sortby=`Marker.label_id`"                                                                                                                                                    |
| **sortdir**                | `ASC`                         | Направление сортировки                                                                                                                                                                                                                                                         |
| **toPlaceholder**          |                               | Если не пусто, сниппет сохранит все данные в плейсхолдер с этим именем, вместо вывода не экран.                                                                                                                                                                                |
| **toSeparatePlaceholders** |                               | Если вы укажете слово в этом параметре, то ВСЕ результаты будут выставлены в разные плейсхолдеры, начинающиеся с этого слова и заканчивающиеся порядковым номером строки, от нуля. Например, указав в параметре "myPl", вы получите плейсхолдеры [[+myPl0]], [[+myPl1]] и т.д. |
| **showLog**                |                               | Показывать дополнительную информацию о работе сниппета. Только для авторизованных в контексте "mgr".                                                                                                                                                                           |
| **parents**                |                               | Список категорий, через запятую, для поиска результатов. По умолчанию выборка ограничена текущим родителем. Если поставить 0 - выборка не ограничивается.                                                                                                                      |
| **resources**              |                               | Список товаров, через запятую, для вывода в результатах. Если id товара начинается с минуса, этот товар исключается из выборки.                                                                                                                                                |
| **includeContent**         |                               | Выбирать поле "content" у товаров.                                                                                                                                                                                                                                             |
| **where**                  |                               | Строка, закодированная в JSON, с дополнительными условиями выборки.                                                                                                                                                                                                            |
| **outputSeparator**        |                               | Необязательная строка для разделения результатов работы.                                                                                                                                                                                                                       |
| **returnIds**              |                               | Возвращать строку с id товаров, вместо оформленных чанков.                                                                                                                                                                                                                     |
| **showUnpublished**        |                               | Показывать неопубликованные товары.                                                                                                                                                                                                                                            |
| **showDeleted**            |                               | Показывать удалённые товары.                                                                                                                                                                                                                                                   |
| **showHidden**             | `1`                           | Показывать товары, скрытые в меню.                                                                                                                                                                                                                                             |
| **outerIfEmpty**           | `1`                           | Включает вывод чанка-обертки (tplOuter) даже если результатов нет.                                                                                                                                                                                                             |

### Параметры userMarker.Record

snippet для вывода кнопки добавить метку ресурсу

| Параметр        | По умолчанию            | Описание                               |
| --------------- | ----------------------- | -------------------------------------- |
| **selector**    | `userMarker`            | Селектор для кнопки добавить метку     |
| **tpl**         | `tpl.userMarker.record` | Чанк оформления для каждого результата |
| **classKey**    | `modResource`           | classKey ресурса для добавления записи |
| **context_key** | `web`                   | Контекст ресурса. По умолчанию web     |
| **resource_id** |                         | id ресурса для добавления метки        |

### Параметры userMarker.Colors

snippet для вывода цветов в форме

| Параметр     | По умолчанию           | Описание                                                       |
| ------------ | ---------------------- | -------------------------------------------------------------- |
| **label_id** |                        | ID метки для выборки. Используется когда отсутствует имя метки |
| **tpl**      | `tpl.userMarker.color` | Чанк оформления для каждого результата                         |

## Системные настройки

| Настройка               | Описание                                             |
| ----------------------- | ---------------------------------------------------- |
| **frontend_jgrowl_js**  | Скрипты фронтенда jgrowl                             |
| **frontend_jgrowl_css** | Стили фронтенда jgrowl                               |
| **frontend_css**        | Стили фронтенда                                      |
| **frontend_js**         | Скрипты фронтенда                                    |
| **meta_context**        | Регистрировать мета тег context                      |
| **regular_expression**  | Регулярное выражение для проверки наименования метки |
| **framework**           | Подключить framework                                 |
| **framework_modal**     | Стили модельного окна                                |
| **resource_markers**    | id страницы с результатми выборки отмеченых ресурсов |
