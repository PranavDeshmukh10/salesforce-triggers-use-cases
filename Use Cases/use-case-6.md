# 🧩 Scenario  
### 📌 As soon as a Lead record is created, create a Task for the Lead Owner to follow up with the customer. 

---

## 🛠️ Solution  
### ⚡ Lead Trigger

```apex
trigger LeadTrigger on Lead (before update, after insert) {
    
    if(Trigger.isAfter && Trigger.isInsert){
        //so the activities here
        LeadTriggerHandler.handleActivitiesAfterInsert(Trigger.NEW);
    }
}
```

### 🧠 LeadTriggerHandler Class

```apex
public class LeadTriggerHandler {
	
    public static void handleActivitiesAfterInsert(List<Lead> newRecords){
        List<Task> taskRecordToInsert = new List<Task>();
    	for(Lead leadRec : newRecords){
         	Task taskRecord = new Task();
            taskRecord.OwnerId = leadRec.OwnerId;
            taskRecord.Description = 'Please followup with the customer';
            taskRecord.Priority = 'High';
            taskRecord.Subject = 'Followup!';
            taskRecord.WhoId = leadRec.Id;
            taskRecordToInsert.add(taskRecord);
         }
            
         if(!taskRecordToInsert.isEmpty()){
            insert taskRecordToInsert;
             System.debug('This is from Lead Trigger Handler!!!');
         }
        	
    	
    }
}
```

## 📄 Trigger on Opportunity Object   
### ⚡ Lead Trigger
<img width="500" height="813" alt="4" src="https://github.com/user-attachments/assets/66700519-6b62-45d9-bb9d-fb142f91ff81" />

### 🧠 LeadTriggerHandler Class
<img width="500" height="734" alt="5" src="https://github.com/user-attachments/assets/e204f29f-fe1f-4404-945f-21d330dd6af8" />

## 📝 Creating a Lead Record  
<img width="500" height="946" alt="1" src="https://github.com/user-attachments/assets/0dfc1769-6010-42a3-92f0-db10b0015951" />

## ✅ Final Result  
### Task is Created
<img width="500" height="715" alt="2" src="https://github.com/user-attachments/assets/1bd1ae12-4346-4d51-9b9b-081fc00407a0" />
<img width="500" height="592" alt="3" src="https://github.com/user-attachments/assets/fe27a39d-a2a8-474b-b2b2-3e4e98acd44f" />


## 🔍 What’s Happening Here?  

| Step             | Description                                  |
| ---------------- | -------------------------------------------- |
| 🟢 Trigger Fires | Runs when a **Lead** is created              |
| 🔄 Handler Call  | Trigger delegates logic to handler class     |
| 👤 Owner Lookup  | Finds the Lead Owner                         |
| 📝 Task Creation | Creates a **High-Priority Follow-Up Task**   |
| 🔗 WhoId         | Links Task to the **Lead**                   |
| 💾 Insert        | All tasks are inserted in one bulk operation |

## 🎯 Business Value  
📞 Every Lead gets an automatic follow-up  
⚡ No sales opportunity is missed  
👥 Tasks are correctly assigned to Lead Owners  
📊 Improves conversion rates  

## 🧠 Real-World Scenario  
Sales teams often lose leads because follow-ups are forgotten.  
This automation ensures **every Lead gets immediate attention** — improving trust and revenue.








