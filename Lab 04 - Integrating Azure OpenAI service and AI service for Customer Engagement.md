### **Integrating Azure OpenAI service and AI service for Customer Engagement**


**Lab Objective**

"As part of a POC, Contoso bank's marketing team would like to work with the Data Analytics and AI engineering teams who can help them build an app that uses data-driven AI-enhanced strategies to improve campaign targeting, so the marketing team can aim for a double-digit conversion rate of the asset customer base within the same budget.
In this lab, you will work on behalf of Contoso bank's AI engineering team to build this app, which makes use of Azure AI, AML and MLOps to achieve the solution."

**At the end of this lab you will know how-to:**

- Use AI-based recommendation systems for prediction
- Using insights from the enhanced segmentation
- Use Azure AI Search Services to enrich the chatbot with search


# Integrating Azure OpenAI service and AI service for Customer Engagement

>**Introduction:** :In this task, we will integrate the Azure OpenAI chatbot into Contoso Bank’s customer engagement platforms. The chatbot will serve as an interactive tool for customers, helping them explore loan products, get personalized loan recommendations, and receive real-time assistance. We will use Azure OpenAI’s natural language processing capabilities to ensure the chatbot delivers a smooth, human-like experience while collecting valuable customer data for further analysis.

### **Task 1 : Set Up Azure AI Search service**

In this task, we create Azure AI Search service for enriching the chatbot with search and query capabilities based on customer data and loan details.

1.  Switch back to Azure portal and search for **Azure AI search** and select it.

    ![](./media/image85.png)

2.  Click on **Create**.

    ![](./media/image86.png)

3.  Select below values and then click on **Review + Create**.

    - Subscription : Your Azure subscription.

    - Resource group - Select your existing resource group

    - Service name - `cbsb-aisearchXXXX` ( replace XXXX with unique number)

    - Location : **west us**/north Europe /location near to you

    ![](./media/image87.png)

4.  Click on **Create** now.

    ![](./media/image88.png)

5.  Wait for the deployment and then click on **Go to resource**.

    ![](./media/image89.png)

6.  Open a Notepad and make a note of URI value as  **AZURE_SEARCH_ENDPOINT** ,we use it to communicate to the service.

    ![](./media/image90.png)

7.  Navigate to the **Keys** section and grab the API Key and save it as AZURE_SEARCH_KEY in your notepad. You will need this to communicate
    with the service.

    ![](./media/image91.png)

### **Task 2 : Create Azure AI multi-service resource**

In this task, We create AI multi-service for NLP to enrich data and interact with customer through chatapp

1.  Create an Azure AI multi-service resource in the **same region as your search service region.**

2.  Open a new tab in a browser and go to  `https://portal.azure.com/#create/Microsoft.CognitiveServicesAllInOne`
    Sign in with your Azure subscription account

3.  Enter below values and then click on **Review + create**.

    - Subscription : Your Azure subscription

    - Resource group : Your existing resource group

    - Region : **Same region as your Search service region**

    - Name : `cbsb-aimultiserviceXXXX` (XXXX can be unique number)

    - Price tier : Standard S0

    - Select **By checking this box I acknowledge that I have read and understood all the terms below** check box.

    ![](./media/image92.png)

    ![](./media/image93.png)

4.  Review the details and click on **Create**.

    ![](./media/image94.png)

5.  Wait for the deployment to be completed. Deployment takes 1-2 min.
    Click on **Go to resource** button.

    ![](./media/image95.png)

6.  Select Keys and Endpoint under the Resource Management in the left navigation menu.Make a note of the AZURE_SEARCH_ENDPOINT and Key 1 values as this will be used later in the lab to communicate with the service.

    ![](./media/image96.png)

### **Task 3 : Create Azure OpenAI resource**

In this task, we create Azure OpenAI resource to deploy OpenAI models for embeddings and completions to use them in Chatapp

1.  Open a new tab and search for **Azure OpenAI** service and select
    it.

    ![](./media/image97.png)

2.  Click on **Create**.

    ![](./media/image98.png)

3.  Enter below details and click on

    - Subscription : Azure subscription

    - Resource group -  your Azure resource group

    - Region : **East US**

    - Name -  `cbazopenaiXXXX` (XXXX can be unique number)

    - Price tier -**Standard S0**

    ![](./media/image99.png)

4.  Click on **Next- > Next- > Create.**

    ![](./media/image100.png)

    ![](./media/image101.png)

    ![](./media/image102.png)

5.  Once the deployment completes, click on **Go to resource**

    ![](./media/image103.png)

6.  Expand Resource management from left navigation ,click on **Keys and  Endpoint**.Copy endpoint value and assign to **AZURE_OPENAI_ENDPOINT** ,
    Copy key and assign to **AZURE_OPENAI_KEY**.Save both these variables in     your Notepad

    ![](./media/image104.png)

7.  Click on **Overview**, right click on **Go to Azure OpenAI Studio** and select **Open link in new tab**.

    ![](./media/image105.png)

8.  Azure OpenAI opens in new tab. Sign in if required. Close pop -ups

    ![](./media/image106.png)

9.  Click on **Deployment** from left navigation menu, select **Deploy model -> Deploy base model.**

    ![](./media/image107.png)

10. Search for `gpt-35-turbo-16k` and select it and then click on **Confirm**

    ![](./media/image108.png)

11. Click on **Customize** button

    ![](./media/image109.png)

12. Select available region(same region as your Azure OpenAI region) and set Tokens per Minute Rate limit to max and then click on
    **Deploy**.

    ![](./media/image110.png)

