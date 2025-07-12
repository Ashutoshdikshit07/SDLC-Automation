# Creating AWS CodeCommmit Repository which triggers Email Notification

1. Create a CodeCommit Repository.
   1. Repository created with the name **CodeCommitNotifications**

2. Create a SNS (SimpleNotificationService).
   1. Create a topic name - **CodeCommitNotify**
   2. In the topic,
      1. Go to **Subscriptions**.
      2. Create a Subscription with email id.
         <img width="1675" height="593" alt="Screenshot 2025-07-12 at 7 06 18 PM" src="https://github.com/user-attachments/assets/edce5398-8d13-4951-9b7f-078f29a7a79b" />
         Make sure you confirm the subscription from the email id provided.
3. Here subscription is going to send an email is through an event, so we will be creating an evenit and we do that with the help of **EventBridge**.
   1. Go to EventBridge and create an **EventBridgeRule**.
      <img width="1680" height="671" alt="Screenshot 2025-07-12 at 7 11 34 PM" src="https://github.com/user-attachments/assets/fab056d6-3a52-4a4c-be1b-6ffd92cb0554" />
   2. Now create an Event, select **AWS Events** or **EventBridge partner events**.
   3. Select Event Patterns,
      1. check **pattern forms**.
      2. **AWS service** as codeCommit
      3. Event Type as All Event (we want to be notified for all the events
    
    <img width="1682" height="831" alt="Screenshot 2025-07-12 at 7 13 43 PM" src="https://github.com/user-attachments/assets/6ed37511-4d51-4b2e-8400-6b32c93c7029" />

   4. Select Targets - refer below screenshot
  <img width="1686" height="820" alt="Screenshot 2025-07-12 at 7 21 33 PM" src="https://github.com/user-attachments/assets/e2abeb74-f4b7-48c4-8108-cd39d2674da0" />

4. Once this is done, make some changes or upload a file to the CodeCommit repository and check if you have received any email.
<img width="1312" height="547" alt="Screenshot 2025-07-12 at 7 23 58 PM" src="https://github.com/user-attachments/assets/201fb124-12f1-4d26-a530-1d9abb97ca2f" />
