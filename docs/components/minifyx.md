---
title: MinifyX
description: Автоматизированное сжатие скриптов и стилей сайта
logo: https://modstore.pro/assets/extras/minifyx/logo-lg.jpg
author: sergant210
modstore: https://modstore.pro/packages/utilities/minifyx
modx: https://extras.modx.com/package/minifyx
repository: https://github.com/modx-pro/MinifyX
---
# MinifyX

Автоматизированное сжатие и кэширование скриптов и стилей сайта.

## Параметры

| Название            | Описание                                                                                                                                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **&cssFilename**    | Префикс или полное имя скомпилированного CSS файла. По-умолчанию указан префикс «styles».                                                                                                                                            |
| **&cssGroups**      | Названия групп стилей (через запятую).                                                                                                                                                                                               |
| **&cssPlaceholder** | Имя плейсхолдера css. Используется, если **&registerCss=\`placeholder\`**. По-умолчанию «MinifyX.css».                                                                                                                               |
| **&cssSources**     | Список CSS файлов для обработки. Можно указывать «\*.css», «\*.less» и «\*.scss».                                                                                                                                                    |
| **&cssTpl**         | Шаблон для скомпилированного файла стилей. Должен быть указан плейсхолдер **[[+file]]**. По-умолчанию *«&lt;link rel="stylesheet" href="[[+file]]"&gt;»*.                                                                            |
| **&forceUpdate**    | Отключить проверку изменения файлов и генерировать новые скрипты и стили каждый раз.                                                                                                                                                 |
| **&hooks**          | Список хуков через запятую для обработки полученного результата. Укажите имя сниппета или файла с расширением.                                                                                                                       |
| **&jsFilename**     | Префикс или полное имя скомпилированного JS файла. По-умолчанию указан префикс «scripts».                                                                                                                                            |
| **&jsGroups**       | Названия групп скриктов (через запятую).                                                                                                                                                                                             |
| **&jsPlaceholder**  | Имя плейсхолдера javascript. Используется, если **&registerJs=\`placeholder\`**. По-умолчанию «MinifyX.javascript».                                                                                                                  |
| **&jsSources**      | Список JS файлов для обработки. Можно указывать «\*.js» и «\*.coffee».                                                                                                                                                               |
| **&jsTpl**          | Шаблон для скомпилированного файла скриптов. Должен быть указан плейсхолдер **[[+file]]**. По-умолчанию *«&lt;script type="text/javascript" src="[[+file]]"&gt;&lt;/script&gt;»*.                                                    |
| **&minifyCss**      | Включает минификацию CSS. По-умолчанию отключена.                                                                                                                                                                                    |
| **&minifyJs**       | Включает минификацию JS. По-умолчанию отключена.                                                                                                                                                                                     |
| **&preHooks**       | Список хуков через запятую для предварительной обработки. Укажите имя сниппета или файла с расширением.                                                                                                                              |
| **&registerCss**    | Подключение сss: «placeholder» - сохранить в плейсхолдер, «default» - подключить в теге <head\>, «print» - подключить в месте вызова сниппета. По-умолчанию, «placeholder».                                                          |
| **&registerJs**     | Подключение javascript: «placeholder» - сохранить в плейсхолдер, «startup» - подключить в теге <head\>, «default» - разместить перед закрывающим <body\>, «print» - подключить в месте вызова сниппета. По-умолчанию, «placeholder». |

## Кэш

Во время работы компонента все готовые файлы кэшируются в директорию, указанную в системной настройке `minifyx_cacheFolder`. По умолчанию она находится в директории assets компонента.

Если вы указываете собственную директорию, то будьте внимательны - Minifyx будет удалять все файлы в ней. **Всегда используйте отдельную пустую директорию для готовых файлов**!

## Группы

Для удобства файлы скриптов и стилей можно объединять в группы. Группы указываются в файле *core/components/minifyx/config/groups.php*.

## Хуки

Хуки - это сниппеты или файлы, которые позволяют выполнять необходимые манипуляции в процессе обработки файлов. Файловые хуки должны находится в папке *core/components/minifyx/hooks*.

Хуки бывают 2-х типов — хуки предварительной обработки и хуки пост обработки. Они указывают в параметрах «preHooks» и «hooks» соответственно. В прехуках можно добавлять группы и файлы. В постхуках изменять имя сформированного кэш-файла и его содержимое, что может пригодиться для дополнительной обработки полученного результата. Например, распарсить плейсхолдер MODX.

В хуках доступен объект **$MinifyX**, у которого есть методы для подключения как групп так и отдельных файлов, а также ряд других полезных методов.

### Методы для работы в прехуках

- addCssGroup('строка или массив') - добавить группу в список групп стилей.
- addJsGroup('строка или массив') - добавить группу в список групп скриптов.
- addCssSource('строка или массив') - добавить файл в список источников стилей.
- addJsSource('строка или массив') - добавить файл в список источников скриптов.
- setCssGroup('строка или массив') - заменить список групп стилей.
- setJsGroup('строка или массив') - заменить список групп скриптов.
- setCssSource('строка или массив') - заменить список файлов стилей.
- setJsSource('строка или массив') - заменить список файлов скриптов.
- getCssGroup('название группы') - получить указанную группу или все группы стилей.
- getJsGroup() - получить указанную группу или все группы скриптов.

### Методы для работы в постхуках

- isCss() - **true**, если компилируется css файл.
- isJs() - **true**, если компилируется javascript файл.
- getContent() - получить содержимое скомпилированного файла.
- setContent($content) - заменить содержимое скомпилированного файла.
- setFilename($filename) - заменить название файла.
- getFileUrl() - получить полный URL скомпилированного файла.
- getFilePath() - получить путь к скомпилированному файлу.

## Примеры

### Вывод сниппета с регистрацией стилей перед </head\> и скриптов перед </body\>

```modx
[[MinifyX?
  &minifyCss=`1`
  &minifyJs=`1`
  &registerCss=`default`
  &registerJs=`default`
  &cssSources=`
    assets/templates/himyf/css/normalize.css,
    assets/templates/himyf/css/foundation.css,
    assets/templates/himyf/css/font-awesome.css,
    assets/templates/himyf/css/app.css
  `
  &jsSources=`assets/templates/himyf/js/foundation.js`
]]
```

Для удобства можно создать набор параметров, в котором указать первые 4 параметра как в примере выше, и назвать его MinifyDefault (т.е. минифицировать и регистрировать в режиме default). Тогда вызов будет выглядеть так:

```modx
[[MinifyX@MinifyDefault?
  &cssSources=`
    assets/templates/himyf/css/normalize.css,
    assets/templates/himyf/css/foundation.css,
    assets/templates/himyf/css/font-awesome.css,
    assets/templates/himyf/css/app.css
  `
  &jsSources=`assets/templates/himyf/js/foundation.js`
]]
```

### Вывод в плейсхолдеры

Если указан режим вывода в плейсхолдеры, то скомпилированный файл стилей будет сохранён в плейсхолдере, указанном в параметре **&cssPlaceholder** (по-умолчанию `MinifyX.css`), а файл скриптов соответственно в плейсхолдере, указанном в параметре **&jsPlaceholder** (по-умолчанию `MinifyX.javascript`).

```modx
[[MinifyX?
  &minifyCss=`1`
  &minifyJs=`1`
  &cssSources=`
    assets/templates/himyf/css/normalize.css,
    assets/templates/himyf/css/foundation.css,
    assets/templates/himyf/css/font-awesome.css,
    assets/templates/himyf/css/app.css
  `
  &jsSources=`assets/templates/himyf/js/foundation.js`
]]
[[+MinifyX.css]]
[[+MinifyX.javascript]]
```

Если вы собираете сайта на шаблонизаторе Fenom, тогда вызов будет следующим:

```fenom
{'!MinifyX' | snippet : [
  'minifyCss' => 1,
  'minifyJs' => 1,
  'jsSources' => '
    assets/plugins/jquery/jquery-2.1.4.min.js,
    assets/js/scripts.js
  ',
  'cssSources' => '
    assets/plugins/bootstrap/css/bootstrap.min.css,
    assets/css/essentials.css,
    assets/css/layout.css,
    assets/css/header-1.css,
    assets/css/color_scheme/green.css
  '
]}
{$_modx->getPlaceholder('MinifyX.css')}
{$_modx->getPlaceholder('MinifyX.javascript')}
```

### Использование групп

Файл *groups.php*.

```php
<?php

