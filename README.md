<img height="34" width="97" src="https://raw.githubusercontent.com/artem-malko/artwork/master/tars/logo.png">
=============

Сборщик верстки, основанный на gulp. Облегчает и ускоряет процесс верстки сайтов любой сложности. Подойдет как командам, так и отдельному разработчику.

TARS — сборщик-фреймворк, включающий в себя набор gulp-тасков, предоставляющий возможность легкого расширения (создания новых тасков) и модифицирования уже существующих.

Основные фичи
-------------

— Понятная и легко масштабируемая файловая структура.
— Jade или Handlebars на выбор в качестве html-шаблонизатора.
— Использование json для передачи данных в шаблоны (опционально, но очень крутая штука, которая позволит избавиться от копипаста).
— SCSS, LESS или Stylus в качестве препроцессора для css. Также в комплекте идет небольшой набор миксинов.
— Autoprefixer. Можно забыть о вендорных префиксах, автопрефиксер сделает всю работу за вас.
— Отдельная сборка css для ie8 и ie9. Основной css-файл больше не будет содержать ненужного кода.
— JS-hinting и linting (можно настроить под себя в .jscsrc в корне).
— Css и js минификация.
— Никаких внешних библиотек и плагинов (кроме html5shiv). И да, это фича, так как вы вольны сами выбирать, какие библиотеки использовать.
— Watching за изменениями файлов (создания и удаления). В текущей версии gulp вотчер не умеет отслеживать создание и удаление файлов кроссплатформенно. Блы написан свой плагин для этого. С 4 версией gulp будем использовать встроенный, так как планируется, что он избавится от всех недостатков.
— Уведомления о выполнении тасков. Может даже иметь звуковое сопровождение, если включиьт соответствующую опцию.
— Livereload с помощью browserSync, так же опционально.
— Расшаривание верстки во внешний веб, опционально.
— Можно легко добавлять новые таски. Есть примеры того, как создать и использовать новый таск внутри TARS.
— Умная работа с изображениями. В первую очередь с вектором (svg).
— Несколько режимов сборки (обычная, с минифицированными файлами, с хешем в названии css- и js-файлов для выкладки в продакшн).
— Создание архива с готовой сборкой.

Установка
----------

Необходимо установить `nodeJS` версии выше или равной 0.8
Далее необходимо установить gulp глобально. (Возможно потребуются права суперюзера или администратора)

    npm i -g gulp

Затем устанавливаем зависимости.

    npm i or npm install

Если не все зависимости были установлены, то последнюю оперция нужно повторить.

После установки всех зависимостей необходимо открыть projectConfig и настроить проект под себя. В конфиге вы можете выбрать шаблонизатор, css-препроцессор, использование уведомлений и т.д.
После того, как выполнена настройка проекта, выполняем следующую команду:    

    gulp init

Данная команда создаст базовую файловую систему, подтянет таски для выбранных вами шаблонизатора и css-препроцессора.

Основные команды
----------------

`gulp init` — Инициализирует проект с заданными опциями в projectConfig.js

`gulp re-init` — Переинициализирует проект с заданными опциями в projectConfig.js. Предлагается использовать данную команду, если вы инициализировали проект с неверными опциями. При переинициализации все папки и файлы удаляются, поэтому не рекомендуется выполнять эту команду, если вы уже начали выполнение работы.

`gulp` или `gulp build` — делает сборку проекта. Подключаются не минимизированные файлы. Тип сборки зависит от переданных ключей вместе с этой командой. Доступные ключи:

* `--min` – в html подключаются минимизирвоанные файлы.
* `--release` – в html подключаются  минимизированные файлы, в названии которых есть hash. Данный режим полезен, если вы напрямую выкладываете верстку на сервер. 

`gulp dev` — инициализация сборщика в режиме разработки. Создается dev-версия проекта, без всех минификаций. Также запускает вотчеры за файлами проекта. Доступные ключи:

* `--lr` – инициализация livereload, если он включен в конфиге проекта.
* `--tunnel` – инициализация проекта с расшаривание верстки во внешний веб. Ссылка будет указана в консоли.

`gulp build-dev` — генерация dev-версии проекта без вотчеров.

Ключи, доступные при любом режиме сборки:
* `--ie9` – включить в сборку стили для ie9.
* `--ie8` – включить в сборку стили для ie8.

`gulp update` – обновление всех зависимостей сборщика до последних стабильных. Может потребоваться какое-то время на выполнение данной команды.

Краткое описание файловой структуры
-----------------------------------

`markup` – основная папка проекта, где находятся все исходники для верстки. Внутри находятся папки:
    * `modules` — папка с модулями.
    * `static` — папка для статики.
    * `pages` — папка с шаблонами страниц.

Каждая страница состоит из модулей, например — «header». Каждый модуль имеет свое html-, css- и js-представление. Также, каждый модуль может иметь подпапку `ie`, в которой можно разместить стили для ie8 и ie9. Модули могут включать в себя другие модули.
В `pages` находятся шаблоны страниц, в которые в итоге будут включены модули. Они являются лэйаутом и должны содеражть в себе как можно меньше кода, чтобы структура страницы была как можно более прозрачная.
Чтобы создать новую страницу, просто скопируйте существующую (или _template), и переименуйте.

Документация
------------