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
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 9/3.png" />

### 🧠 AccountTriggerHandler Class  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 9/4.png" />

## ✅ Hands On Practice



## 🎉 Happy Learning 🎉