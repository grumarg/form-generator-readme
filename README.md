<a id="readme-top"></a>
# Инструкция Form Generator

Документация создания полей формы по json-подобному описанию. 

### Структура Form Generator
```js
  type Form = {
    titleTranslaterKey: string,
    buttonLabelTranslaterKey?: string,
    tabs: FormTab[]
  }
```

```js
  type FormTab = {
    titleTranslaterKey: string,
    fields: FormField[],
    expertMode?: boolean
  }
```  

```js
  type FormField = {
    type: FieldType,
    field: string,
    titleTranslaterKey: string,
    placeholderTranslaterKey?: string,
    defaultValue?: ListItem[] | ListItem | string | number,
    apiDataUrl?: string,
    staticList?: ListItem[],
    hintTranslaterKey?: string,
    validations?: FormValidation[],
    required?: boolean
  }
```

```js
  type ListItem = {
    id?: MongoId,
    keyword: string,
    content: string
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

Необязательное поле `expertMode` в FormTab отвечает за отображение дополнительной вкладки для описания дополнительных полей.  
Такой Tab может быть только один.  
<img width="735" alt="Снимок экрана 2023-11-03 в 20 27 33" src="https://github.com/grumarg/form-generator-readme/assets/70900990/2ca69ac7-7983-4eb6-958a-be79c4483ea7">


### Типы полей:

- [input](#input)
- [textarea](#textarea)
- [list](#list)
- [multiselect](#multiselect)
- [radio](#radio)
- [audio](#audio)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

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
<p align="right">(<a href="#readme-top">back to top</a>)</p>


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
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<a id="list"></a>
## List

**Описание:** Выпадающий список элементов с выбором одного  
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`apiDataUrl` – серверный путь для получения данных  
`staticList` – список элементов по умолчанию (альтернатива `apiDataUrl`)  
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
    defaultValue: 'item2',
    apiDataUrl: '/builder/get-list/weekDays' // или staticList: [{ keyword: 'Monday', content: 'mon' }]
  }
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<a id="multiselect"></a>
## Multiselect

**Описание:** Выпадающий список элементов с выбором нескольких  
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`apiDataUrl` – серверный путь для получения данных  
`staticList` – список элементов по умолчанию (альтернатива `apiDataUrl`)  
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
    apiDataUrl: '/builder/get-list/weekDays' // или staticList: [{ keyword: 'Monday', content: 'mon' }, { keyword: 'Tuesday', content: 'tue' }]
    defaultValue: [{ keyword: 'Monday', content: 'mon' }]
  }
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="radio"></a>
## Radio

**Описание:** Список элементов с выбором одного
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`apiDataUrl` – серверный путь для получения данных  
`staticList` – список элементов по умолчанию (альтернатива `apiDataUrl`)  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
  {
    type: 'radio', 
    field: 'true',
    titleTranslaterKey: 'True',
    placeholderTranslaterKey: 'Select sound...', 
    apiDataUrl: '/builder/get-list/YesNoList' // или staticList: [{ keyword: 'Yes', content: 'yes' }, {keyword: 'No', content: 'no' }]
    defaultValue: { keyword: 'Yes', content: 'yes' },
    required: true
  }
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<a id="audio"></a>
## Audio

**Описание:** Выпадающий список элементов с выбором одного и возможностью загрузить своё аудио
  
**Поля:**  
`type` – тип поля  
`field` – ключ поля при отправке данных  
`titleTranslaterKey` – названия поля (ключ из словаря)  
`apiDataUrl` – серверный путь для получения данных  
`staticList` – список элементов по умолчанию (альтернатива `apiDataUrl`)  
`defaultValue` (необязательное) – значение поля по умолчанию  
`placeholderTranslaterKey` (необязательное) – placeholder для поля (ключ из словаря)  
`hintTranslaterKey` (необязательное) – текст подсказки (ключ из словаря)  
`required` (необязательное) – обязательное поле, выводит ошибку, если поле пустое  
`validations` (необязательное) – массив объектов валидаций (FormValidation[])  

**Пример использования:**

```js
 {
    type: 'audio', 
    field: 'sound',
    titleTranslaterKey: 'Sound',
    placeholderTranslaterKey: 'Select sound...',
    staticList: [{ keyword: 'Voice recorder 1', content: '/voices/audio.wav' }] //  или использовать apiDataUrl
  }
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>
