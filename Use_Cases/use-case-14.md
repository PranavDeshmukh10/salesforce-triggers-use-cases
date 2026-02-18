# 🧩 Scenario  
### 📌 Do not allow contact creation if a contact already exists with the same last name, email & phone. 

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

### 🧠 ContactTriggerHandler Class

```apex
public class ContactTriggerHandler {
    
    public static void handleActivitiesBeforeInsert(List<Contact> newRecords){
        List<Contact> conRec = [SELECt Id, LastName, Email, Phone FROM Contact LIMIT 50000];        
        for(Contact con : newRecords){
            for(Contact existingRec : conRec){
                if(con.LastName == existingRec.LastName && con.Email == existingRec.Email && con.Phone == existingRec.Phone){
                    con.addError('You cannot create a contact as the record with Last Name, Email, Phone already exist!');
                }
            }
            
        }
    }

}

```

## 📄 Trigger   
### ⚡ ContactTrigger  
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 10/4.png" />

### 🧠 ContactTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/5.png" />

## 🐞 Debug Logs  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/3.png" />

## ✅ Hands On Practice





## 🎉 Happy Learning 🎉