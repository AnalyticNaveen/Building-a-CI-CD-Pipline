# Building-a-CI-CD-Pipline

[![Python application test with Github Actions](https://github.com/AnalyticNaveen/Building-a-CI-CD-Pipline/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/AnalyticNaveen/Building-a-CI-CD-Pipline/actions/workflows/main.yml)

## Overview
In this project we have setup a CI/CD pipeline for a python based Machine Learning application which predicts housing prices in the city of Boston.

for Continuous Integration we have used GitHub as source control management service and its GitHub Actions service to perform linting and unit testing to ensure the software is in a usable state.

for Continuous Delivery/Deployment we have used Azure pipeline to deploy the latest changes to the software into production.

Any commits/merges to the master branch of the repository "main" is considered to be a change that needs to deployed. As a result of this action, GitHub actions and Azure Pipeline is triggered.

## Project Plan
This project was carried out using Agile methodologies and details of the planning can be view in the below artifacts:

A [link](https://trello.com/b/Vj5cPxHs/building-a-ci-cd-pipline) to a Trello board for the project

A [link](https://1drv.ms/x/s!An4-ExqtiP10igrbXPRUhq7GxwwR) to a spreadsheet that includes the original and final project plan

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
4. Github action

Create a github action workflow . edit the yml files as per requirement. 
once it is set. if do any commit , codes will be automatically tested and linted in github action
if build is succeed . it look like below image

![passing git action whole](https://user-images.githubusercontent.com/104189782/191118526-f5fb2fcc-65de-4482-843a-c88b76c9bfbb.png)

![passing build](https://user-images.githubusercontent.com/104189782/191118552-0abd16db-3651-4329-8850-c350c90c89dc.png)


5. Prediction.

Once all the libraries and dependencies are installed we can do our prediction for this we run below command 

```bash
./make_prediction.sh
```
the result of the prediction is 20.35373177134412

![prediction new](https://user-images.githubusercontent.com/104189782/191116969-bea4fc46-f5f2-4004-89b5-babe63e77cd3.png)


6. Deploying weebapp

Now, that the app is succesfully running locally, it can be deployed as an Azure WebApp and make requests to the API
```bash
az webapp up --name flaskwebappproject --resource-group Azuredevops --runtime "PYTHON:3.7"
```

Once the webapp is deployed it looks like this 

![webapp](https://user-images.githubusercontent.com/104189782/191119032-e64ce548-df0c-47ae-a072-ae18d8e785a2.png)


7. Creating Azure CICD pipeline 

follow the below steps to create a cicd pipeline

Create a Devops Project  -- for this project we have created Flask-ML-service 

Create a Service Connection -- naviagte to project setting and create service connection

![service connection](https://user-images.githubusercontent.com/104189782/191121290-d8991dc7-2764-4343-ab5a-42c8ddd1e6fa.png)

Create a Agent Pool Agent Pool

![agent pool](https://user-images.githubusercontent.com/104189782/191121367-c3ca36b5-bd05-4dce-862d-9ee7409d9f46.png)

Deployed VM and onnect with agent pool 

![vm deployed](https://user-images.githubusercontent.com/104189782/191121975-d21d0ad3-44b4-4da5-9893-ddc5f69eeab4.png)
![Vm connected with agent pool](https://user-images.githubusercontent.com/104189782/191122118-5b2ab2b1-abc2-43b7-aae0-c930fa2c40b3.png)
![self hosted agent online](https://user-images.githubusercontent.com/104189782/191122202-b0629230-6bba-4dba-9897-ca85596599f7.png)


Create and Run Azure Pipeline

![webapp deployed](https://user-images.githubusercontent.com/104189782/191122912-35552dd4-38d7-4157-914f-a1f05a8c22be.png)

Commit change and test pipeline

do some changes and test the pipline. it should be trigger with each commit.

![webapp deployed1](https://user-images.githubusercontent.com/104189782/191122971-29040593-fbd4-4411-8988-6ac6f5578883.png)


Load test using Locust Load Test

![locust load test](https://user-images.githubusercontent.com/104189782/191123317-b0699c4f-ac5b-4810-b288-e7945bcbcc55.png)

## Enhancements

providing proper package version or libraires can save a lot of time . without proper version we can get error in various steps 

## youtube video

https://youtu.be/wFuYOgghLt0
