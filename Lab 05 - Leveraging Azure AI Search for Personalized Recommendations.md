### **Lab 05 -Leveraging Azure AI Search for Personalized Recommendations**

Contoso Bank is undergoing a comprehensive digital transformation across
all its departments to enhance their operational efficiency and customer
engagement. Currently, the bank's customer base is predominantly.
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

"As part of a POC, Contoso Bank's marketing team would like to work with the Data Analytics and AI engineering teams who can help them build an app that uses data-driven AI-enhanced strategies to improve campaign targeting, so the marketing team can aim for a double-digit conversion rate of the asset customer base within the same budget.
In this lab, you will work on behalf of Contoso Bank's AI engineering team to build this app, which makes use of Azure AI, AML, and MLOps to achieve the solution."

**At the end of this lab you will know how-to:**

- Use Azure AI Search Services to enrich the chatbot with search
- use Azure AI Bot Service for customer engagement using a chatbot



# Leveraging Azure AI Search for Personalized Recommendations

>**Introduction:** In this task, we will leverage Azure AI Search to power personalized recommendations for customers. Azure AI Search allows us to index and analyze customer data, enabling us to recommend relevant loan products based on individual customer preferences and behaviors. We will integrate this search functionality with Contoso Bank’s existing systems to ensure seamless data flow and accurate recommendations.


### **Task 1: Access and Explore the Chatapp.**

In this task, we explore the chat-app

1.  Go back Azure Portal Home page. Search for `App Services' and select it from the drop-down as shown in the below image.

    ![](./media/image150.png)

2.  Click on the App name.

    ![](./media/image151.png)

3.  Expand **Settings** and select **Environmental variables**. Search for **Azure AI Search** and make sure all the variables are updated
    correctly. Click on **Azure_SEARCH_KEY.**

    ![](./media/image152.png)

4.  Get the key from your Setup Azure AI Search service task ( Resource group- > Azure AI search service- > Settings- > Keys -> Key 1),
    enter the key in the Value field and then click on Apply.

    ![](./media/image153.png)

5.  Click on **Add** now to add the AML model endpoint value.

    ![](./media/image154.png)

6.  Go back to AML Studio tab -> Assets -> Endpoints -> finance-service. Copy the REST endpoint value.

    ![](./media/image155.png)

    ![](./media/image156.png)

7.  Switch back to the App service tab, Enter the below values, and then click on  **Apply**.

    - Name: `AML_ENDPOINT`

    - Value: Your AML REST endpoint value.

    ![](./media/image157.png)

8.  Click on **Apply** and **confirm** changes.

    ![](./media/image158.png)

9.  Select **API->CORS** and select

    ![](./media/image159.png)

10. From the collapsible left menu under **Settings**, select **Authentication**. **Delete** the existing Identity provider
    and confirm the deletion.

    ![](./media/image160.png)

11. Click on **Add identity provider**.

    ![](./media/image161.png)

12. Select Microsoft as the Identity provider, update Name select Client secret expiration -90 days and then click **Next: Permissions**.

    ![](./media/image162.png)

13. Click on Add permission. Select **Application** -> Application.ReadWrite.All and then click on **Update permission.**

    ![](./media/image163.png)

14. Click on **Add** now.

    ![](./media/image164.png)

15.  Click on **Overview** and click on **Restart**. Confirm restart by clicking on **Yes**.

    ![](./media/image165.png)

10. Click on **Overview** and then click **on Default domain**.

    ![](./media/image166.png)

11. The app opens in a new tab, Click on **Accept** to allow permissions.

    ![](./media/image167.png)

12. The app opens, enter the below prompts and explore it.

    `List high-value customers`

    `give customer details whose mortgage is not 0`

    ![](./media/image168.png)

    ![](./media/image169.png)
