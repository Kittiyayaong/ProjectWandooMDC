# Module 10 - Connecting a GCP project

### Exercise 1: Create a GCP project

First you need to create a GCP project. 

1.	Navigate to [Create free GCP](https://www.google.com/aclk?sa=l&ai=DChcSEwiA7K7Gubn3AhUJuu0KHbACBZkYABAAGgJkZw&sig=AOD64_0Cc0zndLvPEu7wV4blEFwWvjOWag&q&adurl&ved=2ahUKEwihk6nGubn3AhVFZcAKHWP5BYkQ0Qx6BAgDEAE).  
  ![image](https://github.com/user-attachments/assets/74fe6bb0-4d75-4137-93a2-c8767d9248d2)

2.  Click **Get started for free**.
3.  Now select either an existing Google account or create a new one. 
4.  Follow the on-screen instructions to create the GCP project.
5.  At the end, you should be able to sign in to the [Google Cloud Console](console.cloud.google.com), and see the Dashboard:
  ![image](https://github.com/user-attachments/assets/e579c4a1-b800-4675-83ed-fe9adb8f816e)

6. Copy the project number and project ID, and keep them safe, as you'll be using them in the next exercise.

### Exercise 2: Create the GCP connector in Microsoft Defender for Cloud

In order to be able to protect your GCP resources in Microsoft Defender for Cloud, you need to create the GCP connector in Microsoft Defender for Cloud, which you will do in the following exercise. 


1. Go to the Azure Portal and open **Microsft Defender for Cloud** 
2. Go to **Environment Settings** in the left-hand tab.
3. Click **+ Add environment** and select **Google Cloud Platform** from the dropdown menu.

  ![image](https://github.com/user-attachments/assets/906b2d1a-c2ff-45db-9e3e-bb8b9bc0a7aa)

4. In the **Create GCP connector** page, then fill in all the details:

**Connector Name**: select a new name

**Onboard**: Single project 

**Subscription**: Choose your existing subscription

**Resource Group**: Create a new resource group and name it GCP.

**Location**: Select the location nearest you.

**Scan interval**: You can leave as is.

**GCP project number**: Paste this from exercise 1, or alternatively go to [Google Cloud Console](console.cloud.google.com) and copy the project number from the dashboard.

**GCP project id**: Paste this from exercise 1, or alternatively go to [Google Cloud Console](console.cloud.google.com) and copy the project ID from the dashboard.

  ![image](https://github.com/user-attachments/assets/bf19f11b-e6e1-4932-8607-24863ff63282)


5.  After filling everything in, click **Next: Select plans**.
6. In **Select plans**, the Foundational CSPM plan is enabled by default.

7. Ensure that the Defender CSPM, Servers, Containers and Database plans are set to **On**. 

  ![image](https://github.com/user-attachments/assets/dbceb075-a293-4704-9ead-65e0c01a2b77)

8. Select **Next: Configure access**.
9. Copy the GCP Cloud Shell script. 
  ![image](https://github.com/user-attachments/assets/dbe129b4-c594-437f-b83b-edeb38638f02)

10. Click **GCP Cloud Shell** button which will open up the GCP console with Cloud Shell.
11. Paste the script into the Cloud Shell.
  ![image](https://github.com/user-attachments/assets/34dcc055-9a0a-4795-8800-01e7e1fc1ff6)

12. Let the script run and after it finishes successfully return to Defender for Cloud. 
13. Back in the **Configure access** page click **Next: review and Generate**.
14. In the next screen, after validation completes succesfully, click **Create**

Now, you have successfully created a GCP connector in Microsoft Defender for Cloud. Now you'll be able to get GCP recommendations and alerts.

### Exercise 3: Investigate the GCP recommendations 

Once a vulnerable image has been pushed to the Azure Container Registry registry, then Microsoft Defender for Containers will start scanning the image for vulnerabilities. You will now look into the recommendations in Microsoft Defender for Cloud for this. 

> [!NOTE]
> You will need to create some GCP resources in order to see recommendations for GCP in Microsoft Defender for Cloud.
 
 1. Go to **Microsoft Defender for Cloud** in the **Azure Portal**.
 2. Go to the **Recommendations** tab in Defender for Cloud.
 3. In the upper taskbar, under **Scope**, select **GCP** only. 
 
  ![image](https://github.com/user-attachments/assets/c8aa6ad8-e5db-4155-9459-659f5ce952ba)


If you have existing GCP resources, then you'll be able to see recommendations associated with them.
