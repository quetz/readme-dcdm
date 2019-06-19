# «СБОР ДАННЫХ НА УРОВНЕ БУРОВОЙ»
[![GitHub package.json version](https://img.shields.io/github/package-json/v/n19htz/readme-dcdm.svg)](https://github.com/n19htz/readme-dcdm/blob/master/package.json)
[![GitHub issues](https://img.shields.io/github/issues/n19htz/readme-dcdm.svg)](https://github.com/n19htz/readme-dcdm/issues)
> АРМ «Рабочее место оператора, сопровождающего процесс бурения»

Возможности программного обеспечения:
 * Визуализация в графическом виде цифровой информации от подрядчиков по строительству скважины. (web interface c обратной связью)
 * Разделение прав пользователей.
 * Ретроспективный просмотр информации.
 * Привязка и построение геологического разреза в 3D и 2D формате.
 * Импорт геологических и технологических данных из ASCI, .Las, excel, txt форматов, в т.ч. литологического описания.
 * Регистрация и привязка видео данных, к хронометражу по скважине.
 * Зеркалирования БД.
 * Получение данных от сторонних источников по WITS0 и WITSXML протоколу, IP-TCP.
 * Редактирование формул для получения новых вычислений.
 * Вычисления для параметров по отставанию.
 * Импортирование/экспортирование всей скважины, единым архивом.
 * Конфигурация/создание/удаление/зеркалирование скважины через отдельный web интерфейс. (конфиг)
 * Конфигурация скважины и компоновки инструмента через основной интерфейс и импорт/экспорт.
 * Ввод инклинометрии и её получение от стороннего подрядчика.

## Оглавление
- [Установка](#установка)
- [Использование](#использование)
- [Структура проекта](#структура-проекта)
- [Отображение отладочной инфомации](#отображение-отладочной-инфомации)
- [Лицензия](#лицензия)

## Установка
В терминале используйте [git](https://git-scm.com) или [hub](https://hub.github.com)

```bash
git clone https://github.com/amirig/dcdm.git
```
или
```bash
hub clone amirig/dcdm
```
после завершения клонирования репозитория при помощи [npm](https://docs.npmjs.com):

```bash
cd dcdm
npm install
```

## Использование
Для запуска приложения нужно установить ряд переменных среды окружения:
- **PGUSER** - имя пользователя ДБ,
- **PGPASSWORD** - пароль пользователя ДБ,
- **PGHOST** - IP-адрес ДБ,
- **PGPORT** - порт ДБ,
- **PGDATABASE** - название ДБ,
- **FSSrvAdr** - IP-адрес сервера поиска файлов,
- **FSSrvPort** - порт сервера поиска файлов,
- **PORT** - порт на котором будет запущен вебсервер, _по умолчанию **80**_,
- **DEBUG** - см. _[Отображение отладочной инфомаци](#отображение-отладочной-инфомации)_

Самый простой способ запуска это экспортировать переменные перед запуском стартового скрипта:
```bash
export PGUSER=dcdmsrv PGHOST=localhost PGDATABASE=dcdm PGPASWORD=123 PGPORT=5432 PORT=3000 && npm run start
```

В браузере:
```bash
http://localhost:3000/
```

## Структура проекта
- __dcdm__ - _корневая директория проекта_
  - [DBResTools.js](./DBResTools.js)
  - [MUConverter.js](./MUConverter.js) - _класс конвертации единиц измерений_
  - [OpRegManager.js](./OpRegManager.js)
  - __Uploads__ - _загружаемые/импортируемые файлы_
  - [WellLogQueryBuilder.js](./WellLogQueryBuilder.js) - _класс формирования SQL запроса для получения данных по скважине
                                                          и обработка полученного ответа (усреднение)_
  - [app.js](./app.js) - _web-сервер_
  - __calculation__ - _подсистема поддержки вычисляемых переменных (математика)_
  - __data_collector__ - _подсистема сбора, обработки и передачи данных с буровой_
  - [dbmanager.js](./dbmanager.js) - _класс для выполнения запросов к БД_
  - [dcdm.js](./dcdm.js) - _**стартовый модуль**_
  - [dcdm_config.js](./dcdm_config.js) - _начальные настройки стартового модуля_
  - [main.js](./main.js) - _инициализация и запуск web-сервера_
  - [package.json](./package.json) - _информация о приложении (название, версия, 
                                      зависимости, скрипты для работы с приложением и т.д.)_
  - [pugfunc.js](./pugfunc.js) - _класс для обработки мультиязыковых строк_
  - __reportgen__ - _подсистема генерации отчетов, отрисовки графиков_
  - __routes__ - _маршруты приложения_
  - __sql__ - _файлы SQL запросов_
    - [_createdb.sql](./sql/_createdb.sql) - _файл дампа начального состояния ДБ_
  - __static__ - _статические элементы приложения (стили, изображения, шрифты и т.д.)_
  - __test__ - _скрипты для тестирования приложения_
  - [users.js](./users.js) - _класс для работы с пользователями, алгоритм авторизации_
  - __views__ - _шаблоны страниц приложения_
  - __workwithdb__
    - [dbcalc.js](./workwithdb/dbcalc.js)

## Отображение отладочной инфомации
Для отображения отладочной инфомации необходимо задать 
переменной окружения `DEBUG` значение вида `namespace:worker`, где `namespace` - 
префикс или модуль, a `worker` - имя воркера, отладку которого нужно произвести. Также в переменную `DEBUG` можно передать 
несколько префиксов/воркеров
через запятую или пробел либо использовать маску, например, чтобы запустить отладку всего приложения
нужно установить `DEBUG=*`, или `DEBUG=dcdm:*` для отладки отдельного модуля.

### Доступные значения:
- _`dcdm:dcdm`_ -  [dcdm.js](./dcdm.js)
- _`dcdm:WebServer\main`_ -  [main.js](./main.js)
- _`dcdm:WebServer\app`_ -  [app.js](./app.js)
- _`dcdm:WebServer\routers\index`_ -  [routes/index.js](./routes/index.js)
- _`dcdm:WebServer\routers\autorize`_ -  [routes/autorize.js](./routes/autorize.js)
- _`dcdm:WebServer\routers\dreq`_ -  [routes/dreq.js](./routes/dreq.js)
- _`dcdm:WebServer\routers\home`_ -  [routes/home.js](./routes/home.js)
- _`dcdm:WebServer\routers\import`_ -  [routes/import.js](./routes/import.js)
- _`dcdm:WebServer\routers\report`_ -  [routes/report.js](./routes/report.js)
- _`dcdm:Calc\main`_ -  [calculation/main.js](./calculation/main.js)
- _`dcdm:LagManager`_ -  [calculation/LagManager.js](./calculation/LagManager.js)
- _`dcdm:DC_IPTWITS0\main`_ -  [data_collector/dc_IPTWITS0_main.js](./data_collector/dc_IPTWITS0_main.js)
- _`dcdm:ReportGen\ChartField\main`_ -  [reportgen/chartfield.js](./reportgen/chartfield.js)
- _`dcdm:DBManager`_ -  [dbmanager.js](./dbmanager.js)
- _`dcdm:OpRegManager`_ -  [OpRegManager.js](./OpRegManager.js)
- _`dcdm:Users`_ -  [users.js](./users.js)
- _`dcdm:workwithdb\dbcalc`_ -  [workwithdb/dbcalc.js](./workwithdb/dbcalc.js)
