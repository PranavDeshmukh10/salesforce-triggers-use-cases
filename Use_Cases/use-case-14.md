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
<img width="500" height="358" alt="1" src="https://github.com/user-attachments/assets/d5bd52f0-c0dd-4913-b880-77508fbea303" />

### 🧠 ContactTriggerHandler Class
<img width="500" height="811" alt="2" src="https://github.com/user-attachments/assets/c2fc426b-80a6-4a2e-8495-302d4a3d7b9e" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/be09d1de-ac18-4cb1-bbb0-2a256dc88ac9





## 🎉 Happy Learning 🎉
