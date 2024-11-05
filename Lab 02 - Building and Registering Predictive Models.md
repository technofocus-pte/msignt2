### **Lab 02 - Building and Registering Predictive Models**

**At the end of this lab you will know how-to:**

- Registering datasets for model training 
- Build and register a Machine learning model using Azure machine Learning Studio


#### **Introduction:**
In this lab, we will focus on registering datasets ,building and training machine learning models that predict borrower behavior. Using Azure Machine Learning, we will develop models that analyze historical customer data to forecast potential borrowers’ likelihood of loan conversion. After building the models, we will register them within the Azure ML workspace for further deployment and monitoring. This task emphasizes the importance of creating accurate and scalable models that drive personalized marketing.


### **Task 1 : Register Datasets**

 In this task, we will now register the datasets containing customer data with AML, so we can train the model based on this data. 

1.  Switch back to AML studio tab ( open new tab -> Azure Portal-> Resource group -> AML resource -> Launch Azure Machine learn
    studio), Under **Asset** , click on **Data** from left navigation menu and then click on **Data assets-> Create.**

    ![](./media/image42.png)

2.  Enter the name as : `Dataset1` and select Type : **Tabular** and then click on **Next**.

    ![](./media/image43.png)

3.  On this page, notice that there are several options to choose a source for your dataset including, Azure storage, SQL databases, web files, local files and event Azure Open Datasets. We will choose the Local files as our source in this lab. Select **From local files** and then click **Next**

    ![](./media/image44.png)

4.  On this page, you can see two Datastore types.You can create new datastore from this page .We are selecting Datastore type **as Azure Blob storage** for our lab and select the default blob storage( you can check in Data-\> Datastore) and click
    on **Next**.

    ![](./media/image45.png)

5.  On this page, you have options to upload files or folder but we choose files to upload for this lab.Click on **Upload files or folder** drop down and select **Upload files.**

    ![](./media/image46.png)

6.  Browse to **C:\Labfiles\Data** folder and select **Dataset1.CSV** and
    then click on **Open**.

    ![](./media/image47.png)

7.  Click **Next** now.

    ![](./media/image48.png)

8.  Review the dataset that was imported from the CSV you uploaded in the last step. Then click Next.

    ![](./media/image49.png)

9.  Click **Next** now.

    ![](./media/image50.png)

10. Review the details and then click on **Create**.

    ![](./media/image51.png)

    ![](./media/image52.png)

11. Repeat the above steps and register Dataset2.CSV with the name `Dataset2` also.

    ![](./media/image53.png)

### **Task 2 : Access Notebook to train a model with the AML studio**

In this task,we learn how to access the python SDK notebook from AML

1.  'On AML Studio home page,click on **Compute -> Computer instance.** Select **Compute instance** name and then click under **Application** and select
    **Terminal.**

    ![](./media/image54.png)

2.  Close the pop up window.

    ![](./media/image55.png)

3. In the terminal, install the Python SDK on the compute instance by running the following commands in the terminal:

    `pip install azure-ai-ml`

    >Note : Ignore any (error) messages that say that the packages couldn't be found and uninstalled.

    ![](./media/image56.png)

4. Run the following command to clone a Git repository containing a notebook, data, and other files to your workspace:

    `git clone https://github.com/technofocus-pte/MLOps-Driven-Chatbot-with-Azure-AI-AML-and-Azure-AI-Search-Integration.git`

    ![](./media/image57.png)

5. When the command has completed, in the **Files** pane, click **↻** to refresh the view and verify that a
    new **Users/*your-user-name*/MLops…** folder has been created.

    ![](./media/image58.png)

6. Stay in the same page to continue with the next lab.

>#### **Summary:** We have successfully registered data sets, built and registered predictive models that analyze borrower behavior. These models are now stored in the Azure Machine Learning registry, ready for further deployment and continuous monitoring. With this task completed, Contoso Bank can begin using these models to drive more targeted marketing efforts and improve borrower conversion rates.