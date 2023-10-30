# ci-cd
This repo is for CI/CD code for multiple microservices, here as a example we have pushed code for one code repo, and CD for multiple microservices as module in CD repo.

Here we have taken an example of one Ecommerce application, which is divided into multiple microservices, as below:

- Login page : microservice-1-login
- Categories page : microservice-2-category
- Payment page : microservice-3-payment
- Accounts page : microservice-4-accounts
- Checkout page : microservice-5-checkout
- Card Details page : microservice-6-card-details
- Shopping cart page : microservice-7-shopping-cart
- Save details : microservice-8-savedetails_


**For CI** : we have the code repo folder along with .gitlab-ci.yml file inside : ci-code directory
**For CD** : we have modules for all microservices, and under those modules we have different folder like helm chart, docker file etc. : cd-deploy directory

**In CI we have below jobs :**

- build : This stage will build the artifacts which will be passed to CD deployment pipeline
- test : This stage run unit tests against the code to validate the code functionality
- code-quality : This stage will run, the sonar, secret analysis, maven dependency, and other basic validation on code.
- trigger-deploy : This stage will trigger the pipeline for specific microservice in CD project, with the matching TRIGGER_VARIABLE._

**In CD we have below jobs:**

- build-image-microservice-1-login: This job will be  triggered from microservice 1 CI pipeline, and this will build the image with help of Dockerfile
- container-scanning-microservice-1-login: This stage will scan the vulnerabilities in the image created
- sign-image-microservice-1-login: This stage will sign the image to push it to the image registry with keys
- deploy-dev-microservice-1-login: This stage will deploy the code to the dev cluster
- deploy-teststable-microservice-1-login: This stage will deploy the code to the teststable cluster.