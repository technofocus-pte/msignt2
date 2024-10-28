### **Leveraging MLOps and Azure OpenAI for Targeted Marketing: Contoso Bank's Journey to Expand Borrower Base**

Contoso Bank is undergoing a comprehensive digital transformation across
all its departments to enhance its operational efficiency and customer
engagement. Currently, the bank's customer base is predominantly
composed of liability customers (depositors), while the asset customer
base (borrowers) is relatively smaller. The bank aims to rapidly expand
its asset customer segment to generate additional revenue through loan
interests.

In the previous quarter, the bank launched a marketing campaign
targeting potential borrowers, which resulted in an average conversion
rate in the single digits. As part of its digital transformation
strategy, the marketing department seeks to design more effective
campaigns that leverage targeted marketing techniques. The goal is to
significantly increase the conversion ratio to double digits while
maintaining the same budget as the last campaign. This initiative is
pivotal for driving growth and maximizing the bank's profitability
through increased borrowing activity.

**Lab Objective**

"As part of a POC, Contoso bank's marketing team would like to work with the Data Analytics and AI engineering teams who can help them build an app that uses data-driven AI-enhanced strategies to improve campaign targeting, so the marketing team can aim for a double-digit conversion rate of the asset customer base within the same budget.
In this lab, you will work on behalf of Contoso bank's AI engineering team to build this app, that makes use of Azure AI, AML and MLOps to achieve the solution."

**At the end of this lab you will know how-to:**

1. Import data sets to storage account and clean the data using python SDK notebook
2. Build a Machine learning model using Azure machine Learning
3. Use AI-based recommendation systems for prediction
4. Using insights from the enhanced segmentation
5. Use Azure AI Search Services to enrich the chatbot with search
6. use Azure AI Bot Service for customer engagement using chatbot

**Tools/Technologies/Apps used :**

1.  **Azure Machine Learning (AML)**: For building, training, and
    deploying the predictive model in the banking scenario.

2.  **MLOps**: For applying DevOps practices in machine learning
    workflows, covering model training, deployment, and automated model
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
    model, and working with data pipelines.

### **Task 1: Create Azure machine learning resources** 

1.   In the Edge browser, navigate to Azure Portal at
`https://portal.azure.com` and Sign In using your Azure user credentials (provided in the resources section).

2.  Click on Cloud shell and select **Bash**.

![](./media/image1.png)

3.  Select **No storage account** **required** radio button , select
    **your Azure subscription** and then click on **Apply**.

![](./media/image2.png)

4.  Run below command to clone the project solution.

+++git clone https://github.com/technofocus-pte/MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration.git+++

![](./media/image3.png)

5.  Install Python dependencies (like azureml-sdk):Run below commands

+++pip install azureml-sdk+++

![](./media/image4.png)

6.  Run below script to create resources in Azure.

+++cd MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration/scripts/+++

+++chmod +x setup.sh+++

+++./setup.sh+++

![](./media/image5.png)

7.  Wait for the script to run completely. It takes 4-5 minutes to
    complete.
![](./media/image6.png)

![](./media/image7.png)

8.  Close the **Cloud shell** and click on **Resource group** tile.

![](./media/image8.png)

9.  Click on resource group name.

![](./media/image9.png)

10. Make sure all the resources are created.

![](./media/image10.png)

11. Click on **Azure Machine Learning workspace** name.

![](./media/image11.png)

12. Click on **Access control (IAM)** from left navigation menu, click
    on **Add -> Add role assignment.**

![](./media/image12.png)

13. Select **Privileged administrator roles -> Contributor** role and
    then click **Next.**

> ![](./media/image13.png)

14. Select **user,group or service principal** radio button, click on
    **Select members** link. Search for your Azure subscription tenant
    ,select it and then click on **Select**.

> ![](./media/image14.png)

15. Click on **Review +assign**.

![](./media/image15.png)

16. Again click on **Review + assign**.

> ![](./media/image16.png)

17. Click on **Overview** from left navigation and then click on
    **Launch studio** button.

![](./media/image17.png)

18. AML studio opens in new tab. Sign in with your Azure subscription
    account.

![](./media/image18.png)

19. Click on **Compute** from left navigation menu and make sure compute
    instances and clusters are created and running status.

![](./media/image19.png)

20. Click on **Compute cluster**s , cluster should have created
    successfully.

![](./media/image20.png)

### Task 2 : Assing roles to the subscription

1.  Switch back to **Azure portal** home page and click on **Resource group** tile.

![](./media/image21.png)

2.  Click on your resource group name.

![](./media/image22.png)

3.  Click on **Access control(IAM)** from left navigation menu, select
    **Add - > Add role assignment.**

![](./media/image23.png)

