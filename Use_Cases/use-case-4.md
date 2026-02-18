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
<img width="500" height="813" alt="3" src="https://github.com/user-attachments/assets/97f95b8a-31ca-45ac-b5e2-e2e8458b1dd6" />

## 🐞 Debug Logs  
<img width="500" height="453" alt="4" src="https://github.com/user-attachments/assets/37b8dd71-cf4c-4d17-92e0-5e71fb585aab" />

## ✅ Hands On Practice  



## 🎉 Happy Learning 🎉








