# Конструктор фільтрів

<details>
  <summary>Діаграма</summary>
  <img width="4009" alt="ConstructorFilterDiagram" src="https://user-images.githubusercontent.com/74597949/212402333-3fc2f248-00b7-47f6-99ad-37a1ed3add0e.png">
</details>

## API

```ts
// Модель аккордеонуi
interface IConstructorAccordion {
    property?: string; // key to fill filter
    caption: MultiLanguageValue[]; // label for accordion
    type: EDynamicFilterType;
    listForSelect?: SelectOptionData[];
    accumulator?: Record<string, unknown> | Record<string, unknown>[];
    id: string;
    apiForSelect?: string;
    apiForSelectSchema?: ApiForSelectSchema;
    apiForSelectMethod?: "get" | "post";
    apiForSelectLangTo?: "query" | "body";
    apiForSelectKeyForResponseArray?: string;
}

interface ApiForSelectSchema {
    label: string;
    value: string;
}   
 
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

### Динамічні значення в селект з апі
**apiForSelect** \n
При передачі apiForSelect разом с selectSingle | selectMulti | selectMultiOnly | selectSingleOnly
очікувана модель { label:string; value:any }[]
Наприклад: apiForSelect = "getMyDictionary", буде зроблений Post запит на api/getMyDictionary і сет в селект з response.data

**apiForSelectSchema** \n
Якщо у вас кастомна модель з апі і її необхідно промапити то передається схема
Наприклад апі вертає модель [{ Id: 12, CustomValue: "test" }]
Вказується схема { label: "CustomValue", value: "Id"}
І потім в селекті буде відповідно все відображатись з лейблом від ключа CustomValue і значенням Id

**apiForSelectMethod**
Запит на довідник буде через GET або POST 
По дефолту POST

**apiForSelectLangTo** \n
Передача мови до квері або боді
Якщо боді це поле { Lang: "UA" } (тому що так в універсальному апі)
Якщо квері це поле ?lang="UA"
По дефолту боді

**apiForSelectKeyForResponseArray** \n
Якщо данні для селекту не одразу в response.data а в кастомному полі
Наприклад сервер повертає { totalCount: 12, entites: [{label, value}] }
Вказуєш apiForSelectKeyForResponseArray: "entites", і я буду знати що потрібно брати звідти данні

### Приклад конструктору
```ts
// Ключ виступає роутом для сторінки
"/clients/list/test": [ тут масив об'єктів, приклади нижче ]
```

```ts
{
    caption: [{ lang: Languages.UA, value: "stringArray" }],
    property: "UserPhoneNumber",
    type: EConstructorFilterType.stringArray,
    id: "test_id",
}

// в АПІ попаде модель Filter: [{property: "UserPhoneNumber", filterValue: "value, value...", opr: ELogicOperatorConstructorFilters}]
```
 <img width="395" alt="Screenshot 2023-01-20 at 12 02 04" src="https://user-images.githubusercontent.com/74597949/213668623-373e62e5-a258-4efa-8eb2-a2b512ef59d4.png">
 
```ts
{
    caption: [{ lang: Languages.UA, value: "datepicker" }],
    property: "dates",
    type: EConstructorFilterType.dateRange,
    id: "test_id2",
}

// в АПІ попаде модель Filter: [{property: "dates", filterValue: "YYYY-MM-DD, YYYY-MM-DD", opr: ELogicOperatorConstructorFilters}]
```
 <img width="395" alt="Screenshot 2023-01-20 at 12 02 09" src="https://user-images.githubusercontent.com/74597949/213668674-622dc398-7ae9-4bd1-a1e7-47b005b7bf93.png">
 
```ts
{
    caption: [{ lang: Languages.UA, value: "fields" }],
    type: EConstructorFilterType.fields,
    id: "test_id3",
}

// в АПІ попаде модель Filter: [{property: тут проп який юзер вибере з селекту (колонки з універсального АПІ), filterValue: string[], opr: ELogicOperatorConstructorFilters}]
```

 <img width="395" alt="Screenshot 2023-01-20 at 12 02 24" src="https://user-images.githubusercontent.com/74597949/213668844-984443b7-fd58-4765-a745-14dca9407200.png">
    
      
```ts
{
    caption: [{ lang: Languages.UA, value: "selectMulti" }],
    type: EConstructorFilterType.selectMulti,
    property: "selectMulti",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id4",
}
// в АПІ попаде модель Filter: [{property: "selectMulti", filterValue: "value, value...", opr: ELogicOperatorConstructorFilters}]
```

<img width="395" alt="Screenshot 2023-01-20 at 12 02 31" src="https://user-images.githubusercontent.com/74597949/213668888-add2d6fd-56df-4d4a-a712-7659614b8e26.png">

```ts
{
    caption: [{ lang: Languages.UA, value: "selectSingle" }],
    type: EConstructorFilterType.selectSingle,
    property: "selectSingle",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id5",
}

// в АПІ попаде модель Filter: [{property: "selectSingle", filterValue: string, opr: ELogicOperatorConstructorFilters}]
```

   <img width="395" alt="Screenshot 2023-01-20 at 12 02 38" src="https://user-images.githubusercontent.com/74597949/213668930-0e4be0f2-8ae0-497e-9b81-1a55c4037c5e.png">

```ts
{
    caption: [{ lang: Languages.UA, value: "selectMultiOnly" }],
    type: EConstructorFilterType.selectMultiOnly,
    property: "selectMultiOnly",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id6",
}

// в АПІ попаде модель Filter: [{property: "selectMultiOnly", filterValue: "value, value...", opr: ELogicOperatorConstructorFilters}]
```

 <img width="395" alt="Screenshot 2023-01-20 at 12 02 54" src="https://user-images.githubusercontent.com/74597949/213668999-54955405-9fd5-4f77-a306-8e24a2d9af47.png">

```ts
{
    caption: [{ lang: Languages.UA, value: "selectSingleOnly" }],
    type: EConstructorFilterType.selectSingleOnly,
    property: "selectSingleOnly",
    listForSelect: [
        { label: "xx", value: "xx" },
        { label: "ll", value: "ll" },
    ],
    id: "test_id7",
}

// в АПІ попаде модель Filter: [{property: "selectSingleOnly", filterValue: string, opr: ELogicOperatorConstructorFilters}]
```

 <img width="395" alt="Screenshot 2023-01-20 at 12 02 57" src="https://user-images.githubusercontent.com/74597949/213669044-5f0a2e67-c39b-4513-ab2d-5d3adccabbfc.png">
