# 🧩 Scenario 
### 📌 Whenever an **Opportunity** is marked as **Closed-Won**, create a **Task** for **Opportunity Owner** to **split the revenue among the team** with **High Priority**  

---
## 🛠️ Solution  

### 🏗️ Architecture – Trigger Handler Pattern

In this use case, we use the **Trigger Handler Pattern**, which is a Salesforce best practice because it:

- Separates **business logic** from triggers  
- Makes code **reusable & testable**  
- Keeps triggers **clean and simple**

---

### ⚡ Opportunity Trigger

```apex
trigger OpportunityTrigger on Opportunity (after update) {
    
    // Delegate execution to the handler class
    OpportunityTriggerHandler.HandleActivitiesAfterUpdate(Trigger.new);
}
```

### 🧠 OpportunityTriggerHandler Class

```apex
public class OpportunityTriggerHandler {
	
    public static void HandleActivitiesAfterInsert(){
        
    }
    
    public static void HandleActivitiesAfterUpdate(List <Opportunity> newRecords){
        List<Task> taskList = new List<Task>();
        if(Trigger.isUpdate && Trigger.isAfter){
        	for(Opportunity oppRecord : newRecords){
            	if(oppRecord.StageName == 'Closed Won'){
                    //create a Task Record.
                    Task taskRecord = new Task();
                    taskRecord.Priority = 'High';
                    taskRecord.OwnerId = oppRecord.OwnerId;
                    taskRecord.Description = 'Please split the revenue amongst the team members and enjoy.';
                    taskRecord.Subject = 'Revenue!!!';
                    taskRecord.Status = 'Not Started';
                    taskRecord.WhatId = oppRecord.Id;
                    taskList.add(taskRecord);
                
                	System.debug('Task Record created successfully.');
            	}
        	}
            
            if(!taskList.isEmpty()){
                System.debug('Task created successfully!');
                insert taskList;
            }
    	}
        
    }
}
```

## 📄 Trigger on Opportunity Object   
### ⚡ Opportunity Trigger
<img width="500" height="316" alt="5" src="https://github.com/user-attachments/assets/a2d130f0-75d9-4545-a248-3a29a5d19a5e" />

### 🧠 OpportunityTriggerHandler Class
<img width="500" height="1032" alt="6" src="https://github.com/user-attachments/assets/587e6aaa-37d3-4af4-b520-1f9e8c663a7f" />

## 📝 Updating a Opportunity Record  
### Before Record update
<img width="500" height="954" alt="1" src="https://github.com/user-attachments/assets/76a657a2-abac-4a8c-b831-c23fc975eeaf" />

### After Record update
<img width="500" height="946" alt="2" src="https://github.com/user-attachments/assets/020ac278-a4a8-4fd0-8f38-7f0b15833624" />

## ✅ Final Result  
### Task is Created
<img width="500" height="779" alt="3" src="https://github.com/user-attachments/assets/c6d73e55-cf95-4675-a0a8-8960328ac940" />
<img width="500" height="642" alt="4" src="https://github.com/user-attachments/assets/7f111d98-6563-491b-8cec-e7da0f8fcb3b" />


## 🔍 What’s Happening Here?  

| Step                | Description                                          |
| ------------------- | ---------------------------------------------------- |
| 🟢 Trigger Fires    | Runs when an **Opportunity** is updated              |
| 🎯 Closed-Won Check | Verifies if `StageName = 'Closed Won'`               |
| 📝 Task Creation    | Creates a **High-Priority Task**                     |
| 👤 Owner Assignment | Task is assigned to the **Opportunity Owner**        |
| 🔗 Linking          | Task is linked to the **Opportunity** using `WhatId` |
| 💾 Insert           | All tasks are inserted in one bulk operation         |

## 🎉 Happy Learning 🎉

