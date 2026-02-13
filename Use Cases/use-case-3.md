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

## 📄 Trigger on Task Object  
### Here you can see the trigger written on the Task object:  
<img width="500" height="727" alt="4" src="https://github.com/user-attachments/assets/b171e66c-2d4d-43f6-8711-b08217b7dc6a" />


## 📝 Creating a Task Record  
### A new Task record is being created:  
<img width="500" height="977" alt="1" src="https://github.com/user-attachments/assets/a3d893ab-d2bc-484a-8b5d-6b624048174c" />


## 🐞 Debug Logs  
## The trigger execution can be verified from the debug logs:  
<img width="500" height="318" alt="3" src="https://github.com/user-attachments/assets/9fa03ac3-51d9-4bb5-a63b-30d1adb486e1" />

## ✅ Final Result  
### The Priority field is automatically set to High after record creation:  
<img width="500" height="1043" alt="2" src="https://github.com/user-attachments/assets/793d882e-4684-46a3-b43e-7f6a550b5e45" />


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

## 🎯 Key Benefits  
📞 Phone cases get higher urgency  
⚡ Automatic priority assignment  
📊 Better case management for support teams  
🚫 No manual updates required  

## 🧠 Real-World Scenario  
Customer support teams prioritize **phone calls** because they usually indicate **urgent issues**.  
This trigger ensures Salesforce handles that automatically.  






