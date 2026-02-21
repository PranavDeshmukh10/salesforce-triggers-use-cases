# 🧩 Scenario  
### 📌 As soon as Opportunity is Closed Lost, remove all Opportunity Team Members from the Opportunity 

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
<img width="500" height="465" alt="1" src="https://github.com/user-attachments/assets/a896e022-ec66-40f1-af46-0272f5fb35ff" />

### 🧠 AccountTriggerHandler Class
<img width="500" height="1007" alt="2" src="https://github.com/user-attachments/assets/1ff4a236-e620-46a8-a5f9-c91308d9c173" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/00d6b264-7c93-4677-9ce7-eaa116148ade






## 🎉 Happy Learning 🎉
