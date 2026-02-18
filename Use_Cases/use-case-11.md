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
<img width="500" height="445" alt="3" src="https://github.com/user-attachments/assets/510abcc9-973b-4561-b4a0-dd86b4f03a25" />

### 🧠 AccountTriggerHandler Class
<img width="500" height="884" alt="4" src="https://github.com/user-attachments/assets/3775824b-52be-4504-9eca-83865cda267c" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/e52ea154-5623-48fa-91a1-7f113cfdfe4e






## 🎉 Happy Learning 🎉
