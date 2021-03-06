# button2 

**Статус блока**: в разработке.

Блок предоставляет компонент интерфейса для создания различных типов кнопок. 

Основные [отличия от предыдущей версии блока button](#features). 


## Обзор

### Модификаторы блока

Модификатор | Допустимые значения | Способы установки | Описание
--- | --- | --- | ---
[type](#_type) |  ['link'](#_type_slink), ['submit'](#_type_submit), ['check'](#_type_check), ['radio'](#_type_radio) | BEMJSON | Тип кнопки. **По умолчанию** обычная кнопка.
[theme](#_theme) | `'normal'`, `'pseudo'`, `'action'`, `'clear'` | BEMJSON, JS | **Обязательный**. Стилевое оформление.
[size](#_size) | `'xs'`, `'s'`, `'m'` | BEMJSON, JS | **Обязателный**. Размер кнопки.
[pin](#_pin) | `'round-clear'`, `'clear-round'`, `'round-brick'`, `'brick-round'`, `'brick-clear'`, `'clear-brick'`, `'brick-brick'`, `'clear-clear'` | BEMJSON, JS | Форма уголков и видимость сторон кнопки. **По умолчанию** все уголки скруглены и стороны видимы. 
[width](#_width) | `'aut'`, `'max'` | BEMJSON, JS | Ширина блока. **По умолчанию** кнопка растягивается по ширине текста.
[checked](#_checked) |  `yes` | BEMJSON, JS | Кнопка вжата. Используется для кнопок с модификатором `type` в значении `check` и `radio`.
[disabled](#_disabled) | `'yes'` | BEMJSON, JS | Неактивное состояние.
[focused](#_focused) | `'yes'` | JS | Фокус на кнопке.
[pressed](#_pressed) | `'yes'` | – | Кнопка нажата.
[hovered](#_hovered) | `'yes'` | – | Наведение курсором. Доступен на desktop-уровне.

### Специализированные поля блока

Поле | Тип | Описание
--- | --- | ---
[text](#fields-text) | String | Текст кнопки (не путать с полем `content`). Сокращенная форма использования [элемента text](#elems-text). 
[icon](#elems-icon) | BEMJSON | Иконка кнопки. Рекомендуется для использования без текста. Формируется блоком [icon](#). Сокращенная форма использования элемента `icon`. 
[iconLeft](#elems-icon) | BEMJSON | Иконка кнопки слева от текста. 
[iconRight](#elems-icon) | BEMJSON | Иконка кнопки справа от текста. 
`content` | BEMJSON | Переопределяет содержимое кнопки заданное по умолчанию. Используется для более гибкой настройки.
`name` | String | Значение HTML-атрибута `name`. 
`val` | String | Значение HTML-атрибута `value`. 
`url` | String | Значение HTML-атрибута `href`. Используется только для кнопок-ссылок (модификатор `type` со значением `link`).
`target` | String | Значение HTML-атрибута `target`. Используется только для кнопок-ссылок (модификатор `type` со значением `link`).
`title` | String | Значение HTML-атрибута `title`. 
`id` | String | Значение HTML-атрибута `id`. 
`tabIndex` | String | Значение HTML-атрибута `tabindex`. 

### Элементы блока

Cпособы использования: `BEMJSON`.

| Элемент | Описание |
| --------| -------- |
| [text](#elems-text) | Текст кнопки. |
| [icon](#elems-icon)| Иконка кнопки. |


## Подробнее

Блок `button2` предоставляет расширенные возможности для создания кнопки. Позволяет изменять поведение, состояние, содержимое, размер и внешний вид кнопок.

Функциональность блока основана на стандартной кнопке `<button атрибуты>`,  для ссылок – `<a>`. 

<a name="modifiers"></a>
### Модификаторы блока

<a name="_type"></a>
#### Модификатор `type` (1 вариант)

Допустимые значения: ['link'](#_type_link), ['submit'](#_type_submit), ['check'](#_type_check), ['radio'](#_type_radio).

Значение по умолчанию: `-`. Обычная кнопка.

Способ использования: `BEMJSON`.

Подключите в зависимости модификатор `type` с нужными значениями. 

**Обычная кнопка**

```bemjson
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    text: 'Кнопка'
}
```

<a name="_type_link"></a>
##### Кнопка-ссылка (модификатор `type` в значении `link`)

Создает кнопку, которая обеспечивает переход по адресу, указанному в поле [url](#url).
Для кнопки-ссылки используется тег `<a>` вместо `<button>`. Передать значения полям `url` и `target` в BEMJSON можно с помощью методов [getUrl()](#) и [setUrl()](#) в JS.

```bemjson
{
    block: 'button2',
    mods: {type: 'link', theme: 'normal', size: 's'},
    text: 'Link',
    url: '//yandex.ru'
}
```

<a name="_type_submit"></a>
##### Кнопка отправки формы (модификатор `type` в значении `submit`)

Cоздает кнопку, которая отправляет данные формы на сервер. Кнопка такого типа всегда должна располагаться в форме. Отличается от обычной кнопки дополнительным атрибутом `type="submit"`.

```bemjson
{
    block: 'button2',
    mods: {type: 'submit', theme: 'normal', size: 's'},
    text: 'Submit'
}
```

<a name="_type_check"></a>
##### Кнопка-переключатель (модификатор `type` в значении `check`)

Создает кнопку, которая последовательным нажатием переключается в два положения: первое нажатие – вдавливает кнопку, второе – приводит в первоначальное состояние.
При переключении состояний добавляется/удаляется модификатор `checked`.

```bemjson
{
    block: 'button2',
    mods: {type: 'check', theme: 'normal', size: 's'},
    text: 'Check'
}
```

<a name="_type_radio"></a>
##### Радиокнопка (модификатор `type` в значении `radio`)

Нажатие на кнопку вдавливает ее, и она может быть приведена в первоначальное состояние только программно. Используется в составе радиогруппы.

Нажатием кнопке добавляется модификатор `checked` со значением `yes`.

```bemjson
{
    block: 'button2',
    mods: {type: 'radio', theme: 'normal', size: 's'},
    text: 'Radio'
}
```

<a name="_type"></a>
#### Модификатор `type` (2 вариант)

Тип кнопки.

Способ использования: `BEMJSON`.

| Допустимые значения | Описание |
| ------------------- | -------- |
|[–](#_type_example)|**Значение по умолчанию**. Обычная кнопка. [Пример](#_type_example)|
|['link'](#_type_link_example)| Кнопка-ссылка, которая обеспечивает переход по адресу, указанному в поле [url](#url). Для кнопки-ссылки используется тег `<a>` вместо `<button>`. Передать значения полям `url` и `target` в BEMJSON можно с помощью методов [getUrl()](#) и [setUrl()](#) в JS. [Пример](#_type_link_example)|
|['submit'](#_type_submit_example)| Кнопка отправки данных формы на сервер. Кнопка такого типа всегда должна располагаться в форме. Отличается от **обычной кнопки** дополнительным атрибутом `type="submit"`.|
|['check'](#_type_check_example)| Кнопка-переключатель. Кнопка такого типа последовательным нажатием переключается в два положения: первое нажатие – вдавливает кнопку, второе – приводит в первоначальное состояние. При переключении состояний добавляется/удаляется модификатор `checked`.|
|['radio'](#_type_radio_example)| Радиокнопка. Нажатие на кнопку вдавливает ее, и она может быть приведена в первоначальное состояние только программно. Используется в составе радиогруппы. Нажатием кнопке добавляется модификатор `checked` со значением `yes`.|

Подключите в зависимости модификатор `type` с нужными значениями. 

<a name="_type_example"></a>
**Обычная кнопка**

```bemjson
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    text: 'Кнопка'
}
```

<a name="_type_link_example"></a>
**Кнопка-ссылка**

```bemjson
{
    block: 'button2',
    mods: {type: 'link', theme: 'normal', size: 's'},
    text: 'Link',
    url: '//yandex.ru'
}
```

<a name="_type_submit_example"></a>
**Кнопка отправки данных**

```bemjson
{
    block: 'button2',
    mods: {type: 'submit', theme: 'normal', size: 's'},
    text: 'Submit'
}
```

<a name="_type_check_example"></a>
**Кнопка-переключатель**

```bemjson
{
    block: 'button2',
    mods: {type: 'check', theme: 'normal', size: 's'},
    text: 'Check'
}
```

<a name="_type_radio_example"></a>
**Радиокнопка**

```bemjson
{
    block: 'button2',
    mods: {type: 'radio', theme: 'normal', size: 's'},
    text: 'Radio'
}
```

<a name="_theme"></a>
### Модификатор `theme`

Стилевое оформление. 

Допустимые значения | Описание
--- | ---
`normal` | Обычная кнопка. Используется во всех случаях, кроме нижеперечисленных.
`pseudo` | Прозрачная кнопка. Используется для цветного фона, чтобы уменьшить акцент на элементе.
`action` | Кнопка для выполнения основного действия на странице.
`clear` | Невидимая кнопка. Активный элемент со всеми признаками кнопки, но без видимых границ. Как правило, границы в интерфейсе не нужны иконкам.

Cпособы установки: `BEMJSON` и `JS`.

Нужно использовать с [модификатором size](). (?)

Необходимо самостоятельно подключить зависимость.

**Обычная кнопка**

```js
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    text: 'Normal'
}
```    

**Псевдокнопка**

```js    
{
    block: 'button2',
    mods: {theme: 'pseudo', size: 's'},
    text: 'Pseudo'
}
```
**Кнопка-действия**

```js
{
    block: 'button2',
    mods: {theme: 'action', size: 's'},
    text: 'Action'
}
```

**Невидимая кнопка**

```js
{
    block: 'button2',
    mods: {theme: 'clear', size: 's'},
    icon: {mods: {type: 'load'}}
}
```

<a name="declfields"></a>
### Специализированные поля блока

<a name="fields-text"></a>
#### Поле `text`

Тип: `String`

Значение по умолчанию: `''`. 

Определяет текст, который отображается на кнопке. Рекомендованный способ. При его использовании текст будет экранирован и размещен в [элементе text](#elems-text).

```bemjson
{
    block: 'button2', 
    text: 'Текст кнопки'
}
```

<a name="elems"></a>
### Элементы блока

<a name="elems-text"></a>
#### Текст кнопки (элемент `text`)

>*ТОDO (подумать: привязывать к полю text, а не к элементу или другому абстрактному разделу, как у Вани? Для icon аналогично)*

Элемент используется для экранирования и размещения текста на кнопке. 

Рекомендованный способ установки текста – поле `text`. При его использовании текст будет экранирован и размещен в элементе `text` (?вспомогательный элемент?).

**Установка текста на кнопке** 

```javascript
// С помощью поля `text`
[{
    block: 'button2', 
    text: 'Текст кнопки'
}
// С помощью элемента `text` (эквивалентно)
{
    block: 'button2',
    content: {elem: 'text', content: xmlEscape('Текст кнопки')}
}]
```

<a name="elems-icon"></a>
#### Иконка кнопки (элемент `icon`)

Элемент используется для установки иконки, которая будет отображаться на кнопке. Иконка задается с помощью блока [icon](#).

Поля `icon`, `iconLeft`, `iconRight` используются для удобного определения и расположения иконки на кнопке.

Чтобы установить иконку в кнопку достаточно передать BEMJSON описывающий иноку в одно из вышеперечисленных полей.
При этом:

* `block: 'icon'` не указывается в BEMJSON  кнопки, так как будет выставляться автоматически; (? это нужно описывать?).
* При передаче иконки в поля `iconLeft` или `iconRight` к ней автоматически примиксуется модификатор (?может класс?) `.button2__icon_side_left` или `.button2__icon_side_right` соответственно, который отвечает за позиционирование иконки слева и справа от текста.
* При передаче иконки в поле `icon` дополнительные модификаторы не примешиваются. Этот способ рекомендуется для установки иконки без текста.
* Иконке устанавливается размер (модификатор `size`) с тем же значением, что и у кнопки.

*Установки иконки для кнопки без текста*

```javascript
// В поле `icon`
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    icon: {mods: {type: 'load'}}
},

// Эквивалентный способ установки иконки с помощью блока `icon`
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    content: {
        block: 'icon'
        mods: {type: 'load', size: 's'},
        mix: {block: 'button2', elem: 'icon'}
    }
}
```

**Установка иконки кнопки слева и справа от текста**

```javascript
{ // В поле iconRight, iconLeft
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    iconLeft: {mods: {type: 'arrow', direction: 'bottom'}},
    iconRight: {mods: {type: 'arrow', direction: 'top'}},
    text: 'Кнопка'
},
// Эквивалентный способ установки иконки с помощью блока `icon`
{
    block: 'button2',
    mods: {theme: 'normal', size: 's'},
    content: [
        {
            block: 'icon'
            mods: {type: 'arrow', direction: 'bottom', size: 's'},
            mix: {block: 'button2', elem: 'icon', elemMods: {side: 'left'}}
        },
        {
            block: 'icon'
            mods: {type: 'arrow', direction: 'top', size: 's'},
            mix: {block: 'button2', elem: 'icon', elemMods: {side: 'right'}}
        },
        {elem: 'text', content: xmlEscape('Кнопка')}
    ]
}
```

```javascript
{
    block: 'example-area',
    content: [
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            icon: {mods: {type: 'load', direction: 'bottom'}}
        }, '&nbsp;&nbsp;',
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            icon: {mods: {type: 'arrow', direction: 'bottom'}}
        }, '&nbsp;&nbsp;',
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            iconLeft: {mods: {type: 'arrow', direction: 'left'}},
            text: 'Кнопка'
        }, '&nbsp;&nbsp;',
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            iconRight: {mods: {type: 'arrow', direction: 'right'}},
            text: 'Кнопка'
        }
    ]
}
```
Необходимо самостоятельно подключить зависимость элемента `icon` и от необходимых типов иконок.


---
**NB** На гайдах иконка-стрелка (`icon_type_arrow`) немного шире, чем другие иконки, благодаря чему стрелка выглядит более прижатой к тексту.

---

<a name="features"></a>
### Особенности реализации 

> Опциональный раздел. Содержит важные особенности реализации. Может включать следующие пункты (*в виде маркированного списка*):

* Деградации блока в IE версии X.
* Клавиатурное управление
    
   >**Клавиша** – описание выполняемого действия.  
   **Клавиша** + **Клавиша** – описание выполняемого действия (*для сочетания клавиш*).
* ...