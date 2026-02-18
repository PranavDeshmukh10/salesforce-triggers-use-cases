# 🧩 Scenario  
### 📌 Whenever a **Task** is created, set the **Priority** to **High**

In this use case, whenever a new **Task** record is inserted, its **Priority** field should automatically be set to **High**.  
Since we are modifying a field of the **Task** object before it is saved, we use a **Before Insert Trigger** on **Task**.

---

## 🛠️ Solution

```apex
trigger TaskTrigger on Task (before insert) {
    
    if (Trigger.isInsert && Trigger.isBefore) {
        for (Task taskRecord : Trigger.new) {
            System.debug('Found Task Record');
            taskRecord.Priority = 'High';
        }
    }
}
```

## 📄 Trigger on Task Object   
<img width="500" height="776" alt="2" src="/Use Cases/Use_Case_1/Hands_On_Practice/2.png />  

## 📝 Creating a Task Record  
<img width="500" height="940" alt="1" src="/Use Cases/Use_Case_1/Hands_On_Practice/1.png" />  

## 🐞 Debug Logs  
<img width="500" height="376" alt="3" src="/Use Cases/Use_Case_1/Hands_On_Practice/3.png />


## ✅ Final Result   
<img width="500" height="876" alt="4" src="/Use Cases/Use_Case_1/Hands_On_Practice/4.png" />

## 🔍 What’s Happening Here?

| Step | Description |
|------|-------------|
| 🟢 Trigger Fires | Runs when a **Task** record is created |
| 🔄 Loop | Iterates through all new Task records using `Trigger.new` |
| ✏️ Field Update | Sets `Priority` to **High** before saving |
| 🐞 Debug Log | Confirms trigger execution |
| 💾 Save | Record is saved with updated Priority |

## 🎉 Happy Learning 🎉 
