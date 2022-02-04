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

**5.1**:

*TODO
* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Screen Recording


https://user-images.githubusercontent.com/63422900/152592189-cc6e8e3a-3937-418b-9d95-6fd98faf2fc1.mp4



## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.

