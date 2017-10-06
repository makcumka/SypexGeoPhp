## Install
The new version of `makcumka/sypexgeophp` using [Composer] (http://getcomposer.org).

```bash
$ composer require makcumka/sypexgeophp
```

## 1. Создать объект SxGeo
```php
// Первый параметр - имя файла с базой (используется бинарная БД Sypex Geo)
// Второй параметр - режим работы:
//  SXGEO_FILE   (работа с файлом базы, режим по умолчанию);
//  SXGEO_BATCH  (пакетная обработка, увеличивает скорость при обработке множества
//                IP за раз);
//  SXGEO_MEMORY (кэширование БД в памяти, еще увеличивает скорость пакетной обработки,
//                но требует больше памяти, для загрузки всей базы в память).

$SxGeo = new SxGeo(); // Режим по умолчанию, файл бд SxGeo.dat
//$SxGeo = new SxGeo('SxGeo.dat', SXGEO_BATCH | SXGEO_MEMORY); // Самый быстрый режим пакетной обработки
```

## 2. Определяем страну c БД содержащими страны (SxGeo Country)
```php
$country = $SxGeo->getCountry($ip); // возвращает двухзначный ISO-код страны
// $SxGeo->getCountryId($ip);       // возвращает номер страны
```

## 3. Определяем город (SxGeo City, SxGeo City Max)
```php
// $SxGeo->getCity($ip);     // возвращает краткую информацию, без названия региона, страны и временной зоны
// $SxGeo->getCityFull($ip); // возвращает полную информацию о городе, регионе и стране
$city = $SxGeo->get($ip);    // выполняет getCountry либо getCity в зависимости от типа базы
```

## 4.  Если нужно осводить рессурсы - удаляем объект
```php
unset($SxGeo);
```

Также смотрите пример sxgeo_sample.php (для его работы не забудьте скопировать в тот же каталог SxGeoCity.dat)