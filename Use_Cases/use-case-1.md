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

## 📄 Trigger    
<img width="500" height="463" alt="2" src="https://github.com/user-attachments/assets/fa2e058c-8500-4540-9239-a303f0ab5de5" />

## 🐞 Debug Logs  
<img width="500" height="320" alt="3" src="https://github.com/user-attachments/assets/c8c4539e-b439-42b7-8066-459c6f652ead" />

## ✅ Hands On Practice   
https://github.com/user-attachments/assets/d7dda69b-047c-4da7-bd59-93ba7136eb26



## 🎉 Happy Learning 🎉 
