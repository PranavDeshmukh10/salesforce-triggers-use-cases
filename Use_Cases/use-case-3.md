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
<img width="500" height="727" alt="4" src="/Use Cases/Use_Case_3/Hands_On_Practice/4.png" />

## 🐞 Debug Logs  
<img width="500" height="318" alt="3" src="https://github.com/user-attachments/assets/9fa03ac3-51d9-4bb5-a63b-30d1adb486e1" />

## ✅ Hands On Practice 
https://github.com/user-attachments/assets/8e10b0d1-1792-4254-919b-61bdd55677e0



## 🎉 Happy Learning 🎉