13. Repeat above steps and deploy- `text-embedding-ada-002`

    ![](./media/image111.png)

    ![](./media/image112.png)

14. Set maximum **Tokens per Minute Rate Limit** and then click on **Deploy.**

    ![](./media/image113.png)

    ![](./media/image114.png)

### **Task 4 : Add a data source to Azure AI search service**

In this task, we add data source of all resource to enrich data.

1.  Switch back to Azure portal -> Resource group- > Azure AI search service.

    ![](./media/image115.png)

2.  Click on **Search management -> Data source** . Select **Add data source -> Add data source.**

    ![](./media/image116.png)

3.  Select below values and then click on **Create.**

    - Data source : Azure blob Storage

    - Name : unique name (eg : `enrichdatasource`)

    - Subscription : your Azure subscription

    - Storage account- your Azure storage account

    - Blob container -  `azureml-blob-XXXX` (your default blob container where raw data is uploaded.)

    ![](./media/image117.png)

    ![](./media/image118.png)

### **Task 5 : Create skillsets in Azure AI search**

In this task, we crearte a skillset  object in Azure AI Search that's attached to an indexer. It contains one or more skills that call built-in AI 

1.  On Overview page, click on **Import data** tab.

    ![](./media/image119.png)

2.  Select **Existing data source** and select **enrichdatasourc**, then
    click **Next: Add cognitive skill (Optional)**

    ![](./media/image120.png)

3.  Expand **Attach AI Services** and select the AI multi service
    created in previous task.

    ![](./media/image121.png)

4.  Expand **Add enrichments** ,keep default skillset name. Enable OCR and select all Extract personally identifiable information **except
    Extract personally identifiable information** then click on **Next: Customize target index.**

    ![](./media/image122.png)

5.  Enter Index name as - **customer-index ,** click on **Add filed**.

    ![](./media/image123.png)

6.  Enter **Field name** as : `customer_id`, select type="Edm.String" and select all skills

    ![](./media/image124.png)

7.  Add below fields and then click **Next : Create an indexer**

    - Field name -  `customer_name` , Type - Edm.String ,Skills -All

    - Field name -  `CustomerSince` , Type - Edm.Int32 ,Skills -All

    - Field name -  `campaign_result` , Type - Edm.String ,Skills -All

    - Field name -  `age` , Type - Edm.String ,Skills -All


    ![](./media/image125.png)

8.  Enter the indexer name : `customer-azureblob-indexer` and click **submit**.

    ![](./media/image126.png)

    ![](./media/image127.png)

6.  Click on **Indexer** under **Search management**, you should see new indexer with documents

    ![](./media/image128.png)

7.  Click on **Indexes -> customer-index.** Wait for the Vetor index size to update.

    ![](./media/image129.png)

8.  Search with High value customers, you should search results.

    ![](./media/image130.png)

### **Task 6 : Build and Deploy Chat app in Azure AI Studio.**

In this task we create, configure, and deploy the chatbot powered by Azure AI and integrated with the AML model.

1.  Open a new tab and go to `https://ai.azure.com` and sign in with your Azure subscription account.

    ![](./media/image131.png)

2.  Click on **New project.**

    ![](./media/image132.png)

3.  Enter the unique project name(`cbsbaoai-proj`) and then click on Create a new hub link on the Hub drop down link as shown in below
    image.

    ![](./media/image133.png)

4.  Enter below values and then click on **Next**

    - Hub name : `cbcbaoaihub`

    - Subscription : Your Azure subscription

    - Resource group - your existing resource group

    - Region -same region as your Azure Open AI region

    - Connect Azure AI Services or Azure OpenAI : Select your Azure OpenAI service

    - Connect Azure AI Search : Select your Azure AI Search

    ![](./media/image134.png)

5.  Review the details and then click on **Create a project** button.

    ![](./media/image135.png)

    ![](./media/image136.png)

6.  From left navigation menu, click on **Chat** under **Playground** .In Setup ,select **Add your data** and then click on **Add a new
    data source**.

    ![](./media/image137.png)

7.  Select **Azure AI Search** as **Data source** and then click **Next**.

    ![](./media/image138.png)

8.  Select your **Azure AI Search** service and the Index your  **customer-index**,then click Next.

    ![](./media/image139.png)

9.  Keep the default values, click Next.

    ![](./media/image140.png)

10. Click on **Create** now.

    ![](./media/image141.png)

    ![](./media/image142.png)

11. Enter below prompt in Type here query text bod and press send button.

    `Details of Customer ID- 3`

    ![](./media/image143.png)

12. Enter below prompt and press send

    `List high value customers`

    ![](./media/image144.png)

    ![](./media/image145.png)

13. Now, you are ready to deploy your app. Click on **Deploy- > as a web app.**

    ![](./media/image146.png)

14. Enter below details and then click on **Deploy**. Deployment takes 5-10 min to complete.

    - Select **Create a new web app** radio button

    - Name : should be unique name (eg `mlappchatappXXXX` - XXXX can be unique number)

    - Subscription : Your Azure subscription

    - Resource group - your resource existing resource group

    - Location - West US / East US/East US 2 ( usually east us has high demand and deployment may fail). You can use the same location as the hub

    - Pricing plan : Standard (S1) /S2

    ![](./media/image147.png)

    ![](./media/image148.png)

    ![](./media/image149.png)

>**Summary:** We have successfully integrated the Azure OpenAI chatbot into Contoso Bank’s customer engagement platform. The chatbot provides real-time assistance to potential borrowers, enhancing digital engagement and improving the customer experience. This integration allows the bank to deliver personalized recommendations based on customer behavior and preferences, further supporting targeted marketing efforts.


