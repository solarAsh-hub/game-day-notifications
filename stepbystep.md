![github-header-image-5](https://github.com/user-attachments/assets/578e003e-be66-4374-8b72-e2c80b06bc45)
## 1. Set Up SNS (Simple Notification Service)

### Step 1: Create a Topic
1. Type `SNS` in the AWS search bar and select **Simple Notification Service**.
![image](https://github.com/user-attachments/assets/7bd6870d-8e35-4aab-a588-7e775cfb9bed)

2. On the left-hand menu, select **Dashboard**.
<img src="https://github.com/user-attachments/assets/074280b6-1093-4d6e-aa3c-950bb4e66349" alt="Image Description" width="300">


3. Click **Topics** and then click **Create Topic**.
![image](https://github.com/user-attachments/assets/8a02b040-ac60-433c-b41c-7d4535d45ef2)


4. Select **Standard** as the type.
![image](https://github.com/user-attachments/assets/d4440f04-4b58-4ab1-83d0-779b6c62e101)

5. Click **Create Topic**. Provide a name for your topic.
![image](https://github.com/user-attachments/assets/b49c8800-529f-4ce8-84b0-06106193d2c8)

6. After creating the topic, you will be directed to the topic's details page.
![image](https://github.com/user-attachments/assets/bacf54e4-1386-45fd-9bb7-c55696844f88)



### Step 2: Create a Subscription

1. Click **Create Subscription**.
![image](https://github.com/user-attachments/assets/469b30bc-6496-486c-b473-26c907f1a13c)

2. Under **Protocol**, select **Email**.
3. Enter your email under **Endpoint**.
![image](https://github.com/user-attachments/assets/d527312d-3e48-466e-b6a2-50e36c1b4a9a)

4. Click **Create Subscription**.
![image](https://github.com/user-attachments/assets/180b4b2d-74fc-44a9-9a0c-114b53672f39)


### Step 3: Confirm Subscription
1. Go to your email inbox and confirm the subscription.
![image](https://github.com/user-attachments/assets/df08351e-2501-4469-9f36-db414067b4c4)

3. Once confirmed, you will see the updated subscription status.
![image](https://github.com/user-attachments/assets/c90acb94-92d3-43b3-aab1-32994cef2193)

4. Click **gd_topic
![image](https://github.com/user-attachments/assets/20e01a43-d299-4eb3-b9a5-a72cb787e726)

5. The email and confirmation status will be displayed
![image](https://github.com/user-attachments/assets/51c4c9aa-d75a-4ffd-874f-09df61a147f1)





---

## 2. Set Up IAM Policies

### Step 1: Search and Open IAM
1. Type `IAM` in the AWS search bar and open it in a new browser tab.
![image](https://github.com/user-attachments/assets/648e4a98-3ed6-4352-a618-c02cafb00e97)

2. Navigate to the **Policies** section.

<img src="https://github.com/user-attachments/assets/42788457-f632-45b3-a0a0-5d6183a59c1f" alt="Image" width="300" height="400">


### Step 2: Create a Policy
1. Click **Create Policy
<img src="https://github.com/user-attachments/assets/c5e9ddfa-3717-4557-8785-94f60a624f60" alt="Image Description" width="900">


2. Select **SNS** as the service.
<img src="https://github.com/user-attachments/assets/0854be2a-03bd-4476-b4d0-8899173de630" alt="Image Description" width="900">

3. Switch to the **JSON** tab.
![image](https://github.com/user-attachments/assets/1a20bb84-ec8d-4270-a1c8-e025796ed368)

4. Go to the GitHub repository and copy the `.json` policy file.

![image](https://github.com/user-attachments/assets/dafd40fb-829f-4e3b-a7b8-066f4c2d6738)

6. Paste the template into the **JSON** editor.


7. Insert your subscription ID and change the action to `sns:Publish`.
![image](https://github.com/user-attachments/assets/841acf5c-3fa4-4a85-955a-047f8c2c941e)


9. Click **Next** in the bottom-right corner.
   
<img src="https://github.com/user-attachments/assets/7455ea77-e077-4def-9e3a-9044a073db1d" alt="Image Description" width="400"> 

10. Provide a name for the policy (e.g., `gd_sns_policy`) and click **Create Policy**.
![image](https://github.com/user-attachments/assets/3eefa714-ff5e-4ea2-9434-65babadec839)


---

## 3. Create an IAM Role

### Step 1: Define the Role
1. Go to the **Roles** section in IAM and click **Create Role**.
![image](https://github.com/user-attachments/assets/6c4c295d-9b49-45c9-af6f-d91ca7b12d72)

2. For the **Trusted entity type**, select **AWS Service**.
3. For **Use case**, select **Lambda** and click **Next**.
![image](https://github.com/user-attachments/assets/0bb9c4d9-74ca-47c4-9683-d12ecd8493bd)


### Step 2: Attach Policies
1. Search for `gd_sns_policy` and select it.
![image](https://github.com/user-attachments/assets/562b1823-e41a-4e22-8095-1b7e31153b65)

2. Add the `AWSLambdaBasicExecutionRole` policy.
![image](https://github.com/user-attachments/assets/2edde3a5-56e5-470e-bd86-892d5be43687)

3. Click **Next**.

### Step 3: Name the Role
1. Provide a name for the role (e.g., `gd_lambda_role`).

![image](https://github.com/user-attachments/assets/275ed784-9c0b-4cd8-bf96-6c5d73a9d4ee)

2. Verify the attached policies and click **Create Role**.

![image](https://github.com/user-attachments/assets/4ff52bfc-45c5-45a2-a05c-6b016a571c9b)


---

## 4. Create a Lambda Function

### Step 1: Define the Function
1. Search for `Lambda` in AWS and click **Create Function**.
![image](https://github.com/user-attachments/assets/9808e68c-fb08-43af-b387-2371f940c781)

2. Select **Author from Scratch**.
3. Provide a function name (e.g., `gd_notification`).
4. Choose **Python 3.13** as the runtime.
5. Set the execution role to use the previously created role (`gd_lambda_role`).
6. Click **Create Function**.
![image](https://github.com/user-attachments/assets/0ce9c6c9-98be-4112-ab3e-adb3fc8e74c9)


### Step 2: Add Code to the Lambda Function
1. Scroll down to the **Code Source** section.
![image](https://github.com/user-attachments/assets/e1c4d70c-4e22-4037-9f1f-2e156d2b5c7e)

2. Go to the GitHub repository and copy the `.py` file.
![image](https://github.com/user-attachments/assets/a5367d3c-cee2-4548-9e22-8e9b4cbbd90d)

3. Paste the code into the editor.
4. Click **Deploy**.
![image](https://github.com/user-attachments/assets/da98164d-f677-41d5-90df-ad5c9195ddc7)


### Step 3: Add Environment Variables
1. Click **Configuration** > **Environment Variables**.
![image](https://github.com/user-attachments/assets/b551ceaf-d1f6-4246-b042-50a669e80384)

2. Click **Edit** and then **Add Environment Variables**.
![image](https://github.com/user-attachments/assets/444adb65-a892-40ac-94db-703c85d1728d)

3. Add the following variables:
   - `NBA_API_KEY` (value: your API key from Sportsdata.io).
   - `sns_topic_arn` (value: ARN of the SNS topic created earlier).
![image](https://github.com/user-attachments/assets/3cd8632e-4a1d-47a3-a6ed-b4c69bae85ba)


---

## 5. Set Up Sportsdata.io API

1. Visit [Sportsdata.io](https://sportsdata.io) and sign up for a free trial.
![image](https://github.com/user-attachments/assets/51b9e36e-470d-4458-8ba6-d9a8ee1102f6)

2. After creating an account, find your API key under **Subscriptions**.
![image](https://github.com/user-attachments/assets/2d9911c9-9249-4b37-90c7-a32abd642197)


---

## 6. Test the Lambda Function

### Step 1: Configure and Test
1. Scroll up to the **Test** section in Lambda.
<img src="https://github.com/user-attachments/assets/eb9532e0-4e78-4d50-92b0-dca352c35bfe" alt="Image" width="400"> 

3. Create a test event named `test1`.
![image](https://github.com/user-attachments/assets/8adb314b-a42d-4eed-94bc-7090ca037270)

4. Save and run the test.

### Step 2: Verify Results
1. Upon successful execution, you will receive game-day stats via email with the correct time zone.
![image](https://github.com/user-attachments/assets/13f2159a-43fc-452b-9436-02647082a29e)


---

## 7. Set Up EventBridge Scheduler

### Step 1: Create a Rule
1. Search for `EventBridge` and click **Amazon EventBridge**.
![image](https://github.com/user-attachments/assets/2bf52fac-1c54-45ea-91f3-123875f0d9d7)

2. Click **Create Rule**.
![image](https://github.com/user-attachments/assets/238844f2-300d-42f8-8607-644224e4d78e)

3. Provide a name (e.g., `gd_rule`).
4. Set the rule type to **Schedule**.
![image](https://github.com/user-attachments/assets/487523b4-343c-427d-8f6c-cfa084f4643d)


### Step 2: Define the Schedule
1. Choose **Recurring Schedule** and set it to **Cron-based Schedule**:
   ```
   0 minutes and 9-23/2,0-2/2
   ```

   ![image](https://github.com/user-attachments/assets/7408dde9-bc4c-4b6e-9a9a-523d90502203)

2. Turn off the **Flexible Time Window**.
![image](https://github.com/user-attachments/assets/1b7ed792-8b34-4f98-98b2-088c3dea940f)


### Step 3: Link to Lambda
1. Choose **AWS Lambda** as the target.
![image](https://github.com/user-attachments/assets/46535423-e80b-4ee3-868a-c667e42d5ec5)

2. Select the function `gd_notification` and click **Next**.
![image](https://github.com/user-attachments/assets/260d57ca-04a8-457b-a623-c96bc6d37702)

4. Leave the settings as default and click **Next**.

### Step 4: Review and Create
1. Review the configuration and click **Create Schedule**.
![image](https://github.com/user-attachments/assets/c4ec2794-d348-49f4-9145-d6d5dc449208)

![image](https://github.com/user-attachments/assets/ce3e1411-bb9f-43c5-9d29-f7535127a89c)


---

Congratulations! You have successfully set up SNS, IAM Policies, Lambda Function, and EventBridge Scheduler for automated notifications.
