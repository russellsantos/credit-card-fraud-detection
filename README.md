# Credit Card Fraud Detection 
Portfolio project on developing, deploying and monitoring a a creditcard fraud monitoring service

## Problem Statement 

Credit Card fraud happens when unauthorized users gain access to a person's credit card details for the purpose of charging purchases to the account, or removing funds from it.  This project creates a fraud detection service that can be for each transaction, and will return a fraud score based on how likely the transaction is to be fraud. The fraud detection will be based on a machine learning mdoel that was trained on the [Credit Card Fraud Detection dataset on Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) provided by the [Machine Learning Group of ULB](https://mlg.ulb.ac.be/)

## Dataset

The dataset is based on credit card transactions made by European cardholders in September 2013. The data is two days worth of transactions, counting up to a total of 284,807 rows, with 31 columns. Of the approximately 200K transactions only 492 are marked as fraud. So we have a highly unbalanced dataset.

Also, to protect the data of the original cardholders, PCA was done on the original dataset, and only the featuers transformed using the principal components are used, with only time and amount being features that were not transformed. Here's a full list of the columns:

  - `Time` - this is an integer that represents the number of seconds elapsed between this transaction and the first transaction in the dataset.
  - `V1`, `V2` .... `V28` - these are 28 decimal values that represents the transformed features of the transaction using the principal components.
  - `Amount` - a decimal value that represents the transaction amount. This value is non-negative.
  - `Class` - this is the label of the transction. A `0` means it a legitimate tranasction, and a `1` means that it is a fraudulent tranasction.

## Approach

The purpose of this project is to create a basic fraud detection service that can be called during a tranasction, and will return a fraud score based on how likely it is that the transaction is fraudulent. Note that we are purposefully returning just a score - we are leaving it up to the caller to decide on the threshold to use. This will allow for flexibility, as the caller can use can use different thresholds for different contexts. This will also allow the caller to change the threshold without having to re-deploy the service.

For this project, we will be focusing mostly on creating a model pipeline and deploying it as a service. Thus we will be starting with a very basic model - we will not be optimizing it too much. However we will be at the very least include hyper parameter tuning as part of the model training pipeline.

We will strucuture this project as follows

```bash
├── fraud_detection_service
├── model_monitoring_pipeline
└── model_training_pipeline
```

  - `model_training_pipeline` will contain code that will train the model and publish it to an MLflow server. We will be starting with a very basic model using Random Forest, and we'll do some hyperparameter tuning. Model metrics will be stored using MLFlow tracking.
  - `fraud_detection_service` will contain the REST API. While I believe it would probably be best to use a streaming web service instead of a REST API, that is beyond my current skillsets at the moment. That can be a future improvement for this project. 
  - `model_monitoring_pipeline` will contain code that will do model monitoring. We will be using EvidentlyAI to help monitor this model.

## Usage
  < in progress >

