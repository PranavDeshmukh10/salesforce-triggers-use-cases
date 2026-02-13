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
### Here you can see the trigger written on the Lead object:  
 <img width="500" height="713" alt="4" src="https://github.com/user-attachments/assets/f22817bd-1a76-4133-9008-44837940f1df" />

## 📝 Updating a Lead Record  
### A Lead record is being updated:  
<img width="500" height="1038" alt="1" src="https://github.com/user-attachments/assets/f1aa1457-e67b-4b9a-a697-ff42dca14318" />

## 🐞 Debug Logs  
## The trigger execution can be verified from the debug logs:  
<img width="500" height="386" alt="3" src="https://github.com/user-attachments/assets/dc62871c-de89-40c6-a7ed-60d1dd631c05" />


## ✅ Final Result  
### The Lead Status field is automatically set to Working-Contacted after record updation:  
<img width="500" height="1040" alt="2" src="https://github.com/user-attachments/assets/73603f5a-f358-441d-91d4-2988c1f0f23b" />


## 🔍 What’s Happening Here?  
| Step             | Description                                   |
| ---------------- | --------------------------------------------- |
| 🟢 Trigger Fires | Runs when a **Lead** record is updated        |
| 🔄 Loop          | Iterates through all records in `Trigger.new` |
| ✏️ Field Update  | Sets `Status` to **Working – Contacted**      |
| 🐞 Debug Logs    | Helps confirm execution                       |

## 🎯 Key Notes
✔️ Uses Before Update Trigger → No DML needed  
✔️ Works in bulk updates  
✔️ Ensures data consistency  
✔️ Automatically standardizes Lead status  

## 🧠 Real-World Use Case  
This is useful in sales teams where **any activity or edit on a Lead** means the sales rep has contacted the prospect — so Salesforce updates the status automatically.
