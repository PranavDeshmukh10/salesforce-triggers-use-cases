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

## 📄 Trigger on Contact Object   
### ⚡ ContactTrigger 
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 8/3.png" />

### 🧠 ContactTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 8/4.png" />

## ✅ Final Result  
### New Contact failed  
<img width="500" height="715" alt="2" src="/Salesforce Triggers/Day 8/1.png" />

### New contact created  
<img width="500" height="592" alt="3" src="/Salesforce Triggers/Day 8/2.png" />

## 🔍 What’s Happening Here?  

| Step             | Description                                |
| ---------------- | ------------------------------------------ |
| 🟢 Trigger Fires | Runs when a **Contact** is being created   |
| 🔄 Loop          | Iterates through all new Contact records   |
| 🔍 Validation    | Checks if `AccountId` is null              |
| ❌ Error         | Blocks save using `addError()`             |
| 🚫 Save Blocked  | User cannot create Contact without Account |


## 🎉 Happy Learning 🎉