4.  Search for `AzureML Compute Operator` and select it. Click on
    **Next** .

![](./media/image24.png)

5.  Select **users, group or service principal** radio button, click on
    **select members** hyper link. Search for your **aoaitfsXXXX**
    (relace XXXX with your tenant number) id and select it. Finally,
    click on **Select** button

![](./media/image25.png)

6.  Click on **Next**.

![](./media/image26.png)

7.  Click on **Review + assign** now.

![](./media/image27.png)

8.  After role assignment successful, click on **Add -> Add role
    assignment**.

![](./media/image28.png)

9.  Search for below roles and assign them. Repeat above steps for below
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

### Task 3 : Upload resource into Azure Storage account

 When you create an Azure Machine Learning workspace, a Storage Account
is automatically created and connected to your workspace. You'll
explore how the Storage Account is connected.

1.  In Azure portal- > Resource group , click on Storage account name

![](./media/image36.png)

2.  Select **Configuration** under **Settings**. Then set **Allow Blob
    anonymous access** to **Enabled** and then click **Save**.

![](./media/image37.png)

3.  Click on **Containers** under **Data storage** and click
    **azureml-blobstore-XXXXXXXXXXXXX** container.

![](./media/image38.png)

4.  Click on **Upload -> Browse for files** . select the files from
    **C:\Labfiles\resources** folder and then click on **Open**.

![](./media/image39.png)

5.  Click on **Upload**

![](./media/image40.png)

![](./media/image41.png)

### Task 4 : Register Datasets

1.  Switch back to AML studio tab ( open new tab -> Azure Portal->
    Resource group -> AML resource -> Launch Azure Machine learn
    studio), Under **Asset** , click on **Data** from left navigation
    menu and then click on **Data asset-> Create.**

![](./media/image42.png)

2.  Enter the name as : `Dataset1` and select Type : **Tabular** and
    then click on **Next**.

![](./media/image43.png)

3.  Select **From local files tile** and then click on **Next**.

![](./media/image44.png)

4.  Select Datastore type **as Azure Blob storage** and select the
    default blob storage( you can check in Data-\> Datastore) and click
    on **Next**.

![](./media/image45.png)

5.  Click on **Upload files or folder** drop down and select **Upload
    files.**

![](./media/image46.png)

6.  Browse to **C:\Labfiles\Data** folder and select **Dataset1** and
    then click on **Open**.

![](./media/image47.png)

7.  Click **Next** now.

![](./media/image48.png)

8.  Review the data and change If you want to then click on **Next**.

![](./media/image49.png)

9.  Click **Next** now.

![](./media/image50.png)

10. Review the details and then click on **Create**.

![](./media/image51.png)

![](./media/image52.png)

11. Repeat above steps and register Dataset2.CSV with the name `Dataset2` also.

![](./media/image53.png)

### Task 5 : Set Up Azure AI Search service

1.  Switch back to Azure portal and search for **Azure AI search** and
    select it.

![](./media/image85.png)

2.  Click on **Create**.

![](./media/image86.png)

3.  Select below values and then click on **Review + Create**.

    - Subscription : Your Azure subscription.

    - Resource group - your resource group

    - Service name - `cbsb-aisearchXXXX` ( replace XXXX with unique number)

    - Location : **west us**/north Europe /location near to you

![](./media/image87.png)

4.  Click on **Create** now.

> ![](./media/image88.png)

5.  Wait for the deployment and then click on **Go to resource**.

![](./media/image89.png)

6.  Open a Notepad and make a note of URI value as
    **AZURE_SEARCH_ENDPOINT** ,we use it to communicate to the service.

![](./media/image90.png)

7.  Navigate to the **Keys** section and grab the API Key and save it as
    AZURE_SEARCH_KEY in your notepad. You will need this to communicate
    with the service.

> ![](./media/image91.png)

### Task 6 : Create Azure AI multi-service resource 

1.  Create an Azure AI multi-service resource in the **same region as
    your search service region.**

2.  Open a new tab in a browser and go to  `https://portal.azure.com/#create/Microsoft.CognitiveServicesAllInOne`
    Sign in with your Azure subscription account/

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

6.  Click on **Keys and Endpoint** under **Resource management**. Make a
    note of Key and endpoint to use them in next tasks.

![](./media/image96.png)

### Task 7 : Create Azure OpenAI resource

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

    - Price tier -**Standard**

![](./media/image99.png)

4.  Click on **Next- > Next- > Create.**

![](./media/image100.png)

![](./media/image101.png)

![](./media/image102.png)

5.  Once the deployment completes, click on **Go to resource**

![](./media/image103.png)

6.  Expand Resource management from left navigation ,click on Keys and
    Endpoint.Copy endpoint value and assign to AZURE_OPENAI_ENDPOINT ,
    Copy key and assign to AZURE_OPENAI_KEY.Save both these variables in
    your Notepad

