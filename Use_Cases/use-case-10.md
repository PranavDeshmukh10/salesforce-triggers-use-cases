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
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 10/4.png" />

### 🧠 AccountTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/5.png" />

## 🐞 Debug Logs  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/3.png" />

## ✅ Hands On Practice




## 🎉 Happy Learning 🎉