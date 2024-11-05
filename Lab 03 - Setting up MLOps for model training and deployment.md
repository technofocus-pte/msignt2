### **Lab 03 - Setting up MLOps for model training and deployment using Python SDK**


**In this lab you will learn how-to:**

- Train a model and deploy it in AML using Python SDK


# Setting up MLOps for model training and deployment using Python SDK

>**Introduction:** :In this exercise, we will focus on implementing a streamlined approach to model deployment by utilizing a Python SDK notebook for model training and deployment, rather than automated MLOps pipelines. This hands-on approach allows us to register datasets, build, and deploy predictive models directly through the Azure Machine Learning environment without requiring Azure DevOps pipelines. This setup will enable Contoso Bank to initiate targeted marketing efforts using up-to-date borrower behavior models, which can further be updated manually as needed.

### **Task 1 : Run the notebook to Work with Data**

In this task,we will use python SDK to clean the data and train the model using the data

1.  While still in Azure ML Studio, Terminal for your deployed compute instance, expand **models** folder (created as a result of the previous exercise), and select the **ContosoBankAMLmodel.ipynb** notebook.

2.  Run the first cell to check the latest version of azure-ai-ml package.

    > Note: If the azure-ai-ml package is not installed, run **pip install azure-ai-ml** to install it

    ![](./media/image59.png)

    > Note : Select **Authenticate** and follow the necessary steps if a notification appears asking you to authenticate.

3.  Verify that the notebook uses the **Python 3.8 - AzureML** kernel.If its not using then select it from drop down.

    ![](./media/image60.png)

4.  Restart the kernel as shown in below image.

    ![](./media/image61.png)

5.  Click on **Restart**.

    ![](./media/image62.png)

6.  Read description of each cell under **connect to Workspace** section and run it

    ![](./media/image63.png)

7.  Run cell to **list the datastores** in storage account.

    ![](./media/image64.png)

8.  Run the cell to **clean , merge datasets and save** into **merge_data.CSV** file.

    ![](./media/image65.png)

    ![](./media/image66.png)

9. Run cell to preview merge_data.csv file. Then run all the remaining cells in this section.

    ![](./media/image67.png)

10.  Run cell to Describe the data after transposing

        ![](./media/image68.png)

11. Run all the cells and check merged_data to check number of rows.

    ![](./media/image69.png)

12. Run cell to show unique values in the LoadOnCard Column.

    ![](./media/image70.png)

13. Run cell to show distribution of data in LoanonCard column

    ![](./media/image71.png)

14. Read and run each cell under **Model Preparation** and explore.

    ![](./media/image72.png)

    ![](./media/image73.png)

    ![](./media/image74.png)

15. Read and run cell in **Apply Logistic Regression** section

    ![](./media/image75.png)

16. When we run a Python script as an experiment in Azure Machine Learning, a Conda environment is created to define the execution context for the script. Azure Machine Learning provides a default environment that includes many common packages; including the azureml-defaults package that contains the libraries necessary for working with an experiment run, as well as popular packages like pandas and numpy. Run cell in **Define an environment** section to define and register financial-experiment-env environment

    ![](./media/image76.png)

17. Next, run cell to **view registered environments**.

    ![](./media/image77.png)

18. Run all cells to **run an experiment on remote compute**.

    ![](./media/image78.png)

19. Run the experiment cell . wait for the experiment to complete . It
    takes **15-20 minutes.**. 

    ![](./media/image79.png)

    ![](./media/image80.png)

    ![](./media/image81.png)

20. Run each cell under **Deploy the model as a web service** section.

    ![](./media/image82.png)

21. Run the cell to provide web service endpoint under **Use the web service** section.

    ![](./media/image83.png)

21. Run all cells to predict Asset and liability Customers.

    ![](./media/image84.png)

>**Summary:** Using the Python SDK notebook, we have successfully trained and deployed predictive models for analyzing borrower behavior without relying on automated pipelines or DevOps. This approach allows Contoso Bank to manually update and deploy models as needed, enabling targeted marketing efforts with up-to-date insights into borrower behavior.
