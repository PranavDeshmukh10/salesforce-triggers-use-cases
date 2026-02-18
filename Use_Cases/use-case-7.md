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
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 7/3.png" />

### 🧠 OpportunityTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 7/4.png" />

## ✅ Hands On Practice



## 🎉 Happy Learning 🎉