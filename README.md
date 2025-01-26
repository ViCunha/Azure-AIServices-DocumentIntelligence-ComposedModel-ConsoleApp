
### Overview
---
In this exercise, two custom models will be created and trained to analyze different tax forms. A composed model, which includes both custom models, will then be created. The model will be tested by submitting a form to verify that it recognizes the document type and labeled fields correctly
   
### Key Aspects
---
- Azure Portal
  - Valid subscription

### Environments
---
- Azure Portal
- Azure AI Document Intelligence Studio

### Diagrams
---
![image](https://github.com/user-attachments/assets/152ba4d8-8c36-4a17-8dc4-b6d47837b5be)


### Actions
---
Prepare the environment

[ Run Cloud Shell ]

- In the Azure portal, select the [>_] (Cloud Shell) button at the top of the page to the right of the search box. This opens a Cloud Shell pane at the bottom of the portal.

- The first time you open the Cloud Shell, you might be prompted to choose the type of shell you want to use (Bash or PowerShell). Select Bash. If you don't see this option, skip the step.

- If you're prompted to create storage for your Cloud Shell, ensure your subscription is specified and select Create storage. Then wait a minute or so for the storage to be created

- Make sure the type of shell indicated on the top left of the Cloud Shell pane is switched to Bash. If it is PowerShell, switch to Bash by using the drop-down menu

- Wait for Bash to start.

[ Set up resources ]

- In the Cloud Shell, to clone the code repository, enter this command:

```
rm -r doc-intelligence -f
git clone https://github.com/MicrosoftLearning/mslearn-ai-document-intelligence doc-intelligence
```

- Change the 03-composed-model directory and then execute the setup script:

```
cd doc-intelligence/Labfiles/03-composed-model/
bash setup.sh
```

[ Create the 1040 Forms custom model ]

- In a new browser tab, start the Azure AI Document Intelligence Studio.

- Scroll down, and then under Custom model, select Custom model

- If you're asked to sign into your account, use your Azure credentials.

- If you're asked which Azure AI Document Intelligence resource to use, select the subscription and resource name you used when you created the Azure AI Document Intelligence resource.

- Under My Projects, select + Create a project

- On the Configure service resource page, in the Subscription drop-down list, select your Azure subscription.

- In the Resource group drop-down list, select DocumentIntelligenceResources.

- In the Azure AI Document Intelligence or Azure AI Service Resource drop-down list, select DocumentIntelligence

- In the API version drop-down list, ensure that 2022-06-30-preview is selected and then select Continue.

- On the Configure training data source page, in the Subscription drop-down list, select your Azure subscription

- In the Resource group drop-down list, select DocumentIntelligenceResources.

- In the Storage account drop-down list, select the only storage account listed.

- In the Blob container drop-down list, select 1040examples, and then select Continue.

- In the Review and create page, select Create project.

[ Label the 1040 Forms custom model ]

- In the Label data page, in the top-right of the page, select +, and then select Field

- Type FirstName and then press Enter

- In the document, select John and then select FirstName.

- In the top-right of the page, select +, and then select Field.

- Type LastName and then press Enter

- In the document, select Doe and then select LastName

- In the top-right of the page, select +, and then select Field.

- Type City and then press Enter

- In the document, select Los Angeles and then select City

- In the top-right of the page, select +, and then select Field

[ Train the 1040 Forms custom model ]

In the Azure AI Document Intelligence Studio, select Train

In the Train a new model dialog, in the Model ID textbox, type 1040FormsModel.

In the Build mode drop-down list, select Template, and then select Train

In the Training in progress dialog, select Go to Models

[ Create the 1099 Forms custom model ]

- In Azure AI Document Intelligence Studio, select Custom model.

- Under My Projects, select + Create a project

- In the Project name textbox, type 1099 Forms, and then select Continue.

- On the Configure service resource page, in the Subscription drop-down list, select your Azure subscription.

- In the Resource group drop-down list, select DocumentIntelligenceResources.

- In the Azure AI Document Intelligence or Azure AI Service Resource drop-down list, select DocumentIntelligence

- In the API version drop-down list, ensure that 2022-06-30-preview is selected and then select Continue.

- On the Configure training data source page, in the Subscription drop-down list, select your Azure subscription

- In the Resource group drop-down list, select DocumentIntelligenceResources.

- In the Storage account drop-down list, select the only storage account listed.

- In the Blob container drop-down list, select 1099examples, and then select Continue.

- In the Review and create page, select Create project

[ Label the 1099 Forms custom model ]

- In the Label data page, in the top-right of the page, select +, and then select Field.

- Type FirstName and then press Enter.

- In the document, select John and then select FirstName

- In the top-right of the page, select +, and then select Field

- Type LastName and then press Enter

- In the document, select Doe and then select LastName.

- In the top-right of the page, select +, and then select Field

- Type City and then press Enter

- In the document, select New Haven and then select City.

- In the top-right of the page, select +, and then select Field.

- Type State and then press Enter

- In the document, select CT and then select State

- Repeat the labeling process for the remaining forms in the list on the left. Label the same four fields: FirstName, LastName, City, and State

[ Train the 1099 Forms custom model ]

- In the Azure AI Document Intelligence Studio, select Train.

- In the Train a new model dialog, in the Model ID textbox, type 1099FormsModel

- In the Build mode drop-down list, select Template, and then select Train.

- In the Training in progress dialog, select Go to Models.

- The training process can take a few minutes. Refresh the browser occasionally until both models display the succeeded status.

---

Create and assemble a composed model
In the Azure AI Document Intelligence Models page, select both 1040FormsModel and 1099FormsModel.

[ Create a Custom Classification Model ]

- Select Training Data: Choose a diverse set of documents representing different types (e.g., 1040 and 1099 tax forms).

- Label the Data: Assign labels to the training data indicating the document type.

- Train the Model: Use the labeled data to train a custom classification model that can accurately distinguish between the different document types.

- In the Compose a new model dialog, in the Model ID textbox, type TaxFormsModel and then select Compose. Azure AI Document Intelligence creates the composed model and displays it in the list of custom models:

---

Use the composed model

- In the Azure portal, select All resources and then select the formsrecstorage<xxxxx> storage account, where <xxxxx> is a random number.

- Under Data storage select Containers and then select TestDoc

- To the right of f1040_7.pdf, select ... and then select Download.

- Save the PDF document to your local computer and make a note of the saved location.

- In the Azure AI Document Intelligence Studio, select Custom Classification Model

- Click on “Create a project” 

- Define the required fields (define new folder to the Custom Classification Model

- Click on the “Create” button

- After the Custom Classification Model was create, in the Azure AI Document Intelligence Studio, select Custom Extraction Model

- In the project, on Models select the models that will be part of the composed model

- Click on the “Compose” button
  - Define the name
  - Select the Classification Model (Custom Classification Model)

- Select and configure the custom models

- Click on the “Compose” button

- Click on the “Test” side menu item

- Select f1040_7.pdf, and then select Open.

- Select Analyze. Azure AI Document Intelligence analyses the form by using the composed model

---

Clean up resources

- In the “search resources, services, and doc”, type and select Resource Groups

- Click on the resource group created

- Select Delete resource group and follow the directions to delete the resource group and all of the resources it contains

---

The exercise is not fully compatible with the current UI and features 
(example: the indicated API version is 2022-06-30 and the custom classification model is not described)

### Media
---
![image](https://github.com/user-attachments/assets/94b6dae3-ce7d-4acd-84e2-cb0c45d7572f)
---
![image](https://github.com/user-attachments/assets/b11d7d27-f411-4a23-b7f4-713242ca39ef)
---
![image](https://github.com/user-attachments/assets/d995e6fe-fe02-4069-be91-e339a5b86ff1)
---
![image](https://github.com/user-attachments/assets/0ae1c2c6-c4d7-487d-b191-c85d677fb634)
---
![image](https://github.com/user-attachments/assets/0235b3dd-d0cd-4178-9c5c-00b3b14ce8f0)
---
![image](https://github.com/user-attachments/assets/c5902c6c-0747-4e15-be30-f793958e1c4f)
---
![image](https://github.com/user-attachments/assets/839611bf-4f0e-4892-96de-4f5f85fb2288)
---
![image](https://github.com/user-attachments/assets/b8350ba1-bf8b-4f0c-b464-a75fab3b89ee)
---
![image](https://github.com/user-attachments/assets/b38bb449-815c-4940-9baa-f1d473eabfba)
---
![image](https://github.com/user-attachments/assets/875a7a57-594c-4ea0-943e-a2e68c0046e6)
---
![image](https://github.com/user-attachments/assets/215bb875-78f4-4990-b1e6-71edab422efb)
---
![image](https://github.com/user-attachments/assets/d30b202c-5fc8-4c2a-b542-36e6390c4486)
---
![image](https://github.com/user-attachments/assets/666f4699-1c3f-4a42-99f4-01c181a7e1f7)



### References
---

- https://learn.microsoft.com/en-us/training/modules/create-composed-form-recognizer-model/4-exercise-model

- https://github.com/MicrosoftLearning/mslearn-ai-document-intelligence
