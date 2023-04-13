Basic setup documentation:

Prerequisites:
Before you start make sure you have:
- Google Cloud active account: https://cloud.google.com/
- Github active account: https://github.com/
- Terraform installed: https://www.terraform.io/
- Visual studio code installed (in fact any sort of IDE will do. This example showcases working with VSC)

Steps to perform if you want to host a simple static website using Google Cloud Virtual Machine, Google Cloud Buckets and Terraform:
1. Create a new repository on Github,
2. Download it to your local
3. Add a new working space to downloaded repository

Steps to perform in Visual Studio Code:
1. Create a file: index.html - where you will store the content of your website. 
2. Choose a picture you wish to have on your website and add it to your repository. 
3. Create files you need to have to have in order to create an infrastructure that will be created on Google Cloud Platform:
    main.tf - where you will store the definition of your resources: virtual machine and bucket,
    provider.tf - where you will mark, that google cloud is your cloud provider
    backend.tf - where you will make sure that the files are not just existing on your local disc.
    For proper creation of mentioned files you might need the documentation: https://www.terraform-best-practices.com/

Steps to perform in Google Cloud Platform:
1. You need to create a Service Account in GCP. Service Account in GSP is a type of an account that grants permissions to VMs. This is much safer way than granting the permissions to end users. In order for Terraform to communicate with GCP you need to generate a private key. Go to Google Cloud Console/IAM and admin/Service accounts Click on: Create Service Account:
Fill in:
- Service account name, click Create and continue,
- Grant this service account access to the project - choose Project/Editor, click Continue,
Click: Done. 
Click on the service account you just created and click Keys. Click on Add key/JSON. The file will be automatically downloaded to your local machinte. Open the file, delete all new lines and copy the content of the JSON file.
2. You need to create a Github action to automate the process of deployment. Go to your repository on Github and click on Settings/Secrets and variables/Actions 
    Then choose New repository secret
Fill in:
- Name - choose one and type it
- Secret - you need to paste the content of the JSON file

Steps to perform in Visual Studio Code:
1. In your repository create a new path called .github\workflows
2. In the folder workflows create a new file called terraform.yml - copy my code from terraform.yml and paste it to the file you created
3. Push the commit to Github.

Steps to perform in Github:
1. In your repository find the tab Actions and click it. You shall find there a running workflow triggered by the commit you just made.
The website is deployed in Google Cloud Platform on Virtual Machine, in the bucket you created. 

Steps to perform in GCP:
1. Go to Cloud Storage/Buckets. Click on the bucket you created (you specified the name in the main.tf file).
2. Click on Upload Files - add a file index.html and the picture you chose to put on the website in the .jpg format.
3. Click on index.html, copy public URL and paste it in the browser. You should see the content of the website you specified in index.html.