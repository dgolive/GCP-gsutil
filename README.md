# gcloud command-line tool 


## Install:
- sudo snap install google-cloud-sdk --classic

## Access
- gcloud auth login
- gcloud config set project project-name
- gcloud compute ssh --zone "southamerica-east1-b" "vm-name" --project "project-name"


## Response Format
- gcloud compute instances list --format json
