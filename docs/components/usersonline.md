# UsersOnline

Список пользователей онлайн и сброс авторизации заблокированного пользователя

## Возможности

* Фиксирует дату крайнего появления каждого пользователя (во всех контекстах)
* Выводит список пользователей онлайн на сайте
* Сбрасывает авторизацию отключенных и заблокированных пользователей

## Фиксация даты появления пользователя

Для этого используется объект *UserOnline*, в котором фиксируется:

* ID пользователя
* Текущий контекст
* Дата и время появления

Появление пользователя в контексте *mgr* тоже фиксируется. Чтобы это отключить, выставьте системную настройку `usersonline_mgr_check` в `Нет`.

## Вывод списка пользователей онлайн

Для этой задачи используется сниппет *getOnlineUsers*, который является оберткой над *pdoUsers*. Соответственно, оформлением результатов занимается *pdoUsers*, которому передаются все параметры вызова.

### Параметры сниппета *getOnlineUsers*

| Название          | По умолчанию                                                       | Описание                                                                         |
|-------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **&contexts**     | Пустое значение (проверка во всех контекстах)                      | Список контекстов через запятую, в которых проверяются пользователи              |
| **&timeInterval** | -1 (взять значение из системной настройки *usersonline_time_span*) | Время в секундах, в течение которого пользователь считается находящимся на сайте |

### Системная настройка компонента

| Название                  | По умолчанию | Описание                                                                         |
|---------------------------|--------------|----------------------------------------------------------------------------------|
| **usersonline_time_span** | 900          | Время в секундах, в течение которого пользователь считается находящимся на сайте |

## Сброс авторизации заблокированным пользователям

По умолчанию в MODX, после блокировки пользователь может делать на сайте все, что угодно, пока жива его сессия.
Плагин *UsersOnline* проверяет, активен ли текущий пользователь. Если он заблокирован или отключен, будет запущен автоматический выход из системы и перенаправление на главную страницу, после чего беззаботная жизнь нарушителя закончится.