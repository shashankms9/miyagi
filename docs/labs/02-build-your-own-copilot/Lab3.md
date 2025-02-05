# Lab 3 - Expose Open AI through APIM

In this lab, you'll be exposing Open AI through APIM Gateway URL for Miyagi Application.

### Task 1: Verify the deployed API Management service and create an API

1. Navigate to Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

   ![](./Media/lab3-t1-s1.png)

1. From the left-menu, click on **APIs** **(1)** and select **HTTP** **(2)** under Define a new API to create an HTTP API.

   ![](./Media/lab3-t1-s2.png)

1. Enter the following values in the Create an HTTP API pane:
   
   | **Parameter**        | **Values**           | 
   | -------------------- | -------------------- | 
   | API Type **(1)**     | **Basic**            | 
   | Display name **(2)** | **miyagi-api**       |
   | Name **(3)**         | **miyagi-api**       |
   | Web service URL **(4)** | Enter the Endpoint of OpenAI resource named **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**  |
   | API URL suffix **(5)** | **miyagi** |
   | Click on  **(6)** | **Create** |

   ![](./Media/lab3-t1-s3.png)

1. Once API is created, click on **Overview** **(1)** from the left-menu and copy the **Gateway URL** **(2)** of API Management service. Paste it into Notepad for later use.

   ![](./Media/lab3-t1-s4.png)

### Task 2: Update the Docker Image for Recommendation service

1. Navigate to Visual Studio Code, open the `appsettings.json` file from the path `C:\LabFiles\miyagi\services\recommendation-service\dotnet\appsettings.json`.

   ![](./Media/lab3-t2-s1.png)

1. In the `appsettings.json` file, you have to replace the **endpoint** value from **OpenAI resource endpoint** to **API Gateway URL** which you have copied in Task-1 Step-4.

   ![](./Media/lab3-t2-s2.png)

1. From the Explorer, navigate to `Miyagi/services/recommendation-service/dotnet/` **(1)** path. Right-click on `dotnet` folder and select **Open in Integrated Terminal** **(2)** from the options tab to open terminal with required path.

   ![](./Media/lab3-t2-s3.png)

1. Now, you need to re-build the docker image for recommendation service by running the below docker command. Make to update the docker image name which was created earlier for recommendation service with the same name.

   ```
   docker build . -t [Docker_Image_Name_Recommendation_Service]
   ```

   ![](./Media/lab3-t2-s4.png)

1. Run following command to ACR login.

   **Note**: Please replace **<ACR_Name>** and **[Uname]** with **miyagiacr<inject key="DeploymentID" enableCopy="false"/>**. For [password], navigate to resource group > and select **miyagiacr<inject key="DeploymentID" enableCopy="false"/>** from the resources list. Under Settings, select **Access Keys** and select the check box for **Admin user** and then copy the password.

    ```
    docker login <ACRname>.azurecr.io -u [uname] -p [password]
    ```

1. Once you are logged into ACR. Run the below command to push the update docker image of recommendation service to container registery

   **Note**: Make sure to replace **miyagiacr[DID]** with **miyagiacr<inject key="DeploymentID" enableCopy="false"/>**.

   ```
   docker push miyagiacr[DID].azurecr.io/miyagi-recommendation:latest
   ```

   ![](./Media/lab3-t2-s5.png)

### Task 3: Revision of Recommendation service from Container App

1. Navigate to Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **miyagi-rec-ca-<inject key="DeploymentID" enableCopy="false"/>** Container App from the resources list.

   ![](./Media/lab3-t3-s1.png)

1. In the **miyagi-rec-ca-<inject key="DeploymentID" enableCopy="false"/>** Container App pane, select **Revisions** **(1)** under Applications from left-menu and then open the **Active Revision** named **miyagi-rec-ca-<inject key="DeploymentID" enableCopy="false"/>-SUFFIX** **(2)**.

   ![](./Media/lab3-t3-s2.png)

1. You will see the **Revision details** pop-up in the right-side, click on **Restart**. You will see a pop-up to restart the revision, click on **Continue** to confirm.

   ![](./Media/lab3-t3-s3.png)

   ![](./Media/lab3-t3-s3.1.png)

1. You will see the notification once the Revision is restarted successfully.

   ![](./Media/lab3-t3-s4.1.png)

1. Select **Ingress** **(1)** under Settings from left-menu and then scroll-down to Endponits of Conatiner App i.e, **miyagi-rec-ca-<inject key="DeploymentID" enableCopy="false"/>-SUFFIX** **(2)**. Click on secured link to open it.

   ![](./Media/lab3-t3-s4.png)

1. You can see the swagger page for the recommendation service as shown in the below image:

   ![](./Media/lab3-t3-s5.png)
