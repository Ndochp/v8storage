# v8storage

## Библиотека для упрощения работы с Хранилищем 1С из oscript.

Позволяет выполнять рутинные операции с Хранилищем 1С в стиле [v8runner](https://github.com/oscript-library/v8runner).

Пример работы:
```bsl
ХранилищеКонфигурации = Новый МенеджерХранилищаКонфигурации();
ХранилищеКонфигурации.УстановитьКаталогХранилища(КаталогХранилища);

ХранилищеКонфигурации.ПрочитатьХранилище();

ХранилищеКонфигурации.СохранитьВерсиюКонфигурацииВФайл(НомерВерсии, ИмяФайлаКофигурации);

ТаблицаВерсий = ХранилищеКонфигурации.ПолучитьТаблицаВерсий();
МассивАвторов = ХранилищеКонфигурации.ПолучитьАвторов();

```

Так же описание функциональности содержится в папке `features`. В прилагающихся `step_definitions` можно подсмотреть больше примеров.

## Публичный интерфейс

### Класс МенеджерХранилищаКонфигурации:

> Работа со свойствами объекта МенеджерХранилищаКонфигурации

#### УстановитьУправлениеКонфигуратором
```bsl
// Установка управления конфигуратором в класс менеджер хранилища конфигурации
//
// Параметры:
//   НовыйУправлениеКонфигуратором - класс - инстанс класс УправлениеКонфигуратором из библиотеке v8runner
//
```

#### УстановитьКаталогХранилища
```bsl
// Установка каталога файлового хранилища конфигурации
//
// Параметры:
//   НовыйКаталогХранилища - Строка - путь к папке с хранилищем конфигурации 1С
//
```

#### УстановитьПараметрыАвторитизации
```bsl
// Установка авторитизации в хранилище конфигурации
//
// Параметры:
//   Пользователь - Строка - пользователь хранилищем конфигурации 1С
//   Пароль - Строка - пароль пользователя хранилищем конфигурации 1С (по умолчанию пустая строка)
//
```

#### СохранитьВерсиюКонфигурацииВФайл
```bsl
// Сохранение в файл версии конфигурации из хранилища
//
// Параметры:
//   НомерВерсии - число/строка - номер версии в хранилище
//   ИмяФайлаКофигурации - строка - путь к файлу в который будет сохранена версия конфигурации из хранилища 
//
```

#### ПоследняяВерсияКонфигурацииВФайл
```bsl
// Сохранение в файл последней версии конфигурации из хранилища
// (обертка над процедурой "СохранитьВерсиюКонфигурацииВФайл")
// Параметры:
//   ИмяФайлаКофигурации - строка - путь к файлу в который будет сохранена версия конфигурации из хранилища 
//
```

#### ПрочитатьХранилище
```bsl
// Чтение данных по истории версий и авторов из хранилища
// 
// Параметры:
//   НомерНачальнойВерсии - число - номер версии хранилища, 
//                                  с которой производиться получение истории (по умолчанию 1) 
//  
```

#### ПолучитьТаблицаВерсий
```bsl
// Получение таблицы истории версий из хранилища
// (выполняет ПрочитатьХранилище(1), если еще не было чтения)
//
// Возвращаемое значение таблица значений:
//   Колонки: 
//      Номер   - число - номер версии  
//      Дата    - Дата - Дата версии  
//      Автор   - строка - автор версии  
//      Комментарий   - Строка - многострочная строка с комментарием к версии  
// 
```

#### ПолучитьАвторов
```bsl
// Получение массива авторов версий из хранилища
// (выполняет ПрочитатьХранилище(1), если еще не было чтения)
// 
// Возвращаемое значение массив:
//      Автор - строка - используемые авторы в хранилище  
// 
```

#### ПолучитьОтчетПоВерсиям
```bsl
/// Получение отчет по истории версий  из хранилища
// 
// Параметры:
//   ПутьКФайлуРезультата - Строка - путь к файлу в который будет выгружен отчет, 
//   НомерНачальнойВерсии - число - номер начальной версии хранилища,
//                                  с которой производиться получение истории (по умолчанию 1) 
//   НомерКонечнойВерсии  - число - номер конечной версии хранилища. (по умолчанию - Неопределено)
// 
```

#### ПодключитьсяКХранилищу
```bsl
// Выполняет подключение ранее неподключенной информационной базы к хранилищу конфигурации.
//
// Параметры:
//  ИгнорироватьНаличиеПодключеннойБД  - Булево - Флаг игнорирования наличия уже у пользователя уже подключенной базы данных. По умолчанию = Ложь
//								 	 Выполняет подключение даже в том случае, если для данного пользователя уже есть конфигурация, связанная с данным хранилищем..
//  ЗаменитьКонфигурациюБД - Булево - Флаг замены конфигурации БД на конфигурацию хранилища  (По умолчанию Истина)
//									 Если конфигурация непустая, данный ключ подтверждает замену конфигурации на конфигурацию из хранилища.
//
```

#### СконвертироватьОтчет
```bsl
// Получение отчет по истории версий  из хранилища
// 
// Параметры:
//   ПутьКФайлуРезультата - Строка - путь к файлу отчета в формате mxl 
//   ПутьКФайлуОтчетаJSON - Строка - путь к файлу в который будет выгружен отчет в формате json,
// 
```