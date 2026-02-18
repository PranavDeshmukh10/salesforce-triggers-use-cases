# 🧩 Scenario  
### 📌 As soon as an Opportunity is deleted, create a Task for Opportunity’s Account Owner to investigate why the opportunity was deleted and submit the information. 

---

## 🛠️ Solution  
### ⚡ OpportunityTrigger    

```apex
trigger OpportunityTrigger on Opportunity (after update, before update, after delete) {
    
    if(Trigger.isAfter && Trigger.isDelete){
        OpportunityTriggerHandler.HandleActivitiesAfterDelete(Trigger.OLD); 
    }
}

```

### 🧠 OpportunityTriggerHandler Class

```apex
public class OpportunityTriggerHandler {
    
    public static void HandleActivitiesAfterDelete(List <Opportunity> oldRecords){
        
        Set<Id> accountIds = new Set<Id>();
        Map<Id,Id> oppVsAccMap = new Map<Id,Id>();
        Map<Id,Id> accVsOwnerIdMap = new Map<Id,Id>();
        
        for(Opportunity oppRec : oldRecords){
            accountIds.add(oppRec.AccountId);
            oppVsAccMap.put(oppRec.Id, oppRec.AccountId);
        }
        
        List<Account> accRec = [SELECT Id, OwnerId FROM Account WHERE Id IN : accountIds];
        for(Account acc : accRec){
            accVsOwnerIdMap.put(acc.Id, acc.OwnerId);
        }
        
        List<Task> taskList = new List<Task>();        
        for(Opportunity opp : oldRecords){
            Task taskRecord = new Task();
            taskRecord.Priority = 'High';
            taskRecord.OwnerId = accVsOwnerIdMap.get(oppVsAccMap.get(opp.Id));
            taskRecord.Description = 'Please investigate why the opportunity is deleted and submit the information as soon as possible.';
            taskRecord.Subject = 'Opportunity Record Deleted!';
            taskRecord.Status = 'Not Started';
            taskList.add(taskRecord);
            System.debug('Task Record created successfully.');
        }
        
        if(!taskList.isEmpty()){
            System.debug('Task created successfully!');
            insert taskList;
        }
    }
}

```

## 📄 Trigger   
### ⚡ OpportunityTrigger  
<img width="500" height="451" alt="1" src="https://github.com/user-attachments/assets/c860e8fe-4755-4d1f-8f29-bf4bdd5af0b1" />

### 🧠 OpportunityTriggerHandler Class
<img width="500" height="1035" alt="2" src="https://github.com/user-attachments/assets/be3b3b97-449f-47a8-9314-c9cd6e572a7f" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/10a391ff-1dc3-4932-b282-bbab4a3eb741






## 🎉 Happy Learning 🎉
