# Lab 3 - Expose Open AI through APIM

In this lab, you'll be exposing Open AI through APIM as a gateway for Miyagi Application.

### Task 1: Verify the deployed API Management service and create an API

1. Navigate to Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

   ![](./Media/lab3-t1-s1.png)

1. From the left-menu, click on **APIs** **(1)** and select **HTTP** **(2)** under Define a new API to create an HTTP API.

   ![](./Media/lab3-t1-s2.png)

1. In Create an HTTP API pane, select **Basic** API **(1)** and enter **Display name** as **miyagi-api** **(2)**. Leave **Name** as default with the provided Display name **(3)**. For **Web service URL**, enter the **endpoint** **(4)** of OpenAI resource named **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**. Enter **API URL suffix** as **miyagi** **(5)** and then click on **Create** **(6)**.

   ![](./Media/lab3-t1-s3.png)

1. Once API is created. Click on **Overview** **(1)** from the left-menu, copy the **Gateway URL** **(2)** of API Management service for later use and paste it in notepad.

   ![](./Media/lab3-t1-s3.png)

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

1. 

