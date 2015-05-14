# services-table

Блок используется для создания [Табло сервисов](https://github.yandex-team.ru/lego/services-table).

Табло содержит локализованный набор основных сервисов Яндекса в виде таблицы.
Позволяет:

* отображать один из заранее заданных наборов сервисов, для поддерживаемых языковых регионов (`.ru`, `.соm`, `.turkish`);
* задать во входных данных произвольный набор сервисов. 

Список сервисов, выводимых в блоке по умолчанию, зависит от [языкового региона](#mods_type).
 Регион определяется на основе глобального параметра `content-region` из блока [i-global](https://lego.yandex-team.ru/libs/islands-romochka/v3.x/desktop/i-global/).

[Особенности реализации](#features). 

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [type](#mods-type)  | `'ru'`, `'com'`, `'turkish'` | BEMJSON, JS(?)| Наборы сервисов по умолчанию для поддерживаемых языковых регионов.  |

### Специализированные поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [items](#fields-items)| Array, Object(?) | Шорткат (сокращенная форма?) для задания элементов (сервисов) в блоке. Не используется одновременно с [элементами item](#__item). |
| [serviceIconMods](#fields-serviceIconMods)| Object | Модификаторы для передачи в блок [service-icon](https://github.yandex-team.ru/lego/islands-icons/tree/dev/common.blocks/service-icon), который миксуется к `service__icon`. |
| [maxItemsPerRow](#fields-maxItemsPerRow)| Number(?) | Максимально допустимое число элементов (сервисов) в строке Табло.  (поле блока? пример ?). Значение по умолчанию: 5. Используется только с [полем items](#fields-items). |
| [prefsTarget](#fields-prefsTarget) | String | Значение HTML-атрибута `target` для передачи в блок [service](https://lego.yandex-team.ru/libs/islands-page/support-3.x/desktop/service) сервисов Почта и Перевод. Применяется только с [модификатором type в значении com](#mods-type-com). |
| [all](#fields-all) | Boolean | Шорткат для [элемента all](#elems-all). Используется только с [полем items](). |

### Элементы блока

Cпособы использования: `BEMJSON` (другие варианты не предусмотрены).

| Элемент | Описание |
| --------| -------- |
| [item](#elems-item) | Элемент Табло (сервис), реализованный блоком [service](https://lego.yandex-team.ru/libs/islands-page/support-3.x/desktop/service). |
| [all](#elems-all)  | Псевдокнопка «Все сервисы». Выполняет переход на страницу со списком всех сервисов Яндекса для текущего языкового региона. Включена в наборы сервисов по умолчанию. |


## Подробнее

### Задание произвольного набора сервисов

Блок предоставляет возможнось сформировать нужный список сервисов с помощью поля `item` – сокращенная форма задания элементов Табло (сервисов). Рекомендуемый способ.

```js
{
    block: 'services-table',
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}}
    ]
}
```

что эквивалентно следующей развернутой записи BEMJSON блока, с использованием элемента блока `item`.

```js 
{
    block: 'services-table',
    content: [
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'images',
                iconMods: {color: '56'}
            }
        },
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'maps',
                iconMods: {color: '56'}
            }
        }
    ]    
}        
``` 
Зависимости: На уровне переопределения проекта необходимо добавить зависимости от элементов блока `service-icon`, перечисленных в произвольном наборе сервисов входного BEMJSON. В данном случае:

`../myproject/services-table/ services-table.deps.js`

```javascript 
({ 
    shouldDeps: [
        {
            block: 'service-icon',
            elems: [ 
                {elem: 'images', mods: {color: 56}},
                {elem: 'maps', mods: {color: 56}} 
            ] 
        } 
    ] 
});

При использовании поля `items` сервисы (элементы блока [item](#elems-item)) будут распределены оптимальным образом в Табло, в зависимости от общего количества сервисов и максимально допустимого числа сервисов в строке ([поле maxItemsPerRow](#fields-maxItemsPerRow)). 

---
**NB** В BEMJSON-декларации блока нельзя одновременно использовать сокращенную и развернутую форму записи. Если в BEMJSON блока есть поле `content`, шаблоны применяются как есть.

---

### Добавление псевдокнопки «Все сервисы»

Также появился шорткат для добавления элемента `all`.

```javascript
{
    block: 'services-table',
    items: [
        // ...
    ],
    all: true
}
```
Это соответствует следующей развернутой BEMJSON записи:
```javascript
{
    block: 'services-table',
    content: [
        // ...
        {
            elem: 'all'
        }
    ]
}
```


<a name="mods"></a>
### Модификаторы блока

<!---------------- 1 вариант ------------------->

<a name="mods-type"></a>
#### Модификатор `type`
 
| Допустимые значения | Способ использования | Описание |
| ------------------- | ------------------- | -------------------- | ---------|
| `'ru'` |BEMJSON, JS(?) | **Значение по умолчанию**. Набор сервисов для русскоязычного региона, КУБР (домен `ru`): Картинки, Карты, Новости, Почта, Видео, Перевод, Браузер, Афиша, Диск, Маркет, Словари, Музыка, Такси, Авто, Деньги. |
| `'com'` |BEMJSON| Набор сервисов для англоязычного региона (домен `com`): Картинки, Видео, Почта, Перевод. |
| `'turkish'` |BEMJSON | Набор сервисов для Турции (домен `tr`): Картинки, Карты, Погода, Новости, Почта, Видео, Перевод, Браузер, Маркет, Диск. |

Способ использования: `BEMJSON`, `JS`(?). 

Модификатор `type` используется для изменения набора сервисов в Табло, для различных языковых регионов.

По умолчанию (если модификатор `type` не установлен), значение будет получено из глобального параметра `content-region` блока [i-global](https://github.yandex-team.ru/lego/islands-romochka/blob/dev/common.blocks/i-global/i-global.ru.md)(`islands-romochka`).

```js
<h5>Табло сервисов (по умолчанию)</h3>
{
  block: 'services-table' 
}
<h5>Табло сервисов для русскоязычного региона КУБР</h3>
{
    block: 'services-table',
    mods: {type: 'ru'}  // табло сервисов для России
}
<h5>Табло сервисов для англоязычного региона</h3>
{
    block: 'services-table',
    mods: {type: 'com'}  
}
<h5>Табло сервисов для Турции</h3>
{
    block: 'services-table',
    mods: {type: 'turkish'}  
}
```

<!---------------- 2 вариант ------------------->

<a name="mods-type"></a>
#### Модификатор `type`

Допустимое значение: ['ru'](#mods-type-ru), ['com'](#mods-type-com), ['turkish'](#mods-type-turkish).

Значение по умолчанию: `'ru'`.

Способ использования: `BEMJSON`, `JS`(?). 


Модификатор `type` используется для изменения набора сервисов в Табло, для различных языковых регионов.

По умолчанию (если модификатор `type` не установлен), значение будет получено из глобального параметра `content-region` блока [i-global](https://github.yandex-team.ru/lego/islands-romochka/blob/dev/common.blocks/i-global/i-global.ru.md) (`islands-romochka`).

Табло сервисов (по умолчанию)

```js
{
  block: 'services-table' 
}
```

<a name="mods-type-ru"></a>
##### Табло сервисов для русскоязычного региона (модификатор `type` в значении `ru`)

Определяет набором сервисов для русскоязычного региона КУБР (домен `ru`): Картинки, Карты, Новости, Почта, Видео, Перевод, Браузер, Афиша, Диск, Маркет, Словари, Музыка, Такси, Авто, Деньги. 

```js
{
    block: 'services-table',
    mods: {type: 'ru'} 
}
```

<a name="mods-type-com"></a>
##### Табло сервисов для англоязычного региона (модификатор `type` в значении `com`)

Определяет набор сервисов для англоязычного региона (домен `com`): Картинки, Видео, Почта, Перевод.

```js
{
    block: 'services-table',
    mods: {type: 'com'}  
}
```

<a name="mods-type-turkish"></a>
##### Табло сервисов для Турции ( _type_turkish )

Определяет набор сервисов для Турции (домен `tr`): Картинки, Карты, Погода, Новости, Почта, Видео, Перевод, Браузер, Маркет, Диск.

```js
{
    block: 'services-table',
    mods: {type: 'turkish'}  
}
```

<a name="fields"></a>
### Специализированные поля блока

<a name="fields-items"></a>
#### Поле `items`

Тип: `Object`|`Array`. 

Значение по умолчанию: -.  

Cокращенная форма для задания элементов (сервисов) в блоке. Рекомендованный способ. Не используется одновременно с [элементами item](#elems-item).

При его использовании сервисы (элементы блока [item](#elems-item)) будут распределены оптимальным образом, в зависимости от общего количества сервисов и максимально допустимого числа сервисов в строке ([поле maxItemsPerRow](#fields-maxItemsPerRow)). 

```js
{
    block: 'services-table',
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}}
    ]
}
```
Зависимости: необходимо добави зависимости от соответствующих элементов блока `service-icon`.
Зависимости: На уровне переопределения проекта необходимо добавить зависимости от элементов блока `service-icon`, перечисленных в произвольном наборе сервисов входного BEMJSON. В данном случае:

`../myproject/services-table/ services-table.deps.js`

```javascript 
({ 
    shouldDeps: [
        {
            block: 'service-icon',
            elems: [ 
                {elem: 'images', mods: {color: 56}},
                {elem: 'maps', mods: {color: 56}} 
            ] 
        } 
    ] 
});

<a name="fields-serviceIconMods"></a>
#### Поле `serviceIconMods` (поле элемента item!)

Тип: `Object`. 

Значение по умолчанию: -.  

Используется для передачи модификаторов в блок [service-icon](https://github.yandex-team.ru/lego/islands-icons/tree/dev/common.blocks/service-icon), который миксуется к `service__icon`. Используется в только с [полем items](#fields-items).

```js
{
    block: 'services-table',
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}}
    ]
}
```

<a name="fields-maxItemsPerRow"></a>
#### Поле `maxItemsPerRow`

Тип: `Number`. 

Значение по умолчанию: `5`.  

Определяет максимально допустимое число сервисов в строке Табло. Используется только с [полем items](#fields-items).


Участвует в вычислении количества сервисов в строке, для оптимального распределения всех сервисов в Табло. Например, при максимальном количестве сервисов в строке – 5, шесть сервисов лучше разместить в двух строчках по 3 элемента, а не 5 и 1.

```js
{
    block: 'services-table',
    maxItemsPerRow: 3,
    items: [
        {service: 'images', serviceIconMods: {color: 56}},
        {service: 'maps', serviceIconMods: {color: 56}},
        {service: 'browser', serviceIconMods: {color: 56}},
        {service: 'disk', serviceIconMods: {color: 56}},
        {service: 'mail', serviceIconMods: {color: 56}}
    ]
}
```

<a name="fields-prefsTarget"></a>
#### Поле `prefsTarget`

Тип: `String`. 

Значение по умолчанию: -.

Определяет значение HTML-атрибута `target`, передаваемый для ссылок сервисов (в блок [service]()) Почта и Перевод. Используется только для модификатора `type` в значении `com`.

```js
{
    block: 'services-table',
     mods: {type: 'com'},
     prefsTarget: 'blank'
}
```

<a name="fields-all"></a>
#### Поле `all`

Тип: `Boolean`. 

Значение по умолчанию: -.  

Сокращенная форма записи для добавления [элемента all](#elems-all). Рекомендованный способ. Используется только с [полем items](#elems-items).

```javascript
{
    block: 'services-table',
    items: [
        // ...
    ],
    all: true
}
```
Зависимости: нужна для собственного набора? 


<a name="elems"></a>
### Элементы блока

<a name="elems-item"></a>
#### Элемент `item`

Используется для создания элементов Табло – сервисов, реализуется с помощью блока [service](https://lego.yandex-team.ru/libs/islands-page/v3.x/desktop/service/examples/), который помещается в поле `content` BEMJSON-декларации блока. 

<!-- Сервис представлен иконкой-ссылкой и названием сервиса, ведущие на главную страницу сервиса. -->

Массив элементов `item` используется для задания произвольного набора сервисов.

```js 
{
    block: 'services-table',
    content: [
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'images',
                iconMods: {color: '56'}
            }
        },
        {
            elem: 'item',
            content: {
                block: 'service',
                service: 'maps',
                iconMods: {color: '56'}
            }
        }
    ]    
}        
``` 

Иконки сервисов (в данном случае, цветные размером `56х56`px) будут получены из блока [service-icon](https://github.yandex-team.ru/lego/islands-icons/tree/dev/common.blocks/service-icon) на основе идентификатора сервиса Лего – `service` (в `service-icon` является элементом блока). В модификаторах элементов блока`service-icon`, которые совпадают с ID сервисов, хранятся все иконки сервисов разных размеров и цветности (поэтому небходимо задавать определенный модификатор для иконки).

Зависимости: На уровне переопределения проекта необходимо добавить зависимости от элементов блока `service-icon`, перечисленных в произвольном наборе сервисов входного BEMJSON.

`../myproject/services-table/ services-table.deps.js`

```javascript
({
    shouldDeps: [
        {
            block: 'service-icon',
            elems: [
                {elem: 'images', mods: {color: 56}},
                {elem: 'maps', mods: {color: 56}}
            ]
        }
    ]
});
```
В блоке есть возможность задавать сервисы в сокращенной форме – [поле items](#fields-items). Рекомендованный способ. Используется только в сокращенной форме записи BEMJSON блок, без поля `content`.


<a name="elems-all"></a>
#### Элемент `all`

Добавляет псевдокнопку «Все сервисы», после основного набора сервисов. По нажатию выполняет переход на страницу со списком [всех сервисов Яндекса](http://www.yandex.ru/all) для текущего языкового региона. Используется в развернутой BEMJSON-декларации блока, с полем `content`.

```javascript
{
    block: 'services-table',
    content: [
        // ...
        {
            elem: 'all'
        }
    ]
}
```
Для добавления элемента можно использовать шорткат – [поле all](#fields-all). Используется только с [полем items](#fields-items). 

```js
{
    block: 'services-table',
    items: [
        // ...
    ],
    all: true
}
```
<Зависимости> нужно добавлять для all в произвольном наборе?

<a name="features"></a>
### Особенности реализации 
**Верстка**

* Блок `services-table` представлен блочной таблицей (`display:table`) c максимальной шириной 800px. Ширина блока определяется контентом, но не превышает 800px. При необходимости на уровне сервиса ее можно изменить.

* Элементы блока `item` фиксированного размера, по умолчанию – 160 на 100 px.

**Локализация**

Текст в блоке автоматически локализуется, на основе значения глобального параметра `lang` из `i-global`. Значение по умолчанию: `ru`.