![](./media/image104.png)

7.  Click on **Overview**, right click on **Go to Azure OpenAI Studio**
    and select **Open link in new tab**.

![](./media/image105.png)

8.  Azure OpenAI opens in new tab. Sign in if required. Close pop -ups

![](./media/image106.png)

9.  Click on **Deployment** from left navigation menu, select **Deploy
    model -> Deploy base model.**

![](./media/image107.png)

10. Search for `gpt-35-turbo-16k` and select it and then click on
    **Confirm**

![](./media/image108.png)

11. Click on **Customize** button

![](./media/image109.png)

12. Select available region(same region as your Azure OpenAI region) and
    set Tokens per Minute Rate limit to max and then click on
    **Deploy**.

![](./media/image110.png)

13. Repeat above steps and deploy- `text-embedding-ada-002`

![](./media/image111.png)

![](./media/image112.png)

14. Set maximum **Tokens per Minute Rate Limit** and then click on **Deploy.**

![](./media/image113.png)

![](./media/image114.png)


### Task 8 : Access Notebook to train a model with the Azure Machine 

1.  Click on **Compute -> Computer instance.** Select **Compute
    instance** name and then click under **Application** and select
    **Terminal.**

![](./media/image54.png)

2.  Close the pop up window.

![](./media/image55.png)

12. In the terminal, install the Python SDK on the compute instance by
    running the following commands in the terminal:

`pip install azure-ai-ml`

>Note : Ignore any (error) messages that say that the packages couldn't
>be found and uninstalled.

![](./media/image56.png)

13. Run the following command to clone a Git repository containing a
    notebook, data, and other files to your workspace:

`git clone https://github.com/technofocus-pte/MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration.git`

![](./media/image57.png)

14. When the command has completed, in the **Files** pane,
    click **↻** to refresh the view and verify that a
    new **Users/*your-user-name*/MLops…** folder has been created.

![](./media/image58.png)

15. Stay back in the same page to continue.

### Task 9 : Run the notebook to Work with Data

1.  Expand **models** folder and select the **ContosoBankAMLmodel.ipynb** notebook.

2.  Run the first cell to check the latest version of azure-ai-ml
    package.

> Note: If the azure-ai-ml package is not installed, run **pip install
> azure-ai-ml** to install it

![](./media/image59.png)

> Note : Select **Authenticate** and follow the necessary steps if a
> notification appears asking you to authenticate.

3.  Verify that the notebook uses the **Python 3.8 - AzureML** kernel.If
    its not using then select it from drop down.

![](./media/image60.png)

4.  Restart the kernel as shown in below image.

![](./media/image61.png)

5.  Click on **Restart**.

![](./media/image62.png)

6.  Read description of each cell and run it

![](./media/image63.png)

7.  Run cell to list datastores in storage account.

![](./media/image64.png)

8.  Run the cell to clean , merge datasets and save into
    **merge_data.CSV** file.

![](./media/image65.png)

![](./media/image66.png)

8.Run cell to preview merge_data.csv file.Run all the cells

![](./media/image67.png)

9.  Run cell to Describe the data after transposing

![](./media/image68.png)

10. Run all the cells and check merged_data to check number of rows.

![](./media/image69.png)

11. Run cell to show unique values in the LoadOnCard Column.

![](./media/image70.png)

12. Run cell to show distribution of data in LoanonCard column

![](./media/image71.png)

13. Read and run each cell under Model Preparation and explore.

![](./media/image72.png)

![](./media/image73.png)

![](./media/image74.png)

14. Read and run cell in Apply Logistic Regression

![](./media/image75.png)

15. Run cell to define and register financial-experiment-env environment

![](./media/image76.png)

16. Run cell to view registered environments.

![](./media/image77.png)

17. Run all cells to run an experiment.

![](./media/image78.png)

18. Run the experiment cell . wait for the experiment to complete . It
    takes **15-20 minutes.**. 

![](./media/image79.png)

![](./media/image80.png)

![](./media/image81.png)

19. Run each cell under deploy the model as a web service.

![](./media/image82.png)

19. Run the cell to provide web service endpoint.

![](./media/image83.png)

20. Run all cells to predict Asset and liability Customers.

![](./media/image84.png)

### Task 10 : Add a data source to Azure AI search service

1.  Switch back to Azure portal -> Resource group- > Azure AI search
    service.

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

### Task 11 : Create skillsets in Azure AI search

1.  On Overview page, click on **Import data** tab.

![](./media/image119.png)

2.  Select **Existing data source** and select **enrichdatasourc**, then
    click **Next: Add cognitive skill (Optional)**

> ![](./media/image120.png)

