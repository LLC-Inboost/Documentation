# Конструктор фільтрів

<details>
  <summary>Діаграма</summary>
  <img width="4009" alt="ConstructorFilterDiagram" src="https://user-images.githubusercontent.com/74597949/212402333-3fc2f248-00b7-47f6-99ad-37a1ed3add0e.png">
</details>

## API

```ts
// Модель аккордеону
property?: string; // key to fill filter
caption: MultiLanguageValue[]; // label for accordion
type: EDynamicFilterType;
listForSelect?: SelectOptionData[];
accumulator?: Record<string, unknown> | Record<string, unknown>[];
id: string;

enum EConstructorFilterType {
    "stringArray",
    "dateRage",
    "selectMulti",
    "selectSingle",
    "selectMultiOnly",
    "selectSingleOnly",
    "fields",
}

enum ELogicOperatorConstructorFilters {
    Equals = 1,
    DoesNotEqual = 2,
    IsGreaterThan = 3,
    IsGreaterThanOrEqualTo = 4,
    IsLessThan = 5,
    IsLessThanOrEqualTo = 6,
    IsNull = 7,
    IsNotNull = 8,
    Contains = 9,
    NotContains = 10,
    In = 11,
    NotIn = 12,
    StartWith = 100,
}
```

### Приклад конструктору
```ts
// Ключ виступає роутом для сторінки
"/clients/list/test": [
```

```ts
      {
          caption: [{ lang: Languages.UA, value: "stringArray" }],
          property: "UserPhoneNumber",
          type: EDynamicFilterType.stringArray,
          id: "test_id",
      },
```
 <img width="395" alt="Screenshot 2023-01-20 at 12 02 04" src="https://user-images.githubusercontent.com/74597949/213668623-373e62e5-a258-4efa-8eb2-a2b512ef59d4.png">
 
```ts
{
    caption: [{ lang: Languages.UA, value: "datepicker" }],
    property: "dates",
    type: EDynamicFilterType.dateRange,
    id: "test_id2",
}
```
 <img width="395" alt="Screenshot 2023-01-20 at 12 02 09" src="https://user-images.githubusercontent.com/74597949/213668674-622dc398-7ae9-4bd1-a1e7-47b005b7bf93.png">
 
```ts
{
    caption: [{ lang: Languages.UA, value: "fields" }],
    type: EDynamicFilterType.fields,
    id: "test_id3",
}
```
      <img width="395" alt="Screenshot 2023-01-20 at 12 02 24" src="https://user-images.githubusercontent.com/74597949/213668844-984443b7-fd58-4765-a745-14dca9407200.png">
      
```ts
{
    caption: [{ lang: Languages.UA, value: "selectMulti" }],
    type: EDynamicFilterType.selectMulti,
    property: "selectMulti",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id4",
}
```
      <img width="395" alt="Screenshot 2023-01-20 at 12 02 31" src="https://user-images.githubusercontent.com/74597949/213668888-add2d6fd-56df-4d4a-a712-7659614b8e26.png">
      
```ts
{
    caption: [{ lang: Languages.UA, value: "selectSingle" }],
    type: EDynamicFilterType.selectSingle,
    property: "selectSingle",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id5",
}
```
      <img width="395" alt="Screenshot 2023-01-20 at 12 02 38" src="https://user-images.githubusercontent.com/74597949/213668930-0e4be0f2-8ae0-497e-9b81-1a55c4037c5e.png">
```ts
{
    caption: [{ lang: Languages.UA, value: "selectMultiOnly" }],
    type: EDynamicFilterType.selectMultiOnly,
    property: "selectMultiOnly",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id6",
}
```
      <img width="395" alt="Screenshot 2023-01-20 at 12 02 54" src="https://user-images.githubusercontent.com/74597949/213668999-54955405-9fd5-4f77-a306-8e24a2d9af47.png">
      
```ts
{
    caption: [{ lang: Languages.UA, value: "selectSingleOnly" }],
    type: EDynamicFilterType.selectSingleOnly,
    property: "selectSingleOnly",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id7",
}
```
      <img width="395" alt="Screenshot 2023-01-20 at 12 02 57" src="https://user-images.githubusercontent.com/74597949/213669044-5f0a2e67-c39b-4513-ab2d-5d3adccabbfc.png">

