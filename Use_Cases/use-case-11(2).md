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
<img width="1066" height="535" alt="1" src="https://github.com/user-attachments/assets/ad517493-2a34-4d2b-be77-87d2e2393a7a" />


### 🧠 AccountTriggerHandler Class
<img width="1556" height="1012" alt="2" src="https://github.com/user-attachments/assets/a3870dac-1f7f-4a27-aecb-b71bf9e88aeb" />

## ✅ Hands On Practice
https://github.com/user-attachments/assets/077f012c-751a-4f1a-a5ca-8ebf82af991e



## 🎉 Happy Learning 🎉
