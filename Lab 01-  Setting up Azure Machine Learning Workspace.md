### **Lab 01 - Setting up Azure Machine Learning Workspace**

#### **Introduction**
Contoso Bank is undergoing a comprehensive digital transformation across all its departments to enhance their operational efficiency and customer engagement. Currently, the bank's customer base is predominantly composed of liability customers (depositors), while the asset customer base (borrowers) is relatively smaller. The bank aims to rapidly expand its asset customer segment to generate additional revenue through loan interests.

In the previous quarter, the bank launched a marketing campaign targeting potential borrowers, which resulted in an average conversion rate in the single digits. As part of its digital transformation strategy, the marketing department seeks to design more effective campaigns that leverage targeted marketing techniques. The goal is to significantly increase the conversion ratio to double digits while maintaining the same budget as the last campaign. This initiative is pivotal for driving growth and maximizing the bank's profitability through increased borrowing activity.

**Lab Objective**

As part of a POC, Contoso bank's marketing team would like to work with the Data Analytics and AI engineering teams who can help them build an app that uses data-driven AI-enhanced strategies to improve campaign targeting, so the marketing team can aim for a double-digit conversion rate of the asset customer base within the same budget.
In this lab, you will work on behalf of Contoso bank's AI engineering team to build this app, which makes use of Azure AI, AML and MLOps to achieve the solution.

**By the end of this lab you will know how-to:**

- Setup Azure Machine Learning workspace

**Tools and Technologies used in this lab :**

1.  **Azure Machine Learning (AML)**: For building, training, and
    deploying the predictive model in the banking scenario.

2.  **MLOps**: For covering model training, deployment, and automated model
    management.

3.  **Azure AI Studio**: Used to create, configure, and deploy the
    chatbot powered by Azure AI and integrated with the AML model.

4.  **Azure AI Search**: For enriching the chatbot with search and query
    capabilities based on customer data and loan details.

5.  **Azure App Service**: To host and manage the deployed web
    application (chat app).

6.  **Azure Blob Storage**: For storing and managing datasets used in
    training and prediction.

7.  **Python SDK**: For interacting with Azure services, building the
    model and working with data pipelines.

# Exercise 1: Setting up Azure Machine Learning Workspace
#### **Introduction:**
In this exercise, we will set up the foundational components of the Azure Machine Learning workspace. This workspace will be the environment where we train, deploy, and manage machine learning models. The tasks involves creating a new Azure Machine Learning resource, configuring the necessary compute resources, and ensuring that all security and access controls are in place. This environment will serve as the backbone for building predictive models and integrating MLOps into Contoso Bank’s marketing strategies. We are also assigning required permissions to the subscription to perform the above tasks and uploading loan guide documents for chatapp to use and respond to customer queries


### **Task 1: Setting up Azure Machine Learning Workspace** 

#### **Introduction:**
>In this task, we will setup AML workspace for building, training, and deploying the predictive model in the banking scenario.

1. In the Edge browser, navigate to Azure Portal at
`https://portal.azure.com` and Sign In using your Azure user credentials (provided in the Resources section).

2. Click on Cloud shell and select **Bash**.

    ![](./media/image1.png)

3. Select **No storage account** **required** radio button , select **your Azure subscription** and then click on **Apply**.

    ![](./media/image2.png)

4. Run below command to clone the project solution. +++git clone https://github.com/technofocus-pte/MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration.git+++

    ![](./media/image3.png)


5. Install Python dependencies (like azureml-sdk):Run below commands +++pip install azureml-sdk+++

    ![](./media/image4.png)

6. Run below script to create resources in Azure.

    +++cd MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration/scripts/+++

    +++chmod +x setup.sh+++

    +++./setup.sh+++

    ![](./media/image5.png)

7. Wait for the script to complete. It takes 4-5 minutes for the script to run.

    ![](./media/image6.png)

    ![](./media/image7.png)

8. Close the **Cloud shell** and click on **Resource Group** tile.

    ![](./media/image8.png)

9. Click on your resource group name.

    ![](./media/image9.png)

10. Go through the list of the resources to ensure all the resources are created.

    ![](./media/image10.png)

