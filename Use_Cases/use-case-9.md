# 🧩 Scenario  
### 📌 If an Account with Industry as Agriculture and Type as Prospect is updated and Ownership is set to Private, do not allow user to save the record  

---

## 🛠️ Solution  
### ⚡ AccountTrigger

```apex
trigger AccountTrigger on Account (before update) {
    
    if(Trigger.isUpdate && Trigger.isBefore){
        AccountTriggerHandler.handleBeforeInsert(Trigger.NEW, Trigger.oldMap);
    }

}
```

### 🧠 AccountTriggerHandler Class

```apex
public class AccountTriggerHandler {
    
    public static void handleBeforeInsert(List<Account> newRecord, Map<Id, Account> oldMap){
        for(Account newAcc : newRecord){
            if(newAcc.Industry == 'Agriculture' && newAcc.Type == 'Prospect'){
                if(oldMap.get(newAcc.Id).Ownership != newAcc.Ownership && newAcc.Ownership == 'Private'){
                    newAcc.addError('Ownership cannot be modified!');
                }
            }
        }
        
    }

}
```

## 📄 Trigger   
### ⚡ AccountTrigger  
<img width="955" height="335" alt="3" src="https://github.com/user-attachments/assets/23a23ec7-cf4a-43c2-bcd6-a944fdc70c5b" />


### 🧠 AccountTriggerHandler Class  
<img width="1278" height="559" alt="4" src="https://github.com/user-attachments/assets/8c845b56-fe26-4341-8ba8-004e4de6a18f" />


## ✅ Hands On Practice
https://github.com/user-attachments/assets/fc317c69-9a8c-4dd7-887b-d238740f2a2d




## 🎉 Happy Learning 🎉
