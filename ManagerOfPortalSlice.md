# Slice ManagerOfPortal


### Код слайсу знаходиться ```\src\slices\manager-of-portal```

### Слайс зберігає дані менеджера отримання за запитом 
```https://adm.inboost.ai:5093/api/Users/GetPortalUser```

### У відповідь на запит приходять дані:
```{
    "userName": "TestUser",
    "lastName": null,
    "userPhoneNumber": "380998218222",
    "lang": "UA",
    "email": null,
    "lastUserChatId": "5387",
    "roleId": "6263C588-7FFA-468F-A78C-2716FB398516",
    "roleName": "Оператор підтримки",
    "userId": 130903,
    "urlPhoto": null,
    "messengers": [
      {userChatId: "5243", messenger: "Web"},
      {userChatId: "422270963", messenger: "Telegram"}
    ],
    "portalInfo": {
        "portalId": 2535,
        "portalName": "pashatesting",
        "userId": 5387,
        "roleId": 4,
        "activityStatusUserId": 1,
        "typeUserId": 1
    }
}
```
### Для отримання данніх зі слайсу, використавуйте метод 
```const managerInfo = useAppSelector((state) => state.managerInfoSlice.managerInfo);``` <br>
де в managerInfo зберігається весь об'єкт менеджера