11. Click on **Azure Machine Learning workspace** name.

    ![](./media/image11.png)

12. Click on **Access control (IAM)** from left navigation menu, click
    on **Add -> Add role assignment.**

    ![](./media/image12.png)

13. Select **Privileged administrator roles -> Contributor** role and
    then click **Next.**

    ![](./media/image13.png)

14. Select **user,group or service principal** radio button, click on
    **Select members** link. Search for your Azure subscription tenant
    ,select it and then click on **Select**.

    ![](./media/image14.png)

15. Click on **Review +assign**.

    ![](./media/image15.png)

16. Again,click on **Review + assign**.

    ![](./media/image16.png)

17. Click on **Overview** from left navigation and then click on
    **Launch studio** button.

    ![](./media/image17.png)

18. AML studio opens in new tab. Sign in with your Azure subscription
    account.

    ![](./media/image18.png)

19. Click on Compute in the Manage section, from the left navigation menu. Note that the AML compute you created is listed and the State is **Running**.

    ![](./media/image19.png)

20. Click on **Compute clusters** , cluster should have created
    successfully.

    ![](./media/image20.png)
>#### **Summary:** In this task, we successfully created an Azure Machine Learning workspace and configured compute resources, which will be used for training and deploying machine learning models. These foundational steps ensure that we have a secure, scalable environment in place to support the bank's data science and marketing initiatives.

### **Task 2 : Assign roles to the subscription**

> We need to assign sufficient roles and permissions to your user account on the created resource group in order to be able to index and enrich the customer data, and to be able to create OpenAI services in the workspace.

1. Switch back to **Azure portal** home page and click on **Resource group** tile.

    ![](./media/image21.png)

2. Click on your resource group name.

    ![](./media/image22.png)

3. Click on **Access control(IAM)** from left navigation menu, select **Add - > Add role assignment.**

    ![](./media/image23.png)

4. Search for `AzureML Compute Operator` and select it. Click on
    **Next** .

    ![](./media/image24.png)

5. Select **users, group or service principal** radio button, click on **select members** hyper link. Search for your **aoaitfsXXXX**
    (relace XXXX with your tenant number) id and select it. Finally, click on **Select** button

    ![](./media/image25.png)

6. Click on **Next**.

    ![](./media/image26.png)

7. Click on **Review + assign** now.

    ![](./media/image27.png)

8.  After role assignments are successful, click on **Add -> Add role
    assignment**.

    ![](./media/image28.png)

9.  Search for the below roles and assign them. Repeat above steps for below
    roles as well

    `Search Index Data Reader`

    `Cognitive Services Contributor`

    `Cognitive Services OpenAI User`

    `Search Service Contributor`

    `Azure AI Developer`

    ![](./media/image29.png)

    ![](./media/image30.png)

    ![](./media/image31.png)

    ![](./media/image32.png)

    ![](./media/image33.png)

21. Click on **Role assignments.**

    ![](./media/image34.png)

22. You should be able to see all the assigned roles to your tenant.

    ![](./media/image35.png)

### **Task 3 : Upload Contoso Bank loan documents into Azure Storage account**

 When you create an Azure Machine Learning workspace, a Storage Account
is automatically created and connected to your workspace.Upload Contoso Bank loan documents and access them to answer customer queries in Chatapp

1.  In **Azure portal- > Resource group** , click on Storage account name

    ![](./media/image36.png)

2.  Select **Configuration** under **Settings**. Then set **Allow Blob anonymous access** to **Enabled** and then click **Save**.

    ![](./media/image37.png)

3.  Click on **Containers** under **Data storage** and click **azureml-blobstore-XXXXXXXXXXXXX** container.

    ![](./media/image38.png)

4.  Click on **Upload -> Browse for files** . select the files from **C:\Labfiles\resources** folder and then click on **Open**.

    ![](./media/image39.png)

5.  Click on **Upload**

    ![](./media/image40.png)

    ![](./media/image41.png)

>#### **Summary:** By the end of this exercise, we successfully created an Azure Machine Learning workspace and configured compute resources, which will be used for training and deploying machine learning models with required permissions to perform tasks. These foundational steps ensure that we have a secure, scalable environment in place to support the bank's data science and marketing initiatives.