3.  Expand **Attach AI Services** and select the AI multi service
    created in previous task.

![](./media/image121.png)

4.  Expand **Add enrichments** ,keep default skillset name. Enable OCR
    and select all Extract personally identifiable information **except
    Extract personally identifiable information** then click on **Next:
    Customize target index.**

> ![](./media/image122.png)

5.  Enter Index name as - **customer-index ,** click on **Add filed**.

> ![](./media/image123.png)

6.  Enter **Field name** as : `customer_id`, select type="Edm.String"
    and select all skills

![](./media/image124.png)

7.  Add below fields and then click **Next : Create an indexer**

    - Field name -  `customer_name` , Type - Edm.String ,Skills -All

    - Field name -  `CustomerSince` , Type - Edm.Int32 ,Skills -All

    - Field name -  `campaign_result` , Type - Edm.String ,Skills -All

    - Field name -  `age` , Type - Edm.String ,Skills -All


> ![](./media/image125.png)

8.  Enter the indexer name : `customer-azureblob-indexer` and click
    **submit**.

![](./media/image126.png)

![](./media/image127.png)

6.  Click on **Indexer** under **Search management**, you should see new
    indexer with documents

![](./media/image128.png)

7.  Click on **Indexes -> customer-index.** Wait for the Vetor index
    size to update.

![](./media/image129.png)

8.  Search with High value customers, you should search results.

![](./media/image130.png)

### Task 12 : Build and Deploy Chat app in Azure AI Studio.

1.  Open a new tab and go to `https://ai.azure.com` and sign in with
    your Azure subscription account.

> ![](./media/image131.png)

2.  Click on **New project.**

![](./media/image132.png)

3.  Enter the unique project name(`cbsbaoai-proj`) and then click on
    Create a new hub link on the Hub drop down link as shown in below
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

6.  From left navigation menu, click on **Chat** under **Playground**
    .In Setup ,select **Add your data** and then click on **Add a new
    data source**.

![](./media/image137.png)

7.  Select **Azure AI Search** as **Data source** and then click
    **Next**.

![](./media/image138.png)

8.  Select your **Azure AI Search** service and the Index your
    **customer-index**,then click Next.

> ![](./media/image139.png)

9.  Keep the default values, click Next.

![](./media/image140.png)

10. Click on **Create** now.

![](./media/image141.png)

![](./media/image142.png)

11. Enter below prompt in Type here query text bod and press send
    button.

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

### Task 13 : Access and Explore the Chatapp.

1.  Go back Azure Portal Home page. Search for `App Services and
    select it from drop down as shown in the below image.

![](./media/image150.png)

2.  Click on App name.

![](./media/image151.png)

3.  Expand **Settings** and select **Environmental variables**. Search
    for **Azure AI Search** and make sure all the variable are updated
    correctly. Click on **Azure_SEARCH_KEY.**

> ![](./media/image152.png)

4.  Get the key from your Setup Azure AI Search service task ( REsoruce
    group- > Azure AI search service- > Settings- > Keys -> Key 1),
    enter the key in Value field and then click on Apply.

![](./media/image153.png)

5.  Click on **Add** now to add AML model endpoint value.

![](./media/image154.png)

6.  Go back to AML Studio tab -> Assets -> Endpoints -> finance-service. Copy the REST endpoint value.

![](./media/image155.png)

![](./media/image156.png)

7.  Switch back App service tab, Enter below values and then click on
    **Apply**.

    - Name : `AML_ENDPOINT`

    - Value : Your AML REST endpoint value.

![](./media/image157.png)

8.  Click on **Apply** and **confirm** changes.

![](./media/image158.png)

9.  Select **API->CORS** and select

![](./media/image159.png)

10. From the collapsible left menu under **Settings**,
    select **Authentication**. **Delete** the existing Identity provider
    and confirm deletion.

![](./media/image160.png)

11. Click on **Add identity provider**.

![](./media/image161.png)

12. Select Microsoft as Identity provider, update Name and select Client
    secret expiration -90 days and then click **Next:Permissions**.

![](./media/image162.png)

13. Click on Add permission. Select **Application** ->
    Application.ReadWrite.All and then click on **Update permission.**

![](./media/image163.png)

14. Click on **Add** now.

> ![](./media/image164.png)

9.  Click on **Overview** and click on **Restart**. Confirm restart by
    clicking on **Yes**.

![](./media/image165.png)

10. Click on **Overview** and then click **on Default domain**.

> ![](./media/image166.png)

11. App opens in new tab, Click on **Accept** to allow permissions.

![](./media/image167.png)

12. App opens,enter below prompts and explore it.

`List high value customers`

`give customer details whose mortgage is not 0`

![](./media/image168.png)

![](./media/image169.png)