return [
  'baseCss' => [
    '[[+assets_url]]templates/himyf/css/normalize.css',
    '{assets_url}templates/himyf/css/foundation.css',
    'assets/templates/himyf/css/font-awesome.css',
    'assets/templates/himyf/css/app.css'
  ],
  'baseJs' => [
    'assets/templates/himyf/js/foundation.js',
    '{assets_url}templates/himyf/js/scripts.js'
  ],
];
```

Вызов сниппета

```modx
[[MinifyX?
  &minifyCss=`1`
  &minifyJs=`1`
  &registerCss=`default`
  &registerJs=`default`
  &cssGroups=`baseCss`
  &jsGroups=`baseJs`
]]
```

### Пример прехука, добавляющего необходимые скрипты и стили для тикетов

```php
<?php

if ($modx->resource->parent == 10) {
  // Добавляем группы
  $MinifyX->addCssGroup('ticketsCss,officeCss');
  $MinifyX->addJsGroup('ticketsJs,officeJs');
  // Добавляем файлы
  $MinifyX->addCssSource("{assets_url}css/jquery.fancybox.css");
  $MinifyX->addJsSource("{assets_url}js/jquery.fancybox.js");
}
```

### Пример постхука, исправляющего проблему с единицами измерения vmax и vmin

```php
<?php

if ($MinifyX->isCss()) {
  $data = preg_replace('#vm (ax|in)#', 'vm$1', $MinifyX->getContent());
  $MinifyX->setContent($data);
}
```

Этот хук уже входит в пакет и называется **fixVm**. Также из коробки есть хук **cssToPage**, который регистрирует содержимое файла стилей прямо на страницу. Найти эти хуки можно в папке *core/components/minifyx/hooks*.
