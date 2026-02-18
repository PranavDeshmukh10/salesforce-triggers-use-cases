# 🧩 Scenario  
### 📌 Do not allow Lead deletion if it is Working Contacted  

---

## 🛠️ Solution  
### ⚡ LeadTrigger   

```apex
trigger LeadTrigger on Lead (before update, after insert, before delete) {
    
    if(Trigger.isBefore && Trigger.isDelete){
        LeadTriggerHandler.handleActivitiesBeforeDelete(Trigger.OLD);
    }
}

```

### 🧠 LeadTriggerHandler  Class

```apex
public class LeadTriggerHandler {
    public static void handleActivitiesBeforeDelete(List<Lead> newRecords){
        
        for(Lead leadRec : newRecords){
            system.debug(leadRec.Status);
            if (leadRec.Status == 'Working - Contacted'){
                leadRec.addError('As Status is Working-Contacted, you cannot delete this record!');
                System.debug('Deletion Prevented Successfully!');
            }
        }
        
    }
    
}
```

## 📄 Trigger   
### ⚡ LeadTrigger 
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 10/4.png" />

### 🧠 LeadTriggerHandler  Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/5.png" />

## 🐞 Debug Logs  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/3.png" />

## ✅ Hands On Practice





## 🎉 Happy Learning 🎉