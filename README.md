# Operationalinzing a Machine Learning pipeline:
The goal of the project is to train a AutoML model and deploy the best model following  best practices to followed in a production environment. Also create and publish a pipeline for this model enabling CI/CD functionalities.

**P.S**: Please have a look at demo video provided at the end for a shorter version.

## Architectural Diagram:
The below diagram gives an overview of all the steps followed for this project.
![architecture_dia drawio](https://user-images.githubusercontent.com/63422900/152593514-3f8ab5cb-4862-425e-b534-b6028e89af0d.png)

## Key Steps(Includes commands & screenshots for major steps followed in the project):
### Step 1: Upload data and train a AutoML model in AzureML
**1.1**: Registered dataset
![registered_dataset](https://user-images.githubusercontent.com/63422900/152594050-d88d5d95-0b3c-41e4-a30a-8ef033241e37.png)

**1.2**: Trained AutoML model from the data
![completed auto ml](https://user-images.githubusercontent.com/63422900/152594140-d1612602-851c-444d-a2f4-3389975dd663.png)

**1.3**: The best model got from the AutoML run which was voting Ensemble having a best AUC of 0.94
![best_model](https://user-images.githubusercontent.com/63422900/152594186-2cc6db6a-541c-45fb-ba94-5c7879bd9e01.png)

### Step 2: Deploying the best model
**2.1**: Deployed the best model enabling authentication
![deployed_model1](https://user-images.githubusercontent.com/63422900/152594843-1c9c2b17-e907-417e-b781-9dc4b6b2ef94.png)

**2.2**: Enabling application insights and logging mechanism for the the endpoint. Using the logs.py script. 
![logs](https://user-images.githubusercontent.com/63422900/152595320-1cb531dc-af65-4516-93a8-b9c953cb1f11.png)

**2.3**: Applications insights showing various statistics such as server load and number of requests at a given point of time for the serve. Can be accessed by using "application insights" link present in the deployed model.
![application_insights](https://user-images.githubusercontent.com/63422900/152595666-a2d00ead-6b51-460e-b40e-6bf7d0d9c40a.png)

### Step 3: Using Swagger for documenting the model parameters
Using swggaer.json provided for deployed model in AzureML. Used docker container for swagger and in local machine and viewed swagger model paramters both input as well as output in swagger.

![swagger1](https://user-images.githubusercontent.com/63422900/152595795-7fef96ff-4cfe-4349-811e-ae4a465cff62.png)


![swagger2](https://user-images.githubusercontent.com/63422900/152595802-8a2d0f53-4c50-4b0a-b086-03f25bb2ec4f.png)


### Step 4: Testing the model endpoint and benchmarking results:
**4.1**: Used endpoints.py (which takes authentication key and endpiont as input) , using 2 sample datapoints , gave a post request to get back model results
![result](https://user-images.githubusercontent.com/63422900/152597149-2235f289-d9bd-4ea3-85c8-0fdc0304cd5c.png)

**4.2**: Used apache benchmark to get endpoint benchmark statistics such a mean time for response. Benchmark results for 10 results. Used the below command.
ab -n 10 -v 4 -p data.json -T 'application/json' -H 'Authorization: Bearer SECRET' 'REST_ENDPOINT_URL'

![benchmark](https://user-images.githubusercontent.com/63422900/152597298-969ce494-002c-44b6-a729-1600706081f4.png)

### Step 5: Creating and publishing a AzureML pipeline for the best model
The main objective for creating a machine learning pipeline to enable CI/CD functionalities which makes it easier to handle any changes in a production environment. Once such example would be using the pipeline for continious retraining of the model and easily deploying it production. Here a pipeline is created for the ML model and is published so that it can be consumed from anywhere

**5.1**: Pipeline creation in AzureML and its completed run 
![completed_pipeline_run](https://user-images.githubusercontent.com/63422900/152599388-bd0a5b0e-0e78-4594-a19a-0358444ae172.png)

**5.2**: The scheduled run of the AutoML model
![experiment_overview_azureml](https://user-images.githubusercontent.com/63422900/152599566-16323967-1ad9-4dc2-a08b-446bfc5c9e5d.png)

**5.3**: Published pipeline with the endpoint
*TODO![completed_pipeline_run](https://user-images.githubusercontent.com/63422900/152599469-5ce7fafe-4d80-498f-a541-a25c2e9b8f75.png)

**5.4**: Published pipeline overview with active status
![pipeline_active](https://user-images.githubusercontent.com/63422900/152599660-712e6623-9f9e-4574-9a1b-f85bb5b9db2b.png)

**5.5**: Run widget details output after the pipeline is created and published 
![run_widgets](https://user-images.githubusercontent.com/63422900/152599930-c518abda-1bac-46e5-bd2e-c00a5a528352.png)


## Video demo of the project

https://user-images.githubusercontent.com/63422900/152592189-cc6e8e3a-3937-418b-9d95-6fd98faf2fc1.mp4



## Future Enhancements 

1. Experiment with deep learning models such a MLP's to try and boost the AUC score.
2. Create a frontend UI for easier consumption of the the model.
3. Include functionality to montor data drift and model drift in the published pipeline.

