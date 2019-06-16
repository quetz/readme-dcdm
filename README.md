![GitHub issues](https://img.shields.io/github/issues/n19htz/dcdm-local.svg?style=plastic)
# Foobar
Foobar is a Python library for dealing with word pluralization.

## Описание
Программное обеспечение предназначено:
 * Для визуализации в графическом виде цифровой информации от подрядчиков по строительству скважины. (web interface c обратной связью)
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

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
