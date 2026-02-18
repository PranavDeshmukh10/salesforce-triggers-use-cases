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

## 📄 Trigger on Case Object   
<img width="500" height="727" alt="4" src="/Use Cases/Use_Case_3/Hands_On_Practice/4.png" />


## 📝 Creating a Case Record  
<img width="500" height="977" alt="1" src="https://github.com/user-attachments/assets/a3d893ab-d2bc-484a-8b5d-6b624048174c" />


## 🐞 Debug Logs  
<img width="500" height="318" alt="3" src="https://github.com/user-attachments/assets/9fa03ac3-51d9-4bb5-a63b-30d1adb486e1" />

## ✅ Final Result  
<img width="500" height="1043" alt="2" src="https://github.com/user-attachments/assets/793d882e-4684-46a3-b43e-7f6a550b5e45" />
<video width="800" controls>
  <source src="https://github.com/PranavDeshmukh10/salesforce-triggers-use-cases/raw/master/Use%20Cases/Use_Case_3/Hands_On_Practice/hands-on.mp4" type="video/mp4">
</video>


## 🔍 What’s Happening Here?  

| Step               | Description                            |
| ------------------ | -------------------------------------- |
| 🟢 Trigger Fires   | Runs when a **Case** record is created |
| 🔄 Loop            | Iterates through all new Case records  |
| 📞 Condition Check | Checks if `Origin == 'Phone'`          |
| 🔴 High Priority   | If true → sets **Priority = High**     |
| 🟡 Low Priority    | Otherwise → sets **Priority = Low**    |
| 🐞 Debug Logs      | Confirms which condition ran           |
| 💾 Save            | Record is saved with updated Priority  |

## 🎉 Happy Learning 🎉






