# 🧩 Scenario  
### 📌 Create Contact records based on Create N Contacts field on the Account record

---

## 🛠️ Solution  
### ⚡ AccountTrigger   

```apex
trigger AccountTrigger on Account (before update, after update, after insert) {
    
    if(Trigger.isInsert && Trigger.isAfter){
        AccountTriggerHandler.handleAfterInsert(Trigger.NEW);
    }

}
```

### 🧠 AccountTriggerHandler Class

```apex
public class AccountTriggerHandler {
    
    public static void handleAfterInsert(List<Account> accRecords) {
        List<Contact> conList = new List<Contact>();
        
        for (Account acc : accRecords){
            if(acc.Create_N_Contacts__c != null){
                for(Integer i=1; i<=acc.Create_N_Contacts__c; i++){
                    Contact con = new Contact();
                    con.FirstName = acc.Name;
                    con.LastName = 'User ' + i;
                    con.AccountId = acc.Id;
                    conList.add(con);
                }
                
            }
        }
        
        if(!conList.isEmpty()){
        	insert conList;
        }
    }

}
```

## 📄 Trigger   
### ⚡ AccountTrigger 
<img width="500" height="813" alt="4" src="/Salesforce Triggers/Day 10/4.png" />

### 🧠 AccountTriggerHandler Class
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/5.png" />

## 🐞 Debug Logs  
<img width="500" height="734" alt="5" src="/Salesforce Triggers/Day 10/3.png" />

## ✅ Hands On Practice





## 🎉 Happy Learning 🎉