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
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 10/4.png" />

### 🧠 OpportunityTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/5.png" />

## 🐞 Debug Logs  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/3.png" />

## ✅ Hands On Practice





## 🎉 Happy Learning 🎉