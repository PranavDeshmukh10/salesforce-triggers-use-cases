# 🧩 Scenario  
### 📌 Whenever the Create N Contacts field is updated to new value, create contact as per the updated value  

Note: Salesforce should not create all the contacts again.  
For ex: 
Old value = 3  
New value = 5, 
Then salesforce should create only 2 contacts.

---

## 🛠️ Solution  
### ⚡ AccountTrigger   

```apex
trigger AccountTrigger on Account (before update, after update, after insert) {
    
    if(Trigger.isUpdate && Trigger.isAfter){
        AccountTriggerHandler.handleAfterUpdate(Trigger.NEW, Trigger.oldMap);
    }

}
```

### 🧠 AccountTriggerHandler Class

```apex
public class AccountTriggerHandler {
	public static void handleAfterUpdate(List<Account> accRecord, Map<Id, Account> oldAccMap){ 
	List<Contact> conList = new List<Contact>();

	for (Account acc : accRecord){
            if(oldAccMap.get(acc.Id).Create_N_Contacts__c != acc.Create_N_Contacts__c){
                
                Integer newValue = (Integer)acc.Create_N_Contacts__c - (Integer)(oldAccMap.get(acc.Id).Create_N_Contacts__c);
                for(Integer i=1; i<=newValue; i++){
                    Contact con = new Contact();
                    con.FirstName = acc.Name;
                    con.LastName = 'User ' + (oldAccMap.get(acc.Id).Create_N_Contacts__c + i);
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