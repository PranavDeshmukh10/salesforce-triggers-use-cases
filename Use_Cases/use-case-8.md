# 🧩 Scenario  
### 📌 If a Contact is created without a parent Account, do not allow user to create the contact record 

---

## 🛠️ Solution  
### ⚡ ContactTrigger

```apex
trigger ContactTrigger on Contact (before insert) {
    
    if(Trigger.isInsert && Trigger.isBefore){
        ContactTriggerHandler.handleActivitiesBeforeInsert(Trigger.NEW);
    }
    
}
```

### 🧠 ContactTriggerHandler  Class

```apex
public class ContactTriggerHandler {
    
    public static void handleActivitiesBeforeInsert(List<Contact> newRecords){
        for(Contact newCon : newRecords){
            if(newCon.AccountId == null){
                //throw error
                newCon.addError('Parent Account is mandatory for Contact!');
            }
        }
    }

}
```

## 📄 Trigger   
### ⚡ ContactTrigger 
<img width="500" height="335" alt="3" src="https://github.com/user-attachments/assets/9dafaa68-7cf9-4fc3-bfee-067261027984" />

### 🧠 ContactTriggerHandler Class
<img width="500" height="477" alt="4" src="https://github.com/user-attachments/assets/ef23fade-84d2-4f02-88ba-a5bf2c5d3ae4" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/92846dba-9a2a-4689-be9b-60c023320e32





## 🎉 Happy Learning 🎉
