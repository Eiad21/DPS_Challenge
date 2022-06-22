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

Give the project access to the Compute Engine, Container Registry, and Vertex AI services with the following command

```
gcloud services enable compute.googleapis.com         \
                       containerregistry.googleapis.com  \
                       aiplatform.googleapis.com
```

We'll also need a storage bucket to store our saved model assets. Run the following commands to create one:

```
BUCKET_NAME=gs://$GOOGLE_CLOUD_PROJECT-bucket

gsutil mb -l us-central1 $BUCKET_NAME
```


## Containerize ##

After uploading uploading the file in this repo to the Google Cloud project, we'll need to correctly set the BUCKET_NAME variable in the train.py file with the $BUCKET_NAME value we set previously. Afterwards we'll use the following lines to build a container for the train.py file

```
IMAGE_URI="gcr.io/$GOOGLE_CLOUD_PROJECT/mpg:v1"

docker build ./ -t $IMAGE_URI

docker push $IMAGE_URI
```


## Run Training ##

Next we'll use the container we built to run our training code. First, navigate to the Training subsection in the Vertex section of the Cloud console and select Create.

<img src="https://codelabs.developers.google.com/codelabs/vertex-ai-custom-models/img/vertex-menu-training.png" alt="training_v" width="250"/>

* Select No managed dataset
* Then select  (advanced) Set the training method as Custom training and click Continue.
* Enter a for name for the model 
* Click Continue

Select 'Custom Container' and choose the container created in the previous step

<img src="https://codelabs.developers.google.com/codelabs/vertex-ai-custom-models/img/select-custom-container.png" alt="container_c" width="250"/>
<!-- ![container_c](https://codelabs.developers.google.com/codelabs/vertex-ai-custom-models/img/select-custom-container.png) -->

The only other setting that needs to be set is the 'Machine type' in ' Compute and pricing'. Set it to n1-standard-4 as this training job is a relatively lightweight one and leave the rest as is. The training job will take around 15 minutes to complete

<img src="https://codelabs.developers.google.com/codelabs/vertex-ai-custom-models/img/machine-type-vertex.png" alt="container_c" width="300"/>


## Deploy trained model to endpoint ##

After the model has been deployed, select it from the Models tab and click 'Deploy to Endpoint'. Choose a name for the endpoint, and select an appropriate machine and leave the rest as is.

<img src="https://github.com/Eiad21/DPS_Challenge/blob/main/images/endpointname.png?raw=true" alt="endpoint_name" width="300"/>

<img src="https://github.com/Eiad21/DPS_Challenge/blob/main/images/endpointname.png?raw=true" alt="endpoint_machine" width="300"/>

