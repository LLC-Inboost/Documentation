# Динамічні елементи правої панелі

*Всі поля очікую с маленької букви

## **ACCORDIONS**
- Type: string | string[]
- Title: { lang: string; value: string } [] *обовязкове
- DefaultOpen: boolean чи буде відкритий аккордеон одразу
- [Properties](#Properties)

Якщо додати в джейсон таку саму модель що і для конкретної ноди але с type: “All”, ці елементи будуть у всіх нодах

Якщо додати в конфіг ноди поле excludeDynamicElementsForAllNodes зі значенням true то всі елементи які мають type:”All”, не будуть показані в ноді


## <a name="Properties"></a> Properties
При передачі $css[key] той елемент для якого призначений key буде без дефолтних стилів а будуть вставленні стилі які будуть передані в це поле,
Це повинен бути валідний css (напряму без селектора, наприклад $css: {wrappper: “display:flex;margin:50px;”})
[тут про css](https://www.w3schools.com/css/css_syntax.asp)

- [IncludesVariables][1] string[] <br/>
     "fromNode" - все що динамічно виймається з keyForSave, <br/>
     "fromResponse" те що прилітає с іншого беку в нодах інтеграцій, <br/>
     "default" те що прилітає с апішки, <br/>
     "all" <br/>

### **Type Container**
- Index: number *обовязкове
- Type:  “Container” *обовязкове
- $css: { container: CSS string }
- InnerElements: [Properties](#Properties) *обовязкове (така сама структура тільки вложена)
- EntityParentPropertyLength: number, макс довжина масива в який будуть записуватись проперті з контейнера
- EntityParentSingle: boolean, чи буде контейнер з EntityParentProperty працювати з обєктом чи з масивом обєктів
- EntityParentProperty: ключ в інтерфейсі ноди, якщо передати це поле то всі проперті вложені в контейнер станануть вложеним обєктом в масив с цим ключом,
- EntityParentTextToAddButton: MultiLanguageValue переклад для кнопки додавання сутності в масив entityParentProperty, по дефолту назва "entity add"
---
### **Type Text**
- Caption: { lang: string; value: string } [] це опис для текст ареї
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди  { lang: string; value: string }[] *обовязкове
- Type:  “Text” *обовязкове
- Maxlength: макс довжина тексту в одному об’єкті {lang, value <— цього поля}
- $css: { wrapper: CSS string }
- Placeholder: string
- MultiLanguage: boolean (по дефолту true) чи буде записуватись значення в форматі {lang, value}[] чи просто string
- IncludesVariables[1]: змінні для тексту, по дефолту "all"
---
### **Type TextInput** 
- Caption: { lang: string; value: string } [] це опис для текст ареї
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди  *обовязкове
- Type:  “TextInput” *обовязкове
- Maxlength: макс довжина тексту в одному об’єкті {lang, value <— цього поля}
- $css: { wrapper: CSS string }
- Placeholder: string
- MultiLanguage: boolean (по дефолту false) чи буде записуватись значення в форматі {lang, value}[] чи просто string
- IncludesVariables[1]: змінні для тексту, по дефолту "all"
- TextInputType: "arrayModel" Якщо передати це поле то створиться інпут с кнопкою який буде записувати масив строк в поле property,
---
### **Type Checkbox**
- Caption: { lang: string; value: string } [] це опис
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди string *обовязкове
- $css: { wrapper: CSS string, caption: CSS string, svg: CSS string }
- Type:  “Checkbox” *обовязкове
---
### **Type Radio**
- Caption: { lang: string; value: string } [] це опис
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди string *обовязкове
- $css: { wrapper: CSS string, caption: CSS string, svg: CSS string }
- Type: “RadioButton” *обовязкове
- Value: true | false *обовязкове
---
### **Type Select**
- Caption: { lang: string; value: string } [] це опис 
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди string *обовязкове
- $css: { wrapper: CSS string, caption: CSS string,  }
- Type: “Select” *обовязкове
- SelectType: “single” | “multi” | "searchMulti" | "searchSingle" в залежності від цього типу будуть свг-шки в оціях або радіо або чекбокс *обовязкове і записуватись в проперті або один елемент або масив елементів
- List: {label:string, value: any}[] список с опціями для селекту *обовязкове

#### Приклад двух контейнерів с вложеними пропеті
```json
{
    "type": "All",
    "accordions": [
        {
            "title": [
                {
                    "lang": "UA",
                    "value": "Назва акордеона"
                }
            ],
            "defaultOpen": true,
            "properties": [
                {
                    "index": 0,
                    "maxLength": 80,
                    "type": "Container",
                    "$css": {
                        "container": "display:flex;gap:16px;align-items:center;justify-content:center;padding-top:10px"
                    },
                    "innerElements": [
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Назва імпуту"
                                }
                            ],
                            "index": 0,
                            "property": "ke2k",
                            "type": "TextInput",
                            "placeholder": "custom placeholder"
                        },
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Тайтл імпуту 1"
                                }
                            ],
                            "index": 0,
                            "property": "kek3",
                            "type": "TextInput",
                            "placeholder": "custom placeholder"
                        }
                    ]
                },
                {
                    "caption": [
                        {
                            "lang": "UA",
                            "value": "Назва імпуту"
                        }
                    ],
                    "index": 0,
                    "property": "k4ek",
                    "type": "TextInput",
                    "placeholder": "custom placeholder"
                }
            ]
        },
        {
            "title": [
                {
                    "lang": "UA",
                    "value": "Назва акордеона"
                }
            ],
            "properties": [
                {
                    "index": 1,
                    "type": "Container",
                    "$css": {
                        "container": "display:flex;gap:6px;align-items:center;justify-content:center;padding-top:10px;"
                    },
                    "innerElements": [
                        {
                            "index": 1,
                            "property": "asdasd",
                            "type": "Checkbox"
                        },
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Ключ"
                                }
                            ],
                            "index": 2,
                            "property": "ke12k",
                            "type": "TextInput",
                            "placeholder": "custom placeholder"
                        },
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Значення"
                                }
                            ],
                            "index": 3,
                            "property": "kesd",
                            "type": "TextInput",
                            "$css": {
                                "wrapper": "padding-left:10px;"
                            }
                        }
                    ]
                },
                {
                    "index": 1,
                    "type": "Container",
                    "$css": {
                        "container": "display:flex;gap:6px;align-items:center;justify-content:center;"
                    },
                    "innerElements": [
                        {
                            "index": 1,
                            "property": "asda223sd",
                            "type": "Checkbox"
                        },
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Ключ"
                                }
                            ],
                            "index": 2,
                            "property": "keииии12k",
                            "type": "TextInput",
                            "placeholder": "custom placeholder"
                        },
                        {
                            "caption": [
                                {
                                    "lang": "UA",
                                    "value": "Значення"
                                }
                            ],
                            "index": 3,
                            "property": "kxxcesd",
                            "type": "TextInput"
                        }
                    ]
                }
            ]
        }
    ]
}
```

<img width="240" alt="Screenshot 2022-11-28 at 09 55 25" src="https://user-images.githubusercontent.com/74597949/204223465-4d11c7fe-89ea-4da5-a364-5a48a1cbdbfd.png">
<img width="205" alt="Screenshot 2022-11-28 at 09 55 54" src="https://user-images.githubusercontent.com/74597949/204223552-a73a0752-af7d-46b0-97c7-f9b0ad4cee41.png">

#### Приклад контейнеру з EntityParentSingle
```ts
{
     title: [{ lang: Languages.UA, value: "Назва акордеона" }],
     defaultOpen: true,
     properties: [
         {
             type: ERightPanelPropertyType.container,
             entityParentProperty: "mock" as keyof DialogNode,
             entityParentSingle: true,
             entityParentTextToAddButton: [{ lang: "UA", value: "Custom btn name" }],
             $css: {
                 container:
                     "display:flex;gap:16px;align-items:center;justify-content:flex-start;padding-top:10px;",
             },
             innerElements: [
                 {
                     index: 1,
                     property: "asda223sd",
                     type: ERightPanelPropertyType.checkbox,
                 },
                 {
                     caption: [{ lang: Languages.UA, value: "Ключ" }],
                     index: 2,
                     property: "keииии12k",
                     type: ERightPanelPropertyType.textInput,
                     $css: { wrapper: "width:100%" },
                     placeholder: "custom placeholder",
                 },
                 {
                     caption: [{ lang: Languages.UA, value: "Значення" }],
                     index: 3,
                     property: "kxxcesd",
                     $css: { wrapper: "width:100%" },
                     type: ERightPanelPropertyType.textInput,
                 },
             ],
         },
     ],
 },
```
<img width="803" alt="Screenshot 2023-01-19 at 14 38 01" src="https://user-images.githubusercontent.com/74597949/213444855-bb438d1d-7a2b-4341-b08b-12a0f5440d5a.png">

