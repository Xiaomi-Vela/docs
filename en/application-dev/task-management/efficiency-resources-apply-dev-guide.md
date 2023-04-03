# Efficiency Resource Request Development

## When to Use

To further balance power consumption overhead of the system, privileged system applications can be suspended in the background as other applications. To ensure normal provisioning of important functions, efficiency resource APIs are provided for these applications so that they can execute special tasks and use specific system resources in the background. For example, if they want to receive common events when suspended, they can use the APIs to request the common event resources.

To upgrade your application as a privileged application, you must evaluate your service requirements and submit a request to the application center. The application center will determine whether to accept the request based on the conditions.

## Constraints
Only system applications can request efficiency resources.

## Available APIs

**Table 1** Main APIs for efficiency resources

| API                                     | Description        |
| ---------------------------------------- | ---------- |
| applyEfficiencyResources(request: [EfficiencyResourcesRequest](../reference/apis/js-apis-resourceschedule-backgroundTaskManager.md#efficiencyresourcesrequest)): boolean | Requests efficiency resources.   |
| resetAllEfficiencyResources():void       | Releases efficiency resources.|


## How to Develop

1. When a privileged application in the background needs to use special resources, request the target resources from the system.

2. When the task is complete, release the resources in time. You can choose whether to release some or all resources.

   ```js
   import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';
   
   // Request efficiency resources.
   let request = {
       resourceTypes: backgroundTaskManager.ResourceType.COMMON_EVENT |
           backgroundTaskManager.ResourceType.TIMER,
       isApply: true,
       timeOut: 0,
       reason: "apply",
       isPersist: true,
       isProcess: true,
   };
   
   let res;
   try {
       res = backgroundTaskManager.applyEfficiencyResources(request);
       console.info("the result of request is: " + res);
   } catch (error) {
       console.error(`Operation applyEfficiencyResources failed. code is ${error.code} message is ${error.message}`);
   }
   
   // Release some efficiency resources.
   request = {
       resourceTypes: backgroundTaskManager.ResourceType.COMMON_EVENT,
       isApply: false,
       timeOut: 0,
       reason: "reset",
       isPersist: true,
       isProcess: true,
   };
   try {
       res = backgroundTaskManager.applyEfficiencyResources(request);
       console.info("the result of request is: " + res);
   } catch (error) {
       console.error(`Operation applyEfficiencyResources failed. code is ${error.code} message is ${error.message}`);
   }
   
   // Release all efficiency resources.
   try {
       backgroundTaskManager.resetAllEfficiencyResources();
   } catch (error) {
       console.error(`Operation resetAllEfficiencyResources failed. code is ${error.code} message is ${error.message}`);
   }
   ```