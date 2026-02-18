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

## 📄 Trigger on Lead Object  
 <img width="500" height="713" alt="4" src="/Use Cases/Use_Case_2/Hands_On_Practice/4.png" />

## 📝 Updating a Lead Record  
<img width="500" height="1038" alt="1" src="/Use Cases/Use_Case_2/Hands_On_Practice/1.png" />

## 🐞 Debug Logs  
<img width="500" height="386" alt="3" src="/Use Cases/Use_Case_2/Hands_On_Practice/3.png" />


## ✅ Final Result  
<img width="500" height="1040" alt="2" src="/Use Cases/Use_Case_2/Hands_On_Practice/2.png" />


## 🔍 What’s Happening Here?  
| Step             | Description                                   |
| ---------------- | --------------------------------------------- |
| 🟢 Trigger Fires | Runs when a **Lead** record is updated        |
| 🔄 Loop          | Iterates through all records in `Trigger.new` |
| ✏️ Field Update  | Sets `Status` to **Working – Contacted**      |
| 🐞 Debug Logs    | Helps confirm execution                       |

## 🎉 Happy Learning 🎉
