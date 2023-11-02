# Lab 2: Deploy Apps to Azure Container Apps

In this lab, you'll be building the docker images and publishing it to Azure Container Apps.

### Task 1: Build Docker Images for the Miyagi Application

1. Open Docker Application from the Lab VM desktop by double-clicking on it.
   ![](./Media/docker1.png)
   
1. On **Docker Subscription Service Agreement** window, click **Accept**.
   ![](./Media/docker2.png)

1. On **Welcome to Docker Desktop** window, click on **sign up**.

   ![](./Media/docker3.png)

1. On **Create your account** window, specify the following details:

   | **Settings**         | **Values**           | 
   | -------------------- | -------------------- | 
   | Email                | <inject key="AzureAdUserEmail"></inject>  | 
   | Username             | Odluser<inject key="DeploymentID" enableCopy="false"/>              |
   | Password             | <inject key="AzureAdUserPassword"></inject>         |
   | Send me occasional product updates and announcements. | Select the checkbox |
   |||

   ![](./Media/docker5.png)

1. On Sign in window, enter your email <inject key="AzureAdUserEmail"></inject> and click on **Continue**.

   ![](./Media/docker4.png)

1. On Enter your Password window, provide <inject key="AzureAdUserPassword"></inject> and click on **Continue**

    ![](./Media/docker(6).png)

1. If **This site is trying to open docker desktop.** pop up's click on **Open**.

1. Navigate to miyagi/ui/ right - click on ui/typescript in cascading menu, select **Open in intergate Terminal**.

1. Run following command to build a Docker image

    ```
    Docker build . -t miyagi-ui      
    ```
1. Run foolowing command to show the newly created image
   ```
   docker images
   ```
1. Run following command
   ```
   docker run -t miyagi-ui -p 8001:3000
   ```
1. Navigate back to **Docker desktop**, from left pane select **Images**.
   ![](./Media/docker7.png)

1. On **Images** blade, notice **miyagi-ui(1)** image is created, select **run(2)** icon .
   ![](./Media/docker8.png)

1. On **Run a new containe** window select the dropdown arrow.

   ![](./Media/docker9.png)

1. On **Run a new containe**, under **Ports** for **Host Port** enter **8001** and click on **Run**.

    ![](./Media/docker10.png)

1. On       click on **8001:3000** url link
   ![](./Media/docker11.png)
   
1. You should be able to see the application running locally
   
   ![](./Media/docker12.png)

### Task 2: Build Docker Images for the Recommendation service

1. Navigate to **miyagi/services/recommendation-service/dotnet** right - click on dotnet in cascading menu, select **Open in intergate Terminal**
1. Run following command to build a Docker image

   ```
   docker build . -t miyagi-recommemdation      
   ```
1. Run foolowing command to show the newly created image
   ```
   docker images
   ```
1. Run following command
   ```
   docker run -t miyagi-recommemdation -p 8002:80
   ```
1. Navigate back to **Docker desktop**, from left pane select **Images**.
   ![](./Media/docker7.png)

1. On **Images** blade, notice **miyagi-recommemdation(1)** image is created, select **run(2)** icon .
   ![](./Media/docker13.png)

1. On **Run a new containe** window select the dropdown arrow.

   ![](./Media/docker14-1.png)

1. On **Run a new containe**, under **Ports** for **Host Port** enter **8001** and click on **Run**.

    ![](./Media/docker14.png)

1. On       click on **8001:3000** url link
   ![](./Media/docker15.png)
   
1. You should be able to see the application running locally
   
   ![](./Media/docker16.png)

1. Navigate to miyagi/ui/ right - click on ui/typescript in cascading menu, select **Open in intergate Terminal**.

1. Run following command

   **Note**: Please replace miyagi[did] with miyagi<inject key="DeploymentID" enableCopy="false"/>

   ```
    docker tag miyagi-ui:latest miyagiacr{did].azurecr.io/miyagi-ui:latest
   ```
1. Run the following command to push image to container registery

   **Note**: Please replace miyagi[did] with miyagi<inject key="DeploymentID" enableCopy="false"/>

   ```
    docker push miyagiacr[did].azurecr.io/miyagi-ui:latest

   ```

1. Navigate to **miyagi/services/recommendation-service/dotnet** right - click on dotnet in cascading menu, select **Open in intergate Terminal**

1. Run following command

   **Note**: Please replace miyagi[did] with miyagi<inject key="DeploymentID" enableCopy="false"/>

   ```
    docker tag miyagi-recommendation:latest miyagiacr{did].azurecr.io/miyagi-recommendation:latest
   ```
1. Run the following command to push image to container registery

   **Note**: Please replace miyagi[did] with miyagi<inject key="DeploymentID" enableCopy="false"/>

   ```
    docker push miyagiacr[did].azurecr.io/miyagi-recommendation:latest

   ```

1. Navigate back to **Azure portal**

1. Select resource group miyagi-rg-<inject key="DeploymentID" enableCopy="false"/> resource group page, select miyagiacr-<inject key="DeploymentID" enableCopy="false"/> from resources list.

1. On miyagiacr-<inject key="DeploymentID" enableCopy="false"/> blade, **under** services select **Repositories**, notice miyagi-recommendation and miyagi-ui is present in Repositories.
1. In search bar serach and select **Container instances** and select **+ Create**.
1. 

