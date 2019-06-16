# «СБОР ДАННЫХ НА УРОВНЕ БУРОВОЙ»
[![GitHub package.json version](https://img.shields.io/github/package-json/v/n19htz/readme-dcdm.svg)](https://github.com/n19htz/readme-dcdm/blob/master/package.json)
[![GitHub issues](https://img.shields.io/github/issues/n19htz/readme-dcdm.svg)](https://github.com/n19htz/readme-dcdm/issues)
> АРМ «Рабочее место оператора, сопровождающего процесс бурения»

Программное обеспечение предназначено:
 * Для визуализации в графическом виде цифровой информации от подрядчиков по строительству скважины. (web interface c обратной связью)
 * Разделение прав пользователей.
 * Ретроспективный просмотр информации.
 * Привязка и построение геологического разреза в 3D и 2D формате.
 * Импорт геологических и технологических данных из ASCI, .Las, excel, txt форматов, в т.ч. литологического описания.
 * Регистрация и привязка видео данных, к хронометражу по скважине.
 * Возможность зеркалирования БД.
 * Получение данных от сторонних источников по WITS0 и WITSXML протоколу, IP-TCP.
 * Встроенный редактор формул для получения новых вычислений.
 * Встроенные вычисления для параметров по отставанию.
 * Возможность импортирования/экспортирования всей скважины, единым архивом.
 * Возможность конфигурации/создания/удаления/зеркалирование скважины через отдельный web интерфейс. (конфиг)
 * Конфигурация скважины и компоновки инструмента через основной интерфейс и импорт/экспорт.
 * Ввод инклинометрии и её получение от стороннего подрядчика.

## Оглавление
- [Установка](#установка)
- [Использование](#использование)
- [Отображение отладочной инфомации](#отображение-отладочной-инфомации)
- [Лицензия](#лицензия)
- [Структура проекта](#структура-проекта)

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
Для запуска приложения нужно установить ряд переменных окружающей среды:
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
export PGUSER=dcdmsrv && export PGHOST=localhost && export PGDATABASE=dcdm
&& export PGPASWORD=123 && export PGPORT=5432 && export PORT=3000 && npm run start
```

В браузере:
```bash
http://localhost:3000/
```

## Отображение отладочной инфомации
Для отображения отладочной инфомации необходимо задать 
переменной окружения `DEBUG` значение вида `namespace:worker`, где `namespace` - 
префикс или модуль, a `worker` - имя воркера, отладку которого нужно произвести. Также в переменную `DEBUG` можно передать 
несколько префиксов/воркеров
через запятую или пробел либо использовать маску, например, чтобы запустить отладку всего приложения
нужно установить `DEBUG=*`, или `DEBUG=dcdm:*` для отладки отдельного модуля. Более подробную информацию можно посмотреть **[здесь](https://github.com/visionmedia/debug)**.

## Структура проекта
- __dcdm__
  - [DBResTools.js](dcdm/DBResTools.js)
  - [MUConverter.js](dcdm/MUConverter.js)
  - [OpRegManager.js](dcdm/OpRegManager.js)
  - [README.md](dcdm/README.md)
  - __Uploads__
    - __CmtFiles__
    - __Import__
  - [WellLogQueryBuilder.js](dcdm/WellLogQueryBuilder.js)
  - [app.js](dcdm/app.js)
  - __calculation__
    - [LagManager.js](dcdm/calculation/LagManager.js)
    - [main.js.old](dcdm/calculation/main.js.old)
    - [README.md](dcdm/calculation/README.md)
    - [main.js](dcdm/calculation/main.js)
  - __data_collector__
    - [dc_IPTWITS0_main.js](dcdm/data_collector/dc_IPTWITS0_main.js)
  - [dbmanager.js](dcdm/dbmanager.js)
  - [dcdm.js](dcdm/dcdm.js)
  - [dcdm_config.js](dcdm/dcdm_config.js)
  - [main.js](dcdm/main.js)
  - [package.json](dcdm/package.json)
  - [pugfunc.js](dcdm/pugfunc.js)
  - __reportgen__
    - [chartfield.js](dcdm/reportgen/chartfield.js)
    - __fonts__
      - [pfdindisplaypro-bold-webfont.ttf](dcdm/reportgen/fonts/pfdindisplaypro-bold-webfont.ttf)
      - [pfdindisplaypro-reg-webfont.ttf](dcdm/reportgen/fonts/pfdindisplaypro-reg-webfont.ttf)
      - [pfdintextcomppro-regular-webfont.ttf](dcdm/reportgen/fonts/pfdintextcomppro-regular-webfont.ttf)
      - [pfdintextcomppro-bold-webfont.ttf](dcdm/reportgen/fonts/pfdintextcomppro-bold-webfont.ttf)
  - __routes__
    - [autorize.js](dcdm/routes/autorize.js)
    - [home.js](dcdm/routes/home.js)
    - [import.js](dcdm/routes/import.js)
    - [dreq.js](dcdm/routes/dreq.js)
    - [index.js](dcdm/routes/index.js)
    - [report.js](dcdm/routes/report.js)
  - __sql__
  - __static__
  - __test__
  - [users.js](dcdm/users.js)
  - __views__
    - [autorize.pug](dcdm/views/autorize.pug)
    - [MUTest.pug](dcdm/views/MUTest.pug)
    - [error.pug](dcdm/views/error.pug)
    - [autorize_msg.html](dcdm/views/autorize_msg.html)
    - [home.pug](dcdm/views/home.pug)
    - [home_admin_msg.html](dcdm/views/home_admin_msg.html)
    - [home_import_msg.html](dcdm/views/home_import_msg.html)
    - [home_msg.html](dcdm/views/home_msg.html)
    - [home_regist_msg.html](dcdm/views/home_regist_msg.html)
    - [home_workwithdb_msg.html](dcdm/views/home_workwithdb_msg.html)
    - [inc_home_admacgrp.pug](dcdm/views/inc_home_admacgrp.pug)
    - [inc_home_admacgrpdlg.pug](dcdm/views/inc_home_admacgrpdlg.pug)
    - [inc_home_admintgpnt.pug](dcdm/views/inc_home_admintgpnt.pug)
    - [inc_home_admintgpntdlg.pug](dcdm/views/inc_home_admintgpntdlg.pug)
    - [inc_home_admusers.pug](dcdm/views/inc_home_admusers.pug)
    - [inc_home_admusersdlg.pug](dcdm/views/inc_home_admusersdlg.pug)
    - [inc_home_calc.pug](dcdm/views/inc_home_calc.pug)
    - [inc_home_calcdlg.pug](dcdm/views/inc_home_calcdlg.pug)
    - [inc_home_commentsandfiles_dlg.pug](dcdm/views/inc_home_commentsandfiles_dlg.pug)
    - [inc_home_commentsandfiles.pug](dcdm/views/inc_home_commentsandfiles.pug)
    - [inc_home_dbexport.pug](dcdm/views/inc_home_dbexport.pug)
    - [inc_home_dbimport.pug](dcdm/views/inc_home_dbimport.pug)
    - [inc_home_dbmanipulate.pug](dcdm/views/inc_home_dbmanipulate.pug)
    - [inc_home_regedt.pug](dcdm/views/inc_home_regedt.pug)
    - [inc_home_messages.pug](dcdm/views/inc_home_messages.pug)
    - [inc_home_regedtdlg.pug](dcdm/views/inc_home_regedtdlg.pug)
    - [inc_home_regist_datadlg.pug](dcdm/views/inc_home_regist_datadlg.pug)
    - [inc_home_registries.pug](dcdm/views/inc_home_registries.pug)
    - [inc_home_registriesimport.pug](dcdm/views/inc_home_registriesimport.pug)
    - [inc_home_somedlg.pug](dcdm/views/inc_home_somedlg.pug)
    - [inc_home_unitssetup.pug](dcdm/views/inc_home_unitssetup.pug)
    - [inc_home_wells.pug](dcdm/views/inc_home_wells.pug)
    - [inc_home_widgetdlgs.pug](dcdm/views/inc_home_widgetdlgs.pug)
    - [inc_home_wellsdlg.pug](dcdm/views/inc_home_wellsdlg.pug)
    - [inc_langblock.pug](dcdm/views/inc_langblock.pug)
    - [layout.pug](dcdm/views/layout.pug)
  - __workwithdb__
    - [dbcalc.js](dcdm/workwithdb/dbcalc.js)

## Лицензия
[MIT](https://choosealicense.com/licenses/mit/)
