# Динамічні елементи правої панелі

*Всі поля очікую с маленької букви

## **ACCORDIONS**
- Title: { lang: string; value: string } [] *обовязкове
- DefaultOpen: boolean чи буде відкритий аккордеон одразу
- [Properties](#Properties)

Якщо додати в джейсон туже модель що і для конкретної ноди але с type: “All”, ці елементи будуть у всіх нодах

Якщо додати в конфіг ноди поле excludeDynamicElementsForAllNodes зі значенням true то всі елементи які мають type:”All”, не будуть показані в ноді


### <a name="Properties"></a>
При передачі $css[key] той елемент для якого призначений key буде без дефолтних стилів а будуть вставленні стилі які будуть передані в це поле,
Це повинен бути валідний css (напряму без селектора, наприклад $css: {wrappper: “display:flex;margin:50px;”})
[тут про css](https://www.w3schools.com/css/css_syntax.asp)
---
### **Type Container**
- Index: number *обовязкове
- Type:  “Container” *обовязкове
- $css: { container: CSS string }
- innerElements: [Properties](#Properties) *обовязкове (така сама структура тільки вложена)
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
---
### **Type TextInput** 
- Caption: { lang: string; value: string } [] це опис для текст ареї
- Index: number *обовязкове
- Property: ключ від інтерфейсу ноди  { lang: string; value: string }[] *обовязкове
- Type:  “TextInput” *обовязкове
- Maxlength: макс довжина тексту в одному об’єкті {lang, value <— цього поля}
- $css: { wrapper: CSS string }
- Placeholder: string
- MultiLanguage: boolean (по дефолту false) чи буде записуватись значення в форматі {lang, value}[] чи просто string
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
- SelectType: “single” | “multi” в залежності від цього типу будуть свг-шки в оціях або радіо або чекбокс *обовязкове і записуватись в проперті або один елемент або масив елементів
- List: {label:string, value: any}[] список с опціями для селекту *обовязкове
