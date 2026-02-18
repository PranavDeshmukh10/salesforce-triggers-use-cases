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
<img width="500" height="486" alt="3" src="https://github.com/user-attachments/assets/3800720c-6b0c-4099-a7e9-630dbbd90d85" />

### 🧠 LeadTriggerHandler  Class
<img width="500" height="580" alt="4" src="https://github.com/user-attachments/assets/996ef5b5-f773-425d-87a4-e4993d48b304" />

## 🐞 Debug Logs  
<img width="500" height="248" alt="2" src="https://github.com/user-attachments/assets/4d754479-8f86-4aa7-891b-c1b587c23e81" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/a4e4ee73-5915-4920-a3d5-55e66adea1bb




## 🎉 Happy Learning 🎉
