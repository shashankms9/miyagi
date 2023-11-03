# Lab 3 - Expose Open AI through APIM

In this lab, you'll be exposing Open AI through APIM as a gateway for Miyagi Application.

### Task 1: Verify the deployed API Management service and create an API

1. Navigate to Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

   ![](./Media/lab3-t1-s1.png)

1. From the left-menu, click on **APIs** **(1)** and select **HTTP** **(2)** under Define a new API to create an HTTP API.

   ![](./Media/lab3-t1-s2.png)

1. In Create an HTTP API pane, select **Basic** API **(1)** and enter **Display name** as **miyagi-api** **(2)**. Leave **Name** as default with the provided Display name **(3)**. For **Web service URL**, enter the **endpoint** **(4)** of Open AI resource named **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**. Enter **API URL suffix** as **miyagi** **(5)** and then click on **Create** **(6)**.

   ![](./Media/lab3-t1-s3.png)
