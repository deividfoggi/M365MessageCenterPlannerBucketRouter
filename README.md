# M365 Message Center Planner Bucket Router
This automation will route message center synced tasks in buckets with the same name (case-sensitive) as the name of the bucket. You need to create buckets with the same name of each product category. The automation will also input categories and tags from message center item into the planner task as tags. Finally, if you want to, you can input e-mails for each user responsible for a given product then the user will be assigned to the task in planner.

**Pre-requisites**

 - Configure the message center planner sync accordintly to this documentation. You can whatever name you want for the "incoming" planner:
https://docs.microsoft.com/en-us/office365/planner/track-message-center-tasks-planner#:~:text=You%20can%20only%20sync%20your%20message%20center%20with,a%20task%20in%20the%20bucket%20you%20select%20here.

- Create one bucket per product listed in the following path: https://admin.microsoft.com > Health > Message center > Planner syncing > click Edit under Services list, make sure _All updates_ are selected and also all the categories and products or services as checked as well. You must have one bucket per products or categories that have been checked in the list. **Do not create buckets for the categories because those items are included in plan task as tags.**

- Import the .zip file in flow: https://flow.microsoft.com/en-us/blog/import-export-bap-packages/


**Setup**

1. Get the plan Id by acessing the plan and getting its id in the browser address bar:

  ![image](https://user-images.githubusercontent.com/39340082/128246992-b6e6b6b9-e757-4057-9140-316010c7735d.png)
 
2. Get the "incoming" bucket id using the following steps:

  A. Open https://developer.microsoft.com/en-us/graph/graph-explorer and sign in to Graph explorer with an account with access to the plan using the blue button in the left-hand side
  B. In the field left to the "Run query button", paste the following address with the plan id copied in the step 1:
  
    https://graph.microsoft.com/v1.0/planner/plans/ydWJSZ-twk-ax-_8TDFGPWQAEoR0/buckets

  C. Run the query and find the "incoming" bucket in the response preview list. Copy the id:
 
   ![image](https://user-images.githubusercontent.com/39340082/128247558-00f61121-1f2c-42e7-b5d6-a2059cd16402.png)
    
  D. Open the flow you've imported in the pre-requisites and locate the trigger, and configure it by selecting the group and the planner you've configured in the message center sync setup
  
  ![image](https://user-images.githubusercontent.com/39340082/128248011-df12a993-f481-4383-9c9b-c548ac3f9c19.png)

  E. Use the variable labeled as "List of contacts" to input all contacts in your environment that should be assigned to a task accordingly to the product therefore assiging the tasks of a given product to the reponsible contact/team. You must respect the following format of each item in the array:
  
  [
  "Product 1:user1@contoso.com;user2@contoso.com;user3@contoso.com",
  "Product 2: user4@contoso.com;user5@contoso.com"
  ]
 
 All products to date are included in the array. You just have to input the users semi-somma separated making sure no spaces in each line.
 
  F. Go the the condition labeled "If the bucket is the Incoming bucket" and paste the bucket id you copied in step c:
  
  ![image](https://user-images.githubusercontent.com/39340082/128249031-1b794782-228e-4436-ad1b-cc232a5049f1.png)

 **Test**
 
 In order to confirm that everything is working as expected, you can deleted all tasks in the planner and configure the planner sync once again selecting the same plan you already configured in the flow. For each task, you flow run you be triggered. As a result, each task should be placed in the bucket of the respective product, including all categories and tags as task tags and also assigning the task for the users you've configured in step E.
 
