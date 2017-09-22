---
title: salesforce_code_001_trigger
categories: salesforce
tags: salesforce
photos:
- /images/salesforce.jpeg
---



# trigger

```apex
trigger HelloWorldTrigger on Account (before insert) {
     for(Account a : Trigger.New) {
          a.Description = 'New description';
     }  
}  
```