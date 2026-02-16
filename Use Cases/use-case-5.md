# 🧩 Scenario 
### 📌 Whenever an **Opportunity** is marked as **Closed-Won**, create a **Task** for **Opportunity Owner** to **split the revenue among the team** with **High Priority**  

---
## 🛠️ Solution  

## 🏗️ Architecture – Trigger Handler Pattern

In this use case, we use the **Trigger Handler Pattern**, which is a Salesforce best practice because it:

- Separates **business logic** from triggers  
- Makes code **reusable & testable**  
- Keeps triggers **clean and simple**

---

## ⚡ Opportunity Trigger

```apex
trigger OpportunityTrigger on Opportunity (after update) {
    
    // Delegate execution to the handler class
    OpportunityTriggerHandler.HandleActivitiesAfterUpdate(Trigger.new);
}
```

## 🧠 OpportunityTriggerHandler Class

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
<img width="962" height="316" alt="5" src="https://github.com/user-attachments/assets/a2d130f0-75d9-4545-a248-3a29a5d19a5e" />

### 🧠 OpportunityTriggerHandler Class
<img width="1319" height="1032" alt="6" src="https://github.com/user-attachments/assets/587e6aaa-37d3-4af4-b520-1f9e8c663a7f" />

## 📝 Updating a Opportunity Record  


## 🐞 Debug Logs  


## ✅ Final Result  


## 🔍 What’s Happening Here?  

| Step                | Description                                          |
| ------------------- | ---------------------------------------------------- |
| 🟢 Trigger Fires    | Runs when an **Opportunity** is updated              |
| 🎯 Closed-Won Check | Verifies if `StageName = 'Closed Won'`               |
| 📝 Task Creation    | Creates a **High-Priority Task**                     |
| 👤 Owner Assignment | Task is assigned to the **Opportunity Owner**        |
| 🔗 Linking          | Task is linked to the **Opportunity** using `WhatId` |
| 💾 Insert           | All tasks are inserted in one bulk operation         |

## 🎯 Business Value  

💰 Revenue distribution never gets missed  
📞 Owners get automatic reminders  
⚡ Fully automated post-sales workflow  
📊 Better accountability and tracking  

## 🧠 Real-World Use Case  

After a deal is won, revenue must be shared across sales, marketing, and partners.  
This trigger ensures the O**pportunity Owner is always reminded**, improving financial accuracy and collaboration.

