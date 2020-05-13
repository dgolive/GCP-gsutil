# gcloud command-line tool 


INSTALL
sudo snap install google-cloud-sdk --classic

ACCESS
gcloud auth login
gcloud config set project project-name
gcloud compute ssh --zone "southamerica-east1-b" "vm-name" --project "project-name"


RESPONSE FORMAT
gcloud compute instances list --format json
