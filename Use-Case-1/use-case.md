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
### Here you can see the trigger written on the Task object:  
<img width="1914" height="776" alt="2" src="https://github.com/user-attachments/assets/fbfa4aae-f082-457f-9fc1-185ff6272caf" />  

## 📝 Creating a Task Record  
### A new Task record is being created:  
<img width="700" height="940" alt="1" src="https://github.com/user-attachments/assets/4dbea713-00e9-469a-94a2-b964a6f3d781" />  

## 🐞 Debug Logs  
## The trigger execution can be verified from the debug logs:  
<img width="1915" height="376" alt="3" src="https://github.com/user-attachments/assets/48da741a-e51a-47d9-817c-ab8e131b78c3" />  

## ✅ Final Result  
### The Priority field is automatically set to High after record creation:  
<img width="1916" height="876" alt="4" src="https://github.com/user-attachments/assets/311864e5-c364-43f7-841f-7fb457a81358" />

## 🎯 Key Takeaways

🔹 Before Insert Trigger allows modifying field values before saving  
🔹 No DML statement is required when updating records in before triggers  
🔹 Using Trigger.new ensures bulk-safe execution  
