# 🧩 Scenario  
### 📌 If Opportunity Stage is Modified, update Opportunity Amount based on Probability * Excepted Revenue 

---

## 🛠️ Solution  
### ⚡ OpportunityTrigger 

```apex
trigger OpportunityTrigger on Opportunity (after update, before update) {
    
    if(Trigger.isBefore && Trigger.isUpdate){
        
        OpportunityTriggerHandler.HandleActivitiesBeforeUpdate(Trigger.NEW, Trigger.oldMap);        
        //Trigger.NEW: List<sObject> --> List<Opportunity> --> contains new version
        //Trigger.OLD: List<sObject> --> List<Opportunity> --> contains old version
        //Trigger.newMap: Map<Id,sObject> --> Map<Id, Opportunity> --> new values in key value pair format
        //Trigger.oldMap: Map<Id,sObject> --> Map<Id, Opportunity> --> old values in key value pair format
    }
}
```

### 🧠 OpportunityTriggerHandler Class

```apex
public class OpportunityTriggerHandler {
public static void HandleActivitiesBeforeUpdate(List<Opportunity> oppNewRecords, Map<Id,Opportunity> oldMap){
      
        for(Opportunity newOpp : oppNewRecords){
            if(oldMap.get(newOpp.Id).StageName != newOpp.StageName){
                system.debug('Stage has been modified!!!');
                newOpp.Amount = newOpp.Probability * newOpp.ExpectedRevenue;
            }
            
        }
    }
}
```

## 📄 Trigger   
### ⚡ OpportunityTrigger 
<img width="500" height="546" alt="3" src="https://github.com/user-attachments/assets/5446e2a8-5f13-4fd5-a77c-c325d1f342f1" />

### 🧠 OpportunityTriggerHandler Class
<img width="500" height="541" alt="4" src="https://github.com/user-attachments/assets/acfe80e6-be0f-4be5-a7a9-40b67daafd54" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/ea2d54b2-9785-406b-a1fd-a3f76e571ec0




## 🎉 Happy Learning 🎉
