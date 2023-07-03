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

- input
- [textarea](#textarea)
- list – выпадающий список элементов с выбором одного
- multiselect – выпадающий список элементов с выбором нескольких
- radio – список элементов с выбором одного
- audio - выпадающий список элементов с выбором одного и возможность догрузить свое аудио

## Input

**Описание:** Одиночное текстовое поле.  

**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`placeholderTranslaterKey` (?) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (?) – текст подсказки (ключ из словаря)  
`validations` (?) – массив объектов валидаций (FormValidation[])  

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
