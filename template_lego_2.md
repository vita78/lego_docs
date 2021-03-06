# Название блока 

**Статус блока**: <*Выберите нужный вариант*>
    
> `unstable`  (*для блока с нестабильным API*),   
 `deprecated`, в версии X.X будет удален [ в пользу блока [название_блокаV](#name_newblock.md) ] (*для устаревшего блока или версии блока*)

Блок предоставляет <*Выберите нужный вариант*>
>компонент интереса для ...  
 шаблон, создающий набор HTML-элементов ...  
 СSS-класс, реализующий ...  
 набор JS-классов, реализующий ...
 
 Вспомогательный блок, используемый в составе блока [название_блока](#name_ownerblock) для... 

<[Краткое описание блока](guideline.md/#block-definition)>
 
[Особенности реализации](#feuterus). (*Опциональная ссылка, указывается для новой версии блока и подробного описания причин изменения и др. полезной информации*)  

## Обзор

> **Важно!** В таблицах:  
> 
 * Сначала располагаются обязательные данные, затем опциональные. 
 * **Обязательный** (*Признак для обязательных данных. Указывается **перед** «кратким описанием».*)
 * Уровень переопределния: `название уровня` (*Для данных с уровня переопределения отличного от `common`. Указывается  **после** «краткого описания».*)  
Допустимые значения: `desktop`, `touch-pad`, `touch-phone` (в указанном порядке, после `common`).

> Пример обязательной сущности с уровня определения `desktop`
>
| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [Название модификатора](#modifiers-name)  | ['значение 1'](#) | BEMJSON| **Обязательный**. Краткое описание. Уровень переопределения: `desktop`. |

### Элементы блока

Cпособы использования: `BEMJSON` (другие варианты не предусмотрены).

| Элемент | Описание |
| --------| -------- |
| [Название элемента](#elems-name) (*якорь на соответствующий заголовок*) |[**Обязательный**.] Краткое описание. [Уровень переопределения: `desktop`, `touch-pad`, `touch-phone` (*Выберите необходимое значение*)] |
 
### Модификаторы блока

>*Пример последовательности модификаторов: `type`, `theme`, `size`, `mode`, `disabled`, `focused`, `togglable`, `pressed`, `hovered`.*

>*Допустимые способы использования: `JS`, `BEMJSON`, `—` (нет возможности устанавливать вручную).*

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [Название модификатора](#modifiers-name) (*якорь на соответствующий заголовок* ) | ['значение 1'](#modifiers-name-1), ['значение 2'](#modifiers-name-2) (*якорь на соответствующий заголовок* ) | BEMJSON, JS (*Выберите необходимое значение*) | [**Обязательный**.] Краткое описание. [Уровень переопределения: `desktop`, `touch-pad`, `touch-phone` (*Выберите необходимое значение*)] |

### Специализированные поля блока

>*Пример последовательности полей: `name`, `val`, `text`, `url`, `icon`, `title`, `id`, `tabIndex`.*

>*Допустимые типы данных: `String`, `Number`, `Boolean`, `Array`, `BEMJSON`.*

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [Название поля](#fields-name) (*якорь на соответствующий заголовок* | Тип данных | [**Обязательный**.] Краткое описание. [Уровень переопределения: `desktop`, `touch-pad`, `touch-phone` (*Выберите необходимое значение*)]. |


### JS-параметры блока

| Параметр | Тип | Значение по умолчанию | Описание |
| -------- | --- | --------------------- | -------- |
| [Название параметра](#params-name1) (*якорь на соответствующий заголовок*) |Тип данных | `Значение по умолчанию` | Краткое описание.  |

## Подробнее

<Описание важных аспектов блока не привязанных к структуре документа. Например работа с текстом, иконками и т.п.>

<a name="elems"></a>
### Элементы блока

<a name="elems-name"></a>
#### Элемент `название элемента`

Элемент предоставляет <*Выберите нужный вариант*>

        шаблон для ...
        набор специализированных полей для ...
        СSS-класс, реализующий ...
        JS-класс, реализующий ...

Элемент дополняет <*Выберите нужный вариант*>
        
        базовый блок набором методов (свойств) для ...

Обязательный элемент. *Для необязательных элементов признак не указывается*. 

**Уровень переопределения**: *Указывается, если уровень отличен от `common`. Для `common` – удаляется*.

<Зависимости> *Указывается для опциональных сущностей*

<Описание> 

<Пример

##### Модификаторы элемента блока

>*Пример последовательности модификаторов: `type`, `theme`, `size`, `mode`, `disabled`, `focused`, `togglable`, `pressed`, `hovered`.*

>*Допустимые способы использования: `JS`, `BEMJSON`, `—` (нет возможности устанавливать вручную).*

| Модификатор элемента| Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | --------------------- | -------- |
| [Название модификатора](##elems-name-modifiers-name) (*якорь на соответствующий заголовок* ) | `'значение 1'`, `'значение 2'` | BEMJSON, JS (*Выберите необходимое значение*) |[**Обязательный**.]  Краткое описание. |

<Пример>

##### Специализированные поля элемента блока

| Поле элемента | Тип | Описание |
| ---- | --- | -------- |
| [Название поля](#elems-name-fields-name) (*якорь на соответствующий заголовок*) | Тип данных | [**Обязательный**.] Краткое описание. |

>*Описание доопределения/переопределения элемента и пример для нестандартного случая (при наличии)*

<Пример>

##### JS-параметры элемента блока

| Параметр элемента | Тип | Значение по умолчанию | Описание |
| -------- | --- | --------------------- | -------- |
| [Название параметра](#params-name1) (*якорь на соответствующий заголовок*) |Тип данных | `Значение по умолчанию` | Краткое описание.  |

<Пример>

<a name="modifiers"></a>
### Модификаторы блока

<a name="modifiers-name"></a>
#### Модификатор `название модификатора`

> *Если допустимые значения можно описать лаконично, оформляем данные таблицей*, иначе подразделами.
> 
> **Значение по умолчанию** (*Признак для значения по умолчанию модификатора, указывается перед «кратким описанием».*)

| Допустимые значения | Способ использования | Описание |
| ------------------- | ------------------- | -------------------- | ---------|
| ['значение 1'](#якорь на пример)|BEMJSON, JS (*Выберите необходимое значение*) | [**Значение по умолчанию**.] Краткое описание. [Уровень переопределения: `название уровня`]. |

**Допустимые значения**: ['значение 1'](#modifiers-name-1), ['значение 2'](#modifiers-name-2).  (*якорь на соответствующий заголовок* ) *Обратите внимание, строчные значения заключаются в одинарные вертикальные кавычки и бэктики.*

**Значение по умолчанию**: *Если нет, ставится дефис*.  Обязательный модификатор. *Для необязательных модификаторов признак не указывается*.

**Способ использования**: BEMJSON, JS. *Выберите нужное значение.*

**Уровень переопределения**: *Указывается, если уровень отличен от `common`. Для `common` – удаляется*.

<!--Подключение зависимость на проекте от модификатора `имя модификатора` [и необходимых значений] для `имя_сущности_для_которой_декларируется_зависимость`. -->
<Зависимости> *Указывается для опциональных сущностей*

<Описание>

<Пример>

>*Описание доопределения/переопределения элемента и пример для нестандартного случая (при наличии)*

<a name="modifiers-name-1"></a>
##### Смысловое название блока с примененным модификатором (модификатор `название модификатора` в значении `значение 1`)

<Описание>

<Пример>

<a name="modifiers-name-2"></a>
##### Смысловое название блока с примененным модификатором (модификатор `название модификатора` в значении `значение 2`)

<Описание>

<Пример>

<a name="modifiers-name"></a>
#### Модификатор `название модификатора`

**Допустимое значение**: `булево значение`. *Обратите внимание, булевы значения заключаются только в бэктики.*

**Способ использования**: `BEMJSON`, `JS`. *Выберите нужное значение.*

<Описание>

<Пример>

<a name="declfields"></a>
### Специализированные поля блока

<a name="declfields-field"></a>
#### Поле `название поля`

**Тип**: `String`, `Number`, `Array`, `Boolean`. *Выберите нужный тип данных. Для полиморфных полей типы разделяются знаком `|`*

**Значение по умолчанию**: *Если нет, ставится дефис*.  Обязательное поле. *Для необязательных полей признак не указывается*.

**Уровень переопределения**: *Указывается, если уровень отличен от `common`. Для `common` – удаляется*.

<Зависимости> *Указывается для опциональных сущностей*

<Описание>

<Пример>

<a name="declparams"></a>
### JS-параметры блока

<a name="params-name"></a>
#### Поле `название параметра`

**Тип**: `String`, `Number`, `Array`, `Boolean`. *Выберите нужный тип данных. Для полиморфных параметров типы разделяются знаком `|`*

**Значение по умолчанию**: *Если нет, ставится дефис*.  Обязательный параметр. *Для необязательных параметров признак не указывается*.

**Уровень переопределения**: *Указывается, если уровень отличен от `common`. Для `common` – удаляется*.

<Описание>

<Пример>

<a name="features"></a>
### Особенности реализации 

> Опциональный раздел. Содержит важные особенности реализации. Может включать следующие пункты (*в виде маркированного списка*):
<[Подробное описание блока](guideline.md/#block-description)>

> При необходимости описываются
> *Для составного блока*  
 
Реализация блока включает в себя блоки:

* [название_блока1](ссылка на блока2) (*Ссылка на документацию блоков на Лего-сайте.*)
* [название_блока2](ссылка на блока2)

>*Если функциональность блока базируется на типовом элементе формы* 
 
Функциональность блока основана на типовом элементе формы `<html-элемент>`. (* [Типовые элементы интерфейса](https://ru.wikipedia.org/wiki/Элемент_интерфейса).*)


* Деградации блока в IE версии X.
* Клавиатурное управление
    
   >**Клавиша** – описание выполняемого действия.  
   **Клавиша** + **Клавиша** – описание выполняемого действия (*для сочетания клавиш*).
* ...