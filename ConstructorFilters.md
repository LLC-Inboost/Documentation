# Конструктор фільтрів

<details>
  <summary>Діаграма</summary>
  <img width="4009" alt="ConstructorFilterDiagram" src="https://user-images.githubusercontent.com/74597949/212402333-3fc2f248-00b7-47f6-99ad-37a1ed3add0e.png">
</details>

## API

```ts
// Модель аккордеону
property?: string; // Поле в яке буде акумулюватись значення
caption: MultiLanguageValue[]; // Опис для аккордеону
type: EDynamicFilterType; // Тип фільтру
listForSelect?: SelectOptionData[];
id: string;

enum EDynamicFilterType {
    stringArray = "stringArray",
    dateRange = "dateRage",
    selectMulti = "selectMulti",
    selectSingle = "selectSingle",
    selectMultiOnly = "selectMultiOnly",
    selectSingleOnly = "selectSingleOnly",
    fields = "fields",
}

enum ELogicOperatorConstructorFilters {
    "equal" = "equal",
    "notEqual" = "notEqual",
    "contains" = "contains",
    "notContains" = "notContains",
    "filled" = "filled",
    "notFilled" = "notFilled",
}
```
