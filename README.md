# Инструкция Form Generator

Документация создания полей формы по json-подобному описанию. 

### Структура Form Generator
```js
  type Form = {
    titleTranslaterKey: string,
    buttonLabelTranslaterKey?: string,
    fields: FormField[]
  }
```

```js
  type FormField = {
    type: FieldType,
    field: string,
    titleTranslaterKey: string,
    placeholderTranslaterKey?: string,
    defaultValue?: string[] | string | number,
    itemsServerKey?: string,
    hintTranslaterKey?: string,
    validations?: FormValidation[],
    required?: boolean
  }
```

```js
  type FieldType = 'input' | 'textarea' | 'list' | 'audio' | 'multiselect' | 'radio'
```

```js
  type FormValidation = {
    pattern: string,
    flags?: string,
    errorMessageTranslaterKey: string,
  }
```

### Типы полей:

- [input](#input)
- [textarea](#textarea)
- [list](#list)
- [multiselect](#multiselect)
- [radio](#radio) – список элементов с выбором одного
- [audio](#audio) - выпадающий список элементов с выбором одного и возможность догрузить свое аудио

<a id="input"></a>
## Input

**Описание:** Одиночное текстовое поле.  

**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
  {
    type: 'input',
    field: 'password',
    titleTranslaterKey: 'Password',
    placeholderTranslaterKey: 'Enter password...',
    hintTranslaterKey: "Password must contains at least 8 symbols...",
    validations: [
      {
        pattern: '.{8,}',
        flags: 'g',
        errorMessageTranslaterKey: '8+ symbols',
      }, {
        pattern: '[A-Z]',
        errorMessageTranslaterKey: 'Password must contains at least one capital A-Z',
      }
    ],
  }
```


<a id="textarea"></a>
## Textarea

**Описание:** Текстовое поле с переносом строки.  
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
  {
    type: 'textarea', 
    field: 'description',
    titleTranslaterKey: 'Description',
    placeholderTranslaterKey: 'Type comment...',
  }
```


<a id="list"></a>
## List

**Описание:** Выпадающий список элементов с выбором одного  
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`itemsServerKey` – ключ для получения элементов с сервера  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
  {
    type: 'list',
    field: 'strategy',
    titleTranslaterKey: 'Strategy', 
    placeholderTranslaterKey: 'Select ring strategy...',
    itemsServerKey: 'key1',
    defaultValue: 'item2'
  }
```


<a id="multiselect"></a>
## Multiselect

**Описание:** Выпадающий список элементов с выбором нескольких  
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`itemsServerKey` – ключ для получения элементов с сервера  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
  {
    type: 'multiselect',
    field: 'extensions',
    titleTranslaterKey: 'Extensions',
    placeholderTranslaterKey: 'Select members...',
    itemsServerKey: 'key1',
    defaultValue: []
  }
```

