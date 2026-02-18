# 🧩 Scenario  
### 📌 When a **Lead** is updated and **Industry = Healthcare**, do below things:

🔹 Set **Lead Source** to **Purchased List**  
🔹 Set **SIC Code** to **1100**  
🔹 Set **Primary** to **Yes**  
🔹 Set **Status** to **Working – Contacted**

This ensures that all **Healthcare leads** are categorized and standardized properly without any manual effort.

---

## 🛠️ Solution

```apex
trigger LeadTrigger on Lead (before update) {
    
    if (Trigger.isUpdate && Trigger.isBefore) {
        
        for (Lead leadRecord : Trigger.new) {
            
            leadRecord.Status = 'Working - Contacted';
            System.debug('Lead Status Updated.');
            
            if (leadRecord.Industry == 'Healthcare') {
                leadRecord.LeadSource = 'Purchased List';
                leadRecord.SICCode__c = '1100';
                leadRecord.Primary__c = 'Yes';
                System.debug('Lead Record Updated Successfully.');
            }
        }
    }
}
```

## 📄 Trigger   
<img width="500" height="655" alt="3" src="https://github.com/user-attachments/assets/ac010ca3-bd4b-4662-bf64-6531f6d7bce8" />

## 🐞 Debug Logs  
<img width="500" height="258" alt="4" src="https://github.com/user-attachments/assets/c624f086-9edf-4637-9d4d-5f0fd95b7ffc" />

## ✅ Hands On Practice  
https://github.com/user-attachments/assets/d17b5220-ab2e-4dda-8082-683e8d34a8ef




## 🎉 Happy Learning 🎉








