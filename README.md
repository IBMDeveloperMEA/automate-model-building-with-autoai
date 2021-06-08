# Automate Model Building with AutoAI

## WORKSHOP RESOURCES

- Login/Sign Up for IBM Cloud: https://ibm.biz/DeveloperSummit

With the aim of creating AI for AI, IBM introduced a service on Watson&trade; Studio called [AutoAI](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/wsj/analyze-data/autoai-overview.html).

AutoAI is a capability that automates machine learning tasks to ease the tasks of data scientists. It automatically prepares your data for modeling, chooses the best algorithm for your problem, and creates pipelines for the trained models, and it can be run in public clouds and in private clouds, including IBM Cloud Pak&reg; for Data.

## Learning objectives

This tutorial explains the benefits of the AutoAI service on a use case. This will give you a better understanding of how regression and classification problems can be handled without any code -- and how the tasks (feature engineering, model selection, hyperparameter tuning, etc.) are done with this service. This tutorial also includes details for choosing the best model among the pipelines and how to deploy and use these models via IBM Cloud Pak for Data platform.

## Prerequisites

* [Sign up](https://ibm.biz/DeveloperSummit)

## Estimated time

This tutorial should take approximately 20 minutes to complete (including the training in AutoAI) and is broken up into the following steps:

1. Create a project and AutoAI instance
2. Set up your AutoAI environment and generate pipelines
3. Save AutoAI model
4. Deploy and test the model

## Step 1. Create a project and AutoAI instance

### Create an IBM Cloud Pak for Data project

1. Using a browser, log into your ICP4D instance and click the hamburger (☰) menu in the upper-left corner and click **Projects**. From the Projects page, click **New Project +**.
![Create project](images/autoai-create-project.png)

1. Select **Analytics project** and  click **Next**.
![Create analytics project](images/autoai-create-analytics-project.png)

1. Select **Create an empty project**.
![Create empty project](images/autoai-create-empty-project.png)

1. Give your project a name and an optional description, then click **Create**.
![Name your project](images/autoai-name-project.png)

The data assets page opens and is where your project assets are stored and organized. By clicking the **Assets** bar, you can load your dataset from the interface on the right.

1. Download the [Telco-Customer-Churn.csv](static/Telco-Customer-Churn.csv) dataset.

1. Upload the dataset to the analytics project by clicking on **Browse** and selecting the downloaded file.
![Upload dataset](images/autoai-upload-data-set.png)

## Step 2. Set up your AutoAI environment and generate pipelines

1. To start the AutoAI experience, click **Add to Project +** from the top and select **AutoAI experiment**.
![Add a project](images/autoai-add-project.png)

1. Name your AutoAI experiment asset and leave the default compute configuration option listed in the drop-down menu, then click **Create**.
![Name your services](images/autoai-name-services.png)

1. To configure the experiment, we must give it the dataset to use. Click on the **Select from project** option.
![Add dataset to AutoAI](images/autoai-select-file.png)

1. In the dialog, select the [Telco-Customer-Churn.csv](static/Telco-Customer-Churn.csv) dataset that was uploaded in the previous step, then click **Select asset**.

![Add dataset to AutoAI](images/autoai-select-file-select-asset.png)
1. Once the dataset is read in, we need to indicate what we want the model to predict. Under the Select prediction column, find and click on the **Churn** row. 

1. AutoAI will set up defaults values for the experiment based on the dataset. This includes the type of model to build, the metrics to optimize against, the test/train split, etc. You could view/change these values under Experiment settings. For now, we will accept the defaults and click the **Run experiment** button.
![Choose Churn column and run](images/autoai-choose-churn-and-run.png)

1. The AutoAI experiment will run and the UI will show progress as it happens.
![AutoAI progress](images/autoai-model-progress.png)

1. The UI will show progress as different algorithms/evaluators are selected and as different pipelines are created and evaluated. You can view the performance of the pipelines that have completed by expanding each pipeline section.

1. The experiment can take several minutes to run. Upon completion, you will see a message that the pipelines have been created.
![AutoAI pipelines created](images/autoai-pilelines-complete.png)

## Step 3. Save AutoAI model

The AutoAI process by default selects top-two performing algorithms for a given dataset. After executing the appropriate data pre-processing steps, it follows this sequence for each of the algorithms to build candidate pipelines:

* Automated model selection
* Hyperparameter optimization
* Automated feature engineering
* Hyperparameter optimization

You can review each pipeline and select to deploy the top performing pipeline from this experiment.

1. Scroll down to see the Pipeline leaderboard. The top-performing pipeline is in the first rank.

1. The next step is to select the model that gives the best result by looking at the metrics. In this case, Pipeline 4 gave the best result with the metric "Accuracy (optimized)". You can view the detailed results by clicking the corresponding pipeline from the leaderboard.
![Pipeline leaderboard](images/autoai-pipeline-leaderboard.png)

1. The model evaluation page will show metrics for the experiment, feature transformations performed (if any), which features contribute to the model, and more details of the pipeline.

![Model evaluation](images/autoai-model-evaluation.png)

1. To deploy this model, click on **Save as**, then **Model** to save it.

1. A window opens that asks for the model name, description (optional), etc. You can accept the defaults or give your model a meaningful name/description and then click **Save**.
![Save model name](images/autoai-save-model-name.png)

1. You receive a notification to indicate that your model is saved to your project. Go back to your project main page by clicking on the project name on the navigator on the top left.
![Model notification](images/autoai-model-notification.png)

You will see the new model under the Models section of the Assets page.

![Choose AI model](images/autoai-choose-asset-ai-model.png)

## Step 4. Deploy and test the model

1. Under the Models section of the Assets page, click the name of your saved model.

1. To make the model available to be deployed, we need to make it available in the deployment space. Click on **Promote to deployment space**.
![Deploy the model](images/autoai-deploy-model.png)

1. To promote an asset, the project must first be associated with a deployment space. Click **Associate Deployment Space**.
![Associate deployment space](images/autoai-associate-deployment-space.png)

1. You may have already created a deployment space. In that case, click on the **Existing** tab and choose that deployment, then click **Associate**.
![Associate existing deployment space](images/autoai-associate-existing-deployment-space.png)

1. If you do not have an existing deployment, go to the New tab, give a name for your deployment space, then click **Associate**.
![Create deployment space](images/autoai-create-deployment-space.png)

1. From the model page, once again click on **Promote to deployment space**, then click **Promote to space** in the dialog box that pops up to confirm.
![Promote to deployment space](images/autoai-promote-to-deployment-space.png)

1. This time you will see a notification that the model was promoted to the deployment space succesfully. Click **Deployment space** from this notification. You can also reach this page by using the hamburger (☰) menu and clicking **Analyze > Analytics deployments**.
![Deployment space](images/autoai-view-deployment.png)

1. If you came in through the **Menu > Analyze > Analytics deployments** path, click on your deployment space.
![Click deployment space](images/autoai-click-deployment-space.png)

1. Under the Assets tab, click on the AutoAI model you just promoted.
![Click model in deployment space](images/autoai-deployment-space-choose-model.png)

1. Click **Create deployment** in the top-right corner.
![Click deploy button](images/autoai-click-deploy.png)

1. On the Create a deployment screen, choose **Online** for the deployment type, give the deployment a name and an optional description, then click **Create**.
![Create deployment](images/autoai-name-and-create-deployment.png)

1. The deployment will show as "In progress" and switch to "Deployed" when done.
![Click final deployment](images/autoai-deployed.png)

### Testing the deployed model with the GUI tool

IBM Cloud Pak for Data offers tools to quickly test out Watson machine learning models. We begin with the built-in tooling.

1. Click on the deployment. The deployment API reference tab shows how to use the model using Curl, Java, JavaScript, Python, and Scala. Click on the corresponding tabs to get the code snippet in the language you want to use.
![Deployment API reference](images/autoai-api-reference-curl.png)

1. To get to the built-in test tool, click the **Test** tab, then click on the **Provide input data as JSON** icon and paste the following data under Body:

```
json
   {
   "input_data":[
      {
         "fields":[ "customerID", "gender", "SeniorCitizen", "Partner", "Dependents", "tenure", "PhoneService", "MultipleLines", "InternetService", "OnlineSecurity", "OnlineBackup", "DeviceProtection", "TechSupport", "StreamingTV", "StreamingMovies", "Contract", "PaperlessBilling", "PaymentMethod", "MonthlyCharges", "TotalCharges"],
         "values":[[ "7567-VHVEG", "Female", 0, "No", "No", 1, "No", "No phone service", "DSL", "No", "No", "No", "No", "No", "No", "Month-to-month", "No", "Bank transfer (automatic)", 25.25, 25.25]]
      }
   ]
}
```

1. Click the **Predict** button and the model will be called with the input data. The results will display in the Result window. Scroll down to the bottom of the result to see the prediction ("Yes" or a "No" for Churn).
![Test deployment with JSON](images/autoai-test-json.png)

1. Alternatively, you can click the **Provide input using form** icon and input the various fields, then click **Predict**.
![Input to the fields](images/autoai-input-fields.png)



## Summary

This tutorial explained the benefits of the AutoAI service on a Telco use case so you can have a better understanding of how regression and classification problems can be handled without any code and how the tasks (feature engineering, model selection, hyperparameter tuning, etc.) are done with this service. The tutorial also included details for choosing the best model among the pipelines and how to deploy and use these models via IBM Cloud Pak for Data platform.

Want to find out more about AutoAI? Then, take a look at [Simplify your AI lifecycle with AutoAI](https://developer.ibm.com/technologies/artificial-intelligence/series/explore-autoai/).
