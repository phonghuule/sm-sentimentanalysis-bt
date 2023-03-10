# Creating a multi-label classification model on SageMaker using BlazingText Algorithm

This lab is provided as part of **[AWS Innovate Data And AI/ML Edition](https://aws.amazon.com/events/aws-innovate/apj/aiml-data/)**.

:information_source:
 You will run this lab in your own AWS account. Please follow directions
 at the end of the lab to remove resources to avoid future costs.

 ## Content
 1. [Introduction](#introduction)
 2. [Sentiment Analysis](#sentiment-analysis)
 3. [SageMaker Studio](#sagemaker-studio)
 4. [Setup](#setup)
 5. [SageMaker Studio UI Overview](#sagemaker-studio-ui-overview)
 6. [JupyterLab Notebook](#jupyterlab-notebook)
 7. [Conclusion](#conclusion)
 8. [Cleanup](#cleanup)
 9. [Survey](#survey)

### Introduction

Amazon SageMaker is a fully managed service that removes the heavy lifting from each step of the machine learning workflow, and provides every developer and data scientist with the ability to build, train, and deploy machine learning (ML) models quickly.
The Amazon SageMaker BlazingText algorithm provides highly optimized implementations of the Word2vec and text classification algorithms. The Word2vec algorithm is useful for many downstream natural language processing (NLP) tasks, such as sentiment analysis, named entity recognition, machine translation, etc. Text classification is an important task for applications that perform web searches, information retrieval, ranking, and document classification.
Learn more about Amazon BlazingText algorithm [here](https://docs.aws.amazon.com/sagemaker/latest/dg/blazingtext.html).

### Sentiment Analysis
Sentiment Analysis is an application of NLP. Teaching a machine to analyse a sentiment is a classification problem. 
Here the ML model undergoes a supervised learning where the input data has features that teach the model to predict the label(e.g. Positive, Negative, Neutral).

There are various use cases of Sentiment Analysis wherein businesses can gather the public sentiment on a product that was released recently.

###  SageMaker Studio
In this lab, we will be using the SageMaker Studio. Amazon SageMaker Studio provides a single, web-based visual interface where you can perform all ML development steps. SageMaker Studio gives you complete access, control, and visibility into each step required to build, train, and deploy models.

All ML development activities including notebooks, experiment management, automatic model creation, debugging, and model and data drift detection can be performed within SageMaker Studio.

To know more. See [here](https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html).

###  Setup

1. Navigate to the [Amazon SageMaker](https://console.aws.amazon.com/sagemaker/home) service in the AWS console.
    ![](images/searchsagemaker.png)
2. The SageMaker console is displayed as below. Click on the SageMaker Studio button. Before using the SageMaker studio, we will first need a SageMaker Domain. If you have a SageMaker Domain created already, you could use the same. Else a SageMaker domain will have to be created.
    ![](images/smconsole.png)
3. To create a new SageMaker Domain enter a Name ``aiml-innovate-2023`` in the **Name** section, 
``data-scientist-1`` in the **User Profile** section and then **Create a new role**.
    ![](images/createdomain.png)
4. For this lab, we will allow the new execution role access to **Any S3 bucket**. Once selected, click on Create Role.
    ![](images/createsmrole.png)
5. Once back on the **Create Domain** page, Click on **Submit** button to create the Domain. The domain creation takes a few minutes.
    ![](images/hitsubmitsmdomain.png)
6. Once the domain is created, Click on the **Launch Studio** to Launch the SageMaker Studio. This takes a couple of minutes before the IDE is launched.
    ![](images/launchstudio.png)

### SageMaker Studio UI Overview

The SageMaker Studio UI has a few sections. To explore further, click on the below links:
* [Left Sidebar](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-ui.html#studio-ui-nav-bar)
* [File and resource browser](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-ui.html#studio-ui-browser)
* [Main work area](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-ui.html#studio-ui-work)
* [Settings](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-ui.html#studio-ui-prefs)

### JupyterLab Notebook

1. On SageMaker Studio, click on **Git** option on the **Left Sidebar**. Then click on the **Clone a Repository**.
    ![](images/clonerepo-smstudio.png)
2. Enter the git repo URL as ``https://github.com/phonghuule/sm-sentimentanalysis-bt.git`` and Click on **Clone**.
3. Click on the **File Browser** option on the **Left Sidebar**. Open the ``sentiment-analysis-blazingText.ipynb`` at the location ``sm-sentimentanalysis-bt/notebook``.
    ![](images/notebooklocation.png)
4. Select **Image** as ``Data Science``, **Kernel** as ``Python 3``, **Instance Type** as ``ml.t3.medium`` and click on **Select**.
    ![](images/selectkernel.png)
5. Run all cells as per instructions in the notebook.

### Conclusion
In this lab we 
- Used trained a machine learning learning model to perform a multi-label text classification using Supervised training. 
- understood the nuances of the Input/Output interfaces to the BlazingText algorithm
- deployed the ML model using SageMaker Hosting services and invoked the Endpoint to understand the sentiment of the sentences.

#### Input

```
sentences = [
    "I love this product. I would order it again",
    "I am not sure if I like this product. I probably do."
]
```
#### Output
```json
[
  {
    "label": [
      "__label__3"
    ],
    "prob": [
      0.9555298686027527
    ]
  },
  {
    "label": [
      "__label__2"
    ],
    "prob": [
      0.9004751443862915
    ]
  }
]
```

In the above example:<br/>
```I love this product. I would order it again``` evaluated to a ```__label__3``` or a **Positive** sentiment with a 95.55% probability<br/>
and <br/>
```I am not sure if I like this product. I probably do.``` evaluated to a ```__label__2``` or a **Neutral** sentiment with a 90.04% probability..

### Cleanup
Follow the steps below to perform a cleanup and prevent accumulating usage charges from this lab.
1. On the Left Sidebar, click on **Instances** and Shutdown the **Running Apps** as below.
    ![](images/shutdownrunningapps.png)
2. Then click **File > Shut Down** to shutdown the SageMaker Studio server and then click on **Shutdown All**. This will display **Server stopped** message.

    ![](images/shutdownsm.png)

    ![](images/shutdownall.png)

    ![](images/serverstopped.png)
3. After this, click on the domain ``aiml-innovate-2023``, user profile ``data-scienctist-1`` and then delete all apps. At this there should only be the ``default`` app remaining.    
    ![](images/delete-apps.png)
4.  After the apps have been deleted, click on **Edit** on the _Details_ section within the **User Details** screen.
    ![](images/userdetailsedit.png)
5. Then click on **Delete User** to delete the user ``data-scientist-1``. <br/>
**Note:** If there are other users please delete these to be able to delete the SageMaker Domain.
    ![](images/deleteuser.png)
6. Once back on the SageMaker Studio screen, click on **Delete Domain** to delete the domain created to host the SageMaker Studio.
    ![](images/deletedomain.png)
7. Navigate to **Amazon Sagemaker - Ineference - Endpoints** to delete Endpoint created.
    ![](images/deletedendpoint.png)
8. Navigate to **Amazon Sagemaker - Ineference - Endpoint configurations** to delete the configuration created.
    ![](images/deletedendpointconfig.png)
