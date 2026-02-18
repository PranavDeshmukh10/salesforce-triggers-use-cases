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

## 📄 Trigger   
### ⚡ Lead Trigger
<img width="500" height="813" alt="4" src="https://github.com/user-attachments/assets/66700519-6b62-45d9-bb9d-fb142f91ff81" />

### 🧠 LeadTriggerHandler Class
<img width="500" height="734" alt="5" src="https://github.com/user-attachments/assets/e204f29f-fe1f-4404-945f-21d330dd6af8" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/a86e4ef2-b2bd-4fb4-8488-2aacf9455403




## 🎉 Happy Learning 🎉








