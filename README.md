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

- **input** – текстовое поле
- **textarea** – текстовое поле с переносом строки
- **list** – выпадающий список элементов с выбором одного
- **multiselect** – выпадающий список элементов с выбором нескольких
- **radio** – список элементов с выбором одного
- **audio** - выпадающий список элементов с выбором одного и возможность догрузить свое аудио

# Типы полей:
