# DPS_Challenge
Basic end-to-end machine learning project using VertexAI


## Overview ##
In this project, we describe the usage of Google Cloud's "Vertex AI" ML platform to build a complete end-to-end ML pipeline. We used the popular Auto MPG dataset from Kaggle to predict a vehicle's fuel efficiency using a basic regression with TensorFlow. Additionally, we performed ...


## Environment Setup ##
After signing in to Cloud Console and creating a new project, run these commands to confirm you are set to the correct project

```
gcloud auth list
gcloud config list project
```

If it's not set to the correct project, use this command

```
gcloud config set project <PROJECT_ID>
```