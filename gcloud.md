# Setup Google Cloud Compute Engine Instance

1) Create instance
2) Log into instance and run:\
    `gcloud compute project-info add-metadata --metadata enable-oslogin=TRUE`
3) Install gcloud
4) Run `gcloud auth login` to identify yourself
5) Run `gcloud compute ssh instance-1` where `instance-1` is your instance name