# Building-a-CI-CD-Pipline

[![Python application test with Github Actions](https://github.com/AnalyticNaveen/Building-a-CI-CD-Pipline/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/AnalyticNaveen/Building-a-CI-CD-Pipline/actions/workflows/main.yml)

## Overview
In this project we have setup a CI/CD pipeline for a python based Machine Learning application which predicts housing prices in the city of Boston.

for Continuous Integration we have used GitHub as source control management service and its GitHub Actions service to perform linting and unit testing to ensure the software is in a usable state.

for Continuous Delivery/Deployment we have used Azure pipeline to deploy the latest changes to the software into production.

Any commits/merges to the master branch of the repository "main" is considered to be a change that needs to deployed. As a result of this action, GitHub actions and Azure Pipeline is triggered.

## Project Plan
This project was carried out using Agile methodologies and details of the planning can be view in the below artifacts:

A link to a Trello board for the project
A link to a spreadsheet that includes the original and final project plan

## Instructions
![azure_cicd_architecture](https://user-images.githubusercontent.com/104189782/191111747-1dc9a881-9a24-45ea-a478-658a367e47c3.png)


The process follow to develop this CICD pipeline is listed below . follow the steps to create the pipeline.


1. Create a repo for this project and Clone this repository into Azure Cloud Shell

![git clone with readme](https://user-images.githubusercontent.com/104189782/191113389-bd811b92-873b-4b8b-a885-0f82dfe3aca0.png)


create a new repo for the project . Generate a ssh key in copy the ssh from azure cloud shell using below commands
after copying add this ssh code in github repo and clone this repo in azure cloud shell.

```bash
ssh-keygen -t rsa
CAT /home/odl_user/.ssh/id_rsa.pub
```


2. Create a virtual environment and testing the demo codes.

create a virtual environment and select it using below command.

```bash
python3 -m venv ~/.flaskweb
source ~/.flaskweb/bin/acctivate
```

Create a requirements.txt file which contain the packages or libraries that we require 
Then Create Make file containing install , test , lint properties and run it. this will automatically install the dependency and test the codes.


```bash
pylint==2.15.0
pytest==7.1.3
```

```python

install:
	pip install  --upgrade pip &&\
		pip install -r requirements.txt

test:
	#python -m pytest -vv test_hello.py added 

lint:
	pylint --disable=R,C,W1203,bare-except --fail-under=6  app.py

all: install lint test

```
Run below command for testing

```
make all
```
if the test is passed it looks similar to below image 

![test paased](https://user-images.githubusercontent.com/104189782/191115398-4b0daef6-0f01-4e7d-aab7-c32e37286d8c.png)

3. Creating requirement.txt file for this project .

For building this project we have used below libraries 

```bash
pylint==2.15.0
pytest==7.1.3
Flask==2.2.2
pandas==0.24.2
scikit-learn==0.20.3
joblib==1.1.0
locust==2.12.0
```

4. Prediction.

Once all the libraries and dependencies are installed we can do our prediction for this we run below command 

```bash
./make_prediction.sh
```
the result of the prediction is 20.35373177134412

![prediction new](https://user-images.githubusercontent.com/104189782/191116969-bea4fc46-f5f2-4004-89b5-babe63e77cd3.png)

5. Deploying weebapp

Now, that the app is succesfully running locally, it can be deployed as an Azure WebApp and make requests to the API
```bash
az webapp up --name flaskwebappproject --resource-group Azuredevops --runtime "PYTHON:3.7"
```


App Home Page

Once the application is deployed, we can make an API request using the command NOTE: Change the url in the file 'make_predict_azure_app.sh'

sh ./make_predict_azure_app.sh
Make request to the WebApp

Logs from the webapp can be viewed using the command

az webapp log tail
Logs from the WebApp

Azure pipeline can now be configured for the webapp as detailed below: Note the official documentation should be referred to and double checked as you setup CI/CD.

Create a Devops Project Devops Project

Create a Service Connection Service Connection

Create a Agent Pool Agent Pool

Create Azure Pipeline Azure Pipeline

Run Pipeline to deploy the WebApp / Commit new features to the 'main' branch, which will automatically trigger the pipeline Deploy using Pipeline

Load test using Locust Load Test

Enhancements
Several improvements can be made to this project, some of the ideas are:

Currently the 'main' branch is unprotected. This branch can be setup such that additions can only be made using Pull Requests
Instead of using Azure Pipelines, GitHub actions itself can be used to setup continuos delivery/deployment
This app can be containerized as a Docker app and be deployed using Kubernetes
Demo
https://www.youtube.com/watch?v=Vs4AUya_4g8
