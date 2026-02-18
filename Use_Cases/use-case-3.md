# 🧩 Scenario  
### 📌 When a **Case** is created, set **Priority** based on **Case Origin**
- If **Case Origin = Phone** → Priority = **High** 📞  
- Else → Priority = **Low** 📩

This ensures that **phone calls get immediate attention** compared to other case sources.
Since we are modifying a field of the **Case** object before it is saved, we use a **Before Insert Trigger** on **Case**.  

---

## 🛠️ Solution

```apex
trigger CaseTrigger on Case (before insert) {
	
    if(Trigger.isInsert && Trigger.isBefore){
        for(Case caseRecord : Trigger.NEW){
            if(caseRecord.Origin == 'Phone'){
                caseRecord.Priority = 'High';
                System.debug('Priority has been set as High.');
            }
            else {
                caseRecord.Priority = 'Low';
                System.debug('Priority has been set as Low.');
            }
        }
    }
}
```

## 📄 Trigger   
<img width="500" height="651" alt="4" src="https://github.com/user-attachments/assets/96b2a5f3-df33-499b-b222-14c97e8aac16" />

## 🐞 Debug Logs  
<img width="500" height="242" alt="3" src="https://github.com/user-attachments/assets/9b77aa94-d1db-4fbe-85e1-9d1c4a221131" />

## ✅ Hands On Practice 
https://github.com/user-attachments/assets/8e10b0d1-1792-4254-919b-61bdd55677e0



## 🎉 Happy Learning 🎉






