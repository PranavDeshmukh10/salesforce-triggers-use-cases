# 🧩 Scenario  
### 📌 Every time an Account website is updated, update the website field on all its child contacts 

---

## 🛠️ Solution  
### ⚡ AccountTrigger   

```apex
trigger AccountTrigger on Account (before update, after update) {
    if(Trigger.isUpdate && Trigger.isAfter){
        AccountTriggerHandler.handleAfterUpdate(Trigger.NEW, Trigger.oldMap);
    }

}
```

### 🧠 AccountTriggerHandler Class

```apex
public class AccountTriggerHandler {
    public static void handleAfterUpdate(List<Account> accRecord, Map<Id, Account> oldAccMap){
        Map<Id, String> accToWebsite = new Map<Id, String>();
        List<Id> addIdToChild = new List<Id>();
        
        for(Account acc : accRecord){
            if(oldAccMap.get(acc.Id).Website != acc.Website){
                accToWebsite.put(acc.Id, acc.Website);
            }
        }
        
        if (accToWebsite.keySet().size() > 0){
            List<Contact> addConToUpdate = new List<Contact>();
            List<Contact> conRec = [SELECT Id, FirstName, Website__c, Contact.AccountId FROM Contact WHERE AccountId IN : accToWebsite.keySet()];
            for(Contact con : conRec){
                con.Website__c = accToWebsite.get(con.AccountId);
                addConToUpdate.add(con);
            }
            
            if(addConToUpdate.size() > 0){
                update addConToUpdate;
                System.debug('Contact Website updated!');
            }
        }
        
    }

}
```

## 📄 Trigger   
### ⚡ AccountTrigger 
<img width="500" height="415" alt="4" src="https://github.com/user-attachments/assets/785576ef-2acd-4e93-925d-5ad178e13e01" />


### 🧠 AccountTriggerHandler Class
<img width="500" height="983" alt="5" src="https://github.com/user-attachments/assets/5b172ca2-7e48-4f31-9341-2a762ae46e93" />


## 🐞 Debug Logs  
<img width="500" height="245" alt="3" src="https://github.com/user-attachments/assets/f176bb7c-871e-41ea-93bc-125f98c14bbb" />


## ✅ Hands On Practice
https://github.com/user-attachments/assets/6fcbae00-6f57-434d-99c0-28715e969212





## 🎉 Happy Learning 🎉
