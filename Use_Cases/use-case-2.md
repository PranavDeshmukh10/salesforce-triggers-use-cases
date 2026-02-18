# 🧩 Scenario  
### 📌 Whenever a **Lead** record is updated, set the **Lead Status** to **Working-Contacted**

In this use case, whenever a **Lead** record is updated, its **Lead Status** field should automatically be set to **Working-Contacted**.  
Since we are modifying a field of the **Lead** object before it is saved, we use a **Before Update Trigger** on **Lead**.

---

## 🛠️ Solution

```apex
trigger LeadTrigger on Lead (before update) {
	
    if(Trigger.isUpdate && Trigger.isBefore){
        for(Lead leadRecord : Trigger.NEW){
            System.debug('Lead Record Found.');
            leadRecord.Status = 'Working - Contacted';
            System.debug('Lead Status Updated.');
        }
    }
}
```

## 📄 Trigger 
<img width="500" height="491" alt="4" src="https://github.com/user-attachments/assets/2fa70799-ad76-458a-829c-2ded2f046e8a" />

## 🐞 Debug Logs  
<img width="500" height="273" alt="3" src="https://github.com/user-attachments/assets/b5401f23-b2bb-48dd-ab56-0f85783cf1cf" />

## ✅ Hands On Practice  
https://github.com/user-attachments/assets/2d42115f-51af-4b73-b244-360c86b603b4



## 🎉 Happy Learning 🎉
