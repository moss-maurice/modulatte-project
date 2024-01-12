# Ядро проекта modulatte

[![Language](https://img.shields.io/badge/php-%5E7.3-blue)](https://img.shields.io/badge/php-%5E7.3-blue) [![Language](https://img.shields.io/badge/EvolutionCMS-%5E3.0-brightgreen)](https://img.shields.io/badge/EvolutionCMS-%5E3.0-brightgreen) [![Language](https://img.shields.io/badge/Laravel-%5E8.0-red)](https://img.shields.io/badge/Laravel-%5E8.0-red)

Пакет проекта модуля для mmaurice/modulatte-project

## Содержание

-   [Установка](#install)
-   [Назначение каталогов пакета](#package-folders)
-   [Доступные консольные команды](#commands)

## Install

Произвести устновку базового модуля **Modulatte**:

```sh
root@ssh:~/core/custom/packages/main/#: cd assets/modules
root@ssh:~/core/custom/packages/main/assets/modules/#: create-project mmaurice/modulatte-project modulatte
```

## Package Folders

#### Конфигурация (config)

Вся конфигурация модуля содержится в файле `module.php` внутри каталога `config`. Пример содержимого файла:

```php
return [

    // Название модуля
    'name' => 'Тест-модуль',

    // Иконка модуля
    'icon' => 'fa fa-atlas',

];
```

#### Ресурсы (resources)

Каталог ресурсов содержит в себе другие подкаталоги:
-- `scripts` - содержит необходимые для расширения функционала модуля скрипты JS
-- `styles` - содержит необходимые для расширения функционала модуля стили CSS
-- `views` - содержит необходимые для расширения функционала модуля шаблоны BLADE

Важно понимать, что в механике работы модуля используются базовые шаблоны, которые поставляются в пакете `mmaurice\modulatte-support`. Но при необходимости расширить тот или иной файл шаблона blade, необходимо скопировать этот файл (с учётом иерархии каталогов) из каталога `/vendor/mmaurice/modulatte-support/resource/views/*` в каталог `/resources/views/*` модуля. Правда, есть нюанс с каталогом tab в шаблонах пакета. Там содержатся базовые шаблоны для всех табов по-умолчанию. Если необходимо кастомизировать шаблон только для одного таба в модуле, необходимо скопировать файл `/vendor/mmaurice/modulatte-support/resource/views/tab/*` в каталог `/resources/views/tabs/<tab-name>/*`

Кроме этого, в каталоге `resources` допустимо создавать иные необходимые для работы приложения каталоги. Например, `images`, `fonts`, `saas`, `scss` и прочие.

#### Код модулей (modules)

В каталоге `modules` содержится список каталогов модулей. Обязательно с заглавной буквы

В базовом исполнении каталог содержит самые важные для работы модуля файлы:
-- `Controllers` - каталог для размещения логики контроллеров табов
-- `Models` - каталог для размещения моделей табов
-- `Module.php` - базовый файл модуля (для инициилизации и дальнейшего расширения)

Контроллер содержит базовые методы для инициализации работы CRUD-модуля:
-- `index` - метод, отображающий интерфейс главного окна таба модуля
-- `list` - метод для вывода списка сущностей
-- `create` - метод, отображающий интерфейс для создания сущности
-- `update` - метод, отображающий интерфейс для редактирования сущности
-- `delete` - метод для удаления сущности

Кроме этого, есть следующие служебные методы:
-- `actionBar` - метод для управления кнопками Action Bar таба
-- `model` - метод для вывода объекта текущей модели (зависит от таба)

Для больших деталей рекомендуется изучить код исходного контроллера модуля

Модель так же содержит свою иерархию методов и логику работы. **Будет описано позже**

#### Загрузчик (bootstrap.php)

Необходим для предзагрузки ядра модуля. Необходим как альтернатива autoload, но в будущем (после перехода на мультимодуль) скорее всего утратит смысл.

#### Точка входа (index.php)

Точка входа, необходимая для подключения загрузчика модуля, а так же копируется при развёртывании поставки в публичный каталог модулей

#### Инициализация модулей (initialize.php)

Точка входа, необходимая для инициализации загрузчика модуля

## Commands

Команды в данный момент не поддерживаются, но планируется их создание в будущем.
