# ImageTrainer
Image training app written in Python using Keras &amp; Tensorflow based on image folder names
# To activate virtual env:
pip install virtualenv
virtualenv venv
venv\Scripts\activate
# To install all requirements:
pip install -r .\requirements.txt
# install tensorflow:
pip install tensorflow
pip install cloudml-hypertune
pip install tensorflow-gpu
# to start python type:
clear
python .\trainer.py
python .\DataHandler.py

# Build and test your Docker image locally run at google cloud SDK shell
# Refer help https://cloud.google.com/ai-platform/training/docs/custom-containers-training

docker build -t asia.gcr.io/lively-aloe-320309/tf_image_callsification:image_classification .

docker image list

gcloud auth login

docker push asia.gcr.io/lively-aloe-320309/tf_image_callsification:image_classification

# Launching a training jobon gcloud AI-platform. To do this activate cloud shell on https://console.cloud.google.com/ai-platform/jobs?project=lively-aloe-320309
# and write these cmds over there in web browser:

export REGION=asia-southeast1
echo $REGION

export JOB_NAME=image_classification_container_job_$(date +%Y%m%d_%H%M%S)
echo $JOB_NAME

export IMAGE_URI=asia.gcr.io/lively-aloe-320309/tf_image_callsification:image_classification
echo $IMAGE_URI

gcloud ai-platform jobs submit training $JOB_NAME \
  --region $REGION \
  --master-image-uri $IMAGE_URI \
  -- \
  --batch_size=8
