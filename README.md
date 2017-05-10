# Elastic Beanstalk Multi Container Node.js + Tomcat with Nginx Demo App

This demo app shows you how to run simple Node.js and Tomcat applications listening on different ports. This application makes use of the [Node.js](https://registry.hub.docker.com/u/library/node/) and [Tomcat](https://registry.hub.docker.com/u/library/tomcat/) Docker images from the official Docker library.

## Run the App
Follow the steps below to deploy this application to an Elastic Beanstalk Multi-container Docker environment. Accept the default settings unless indicated otherwise in the steps below:

1. Download the ZIP file from the [Releases section](https://github.com/awslabs/eb-docker-multiple-ports/releases) of this repository.
2. Login to the [Elastic Beanstalk Management Console](https://console.aws.amazon.com/elasticbeanstalk)
3. Click 'Create New Application' and give your app a name and description
4. Click 'Create web server' and select an IAM instance profile to use.<br>*Note: Please ensure the IAM instance profile you select has the necessary permissions. For more information, see [Container Instance Role](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html#create_deploy_docker_ecs_role)*
5. Choose 'Multi-container Docker' in the 'Predefined configuration' dropdown and click `Next`
6. Upload the ZIP file downloaded in step 1
7. Review and launch the application


### Sample Elastic Beanstalk Multi Container 
### Node.js + Tomcat Demo App

![AyeAye](https://github.com/shippableSamples/node-build-push-docker-hub/blob/master/public/resources/images/captain.png)

# Sample Java/Tomcat app running in Docker container on Elastic Beanstalk

A simple demo to deploy two containers to a multi-container environment listening 
on different ports to Amazon Elastic Beanstalk using Shippable.

This repo demonstrates the following features:
* Set up serverless CI, i.e. on Shippable-provided infrastructure
* Set up CD pipelines for deploying a docker image to a Multi-Container Docker 
Configuration on Amazon Elastic Beanstalk
* Perform docker build to create Tomcat container and Node app container
* Push docker images to Amazon ECR
* Automatically deploy docker images to TEST environment on Elastic Beanstalk
* Manually deploy docker images to PROD environment on Elastic Beanstalk
* Set up runCLI job types in Shippable using AWS EB CLI

## Prerequisites to run this sample
* Source control account (e.g. GitHub, Bitbucket, Gitlab)
* Shippable account (sign up for free at www.shippable.com)
* Amazon Web Services account (aws.amazon.com)

## Setup
* Fork this repo to your source control account
* Follow the [AWS instructions](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html)
to create a Elastic Beanstalk application, called `deploy-eb-docker-multi-container`, 
and two multi-container Docker environments, one called `test-01` and one called 
`prod-01` (just deploy the Sample application for now)
* [Follow the instructions](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.container.console.html#docker-images) 
to enable your EB environments to access your private docker images in Amazon ECR
* Follow the [instructions](insert link) to store your AWS credentials needed 
for this sample in Shippable
* All CI config is in `shippable.yml`. Check this file and update the config 
wherever the comment asks you to replace with your specific values (for example, 
to replace with your Integration names)
* Enable the project for CI
  * Select your subscription from the dropdown menu in upper left (three 
  * Select the **Enable project** tab
  * Enable your forked repo "deploy-eb-docker-multi-container"
  * If you don't see it in the list, select **Sync** and search again
* All pipeline config is in `shippable.resources.yml` and `shippable.jobs.yml`. 
Check these files and update config wherever the comment asks you to replace 
with your specific values (for example, to replace with your Integration names)
* Add the pipeline to your SPOG view in Shippable:
  * Select your subscription from the dropdown menu in upper left (three 
  horizontal lines)
  * Select the **Pipelines** tab
  * Select the "+" icon in the upper right
  * Select the source control repo where your fork is 

## Run the pipeline 
* Right-click on the runCI job in the SPOG view named 'deploy-eb-docker-multi-
container_runCI' and run the job.
  * This will run the CI job and push your images to ECR, then trigger a 
  deployment to your `test-01` environment in Elastic Beanstalk
  * This demo uses a custom scripting job type called 'runCLI' in Shippable - 
  [learn more about 'runCLI' jobs](http://docs.shippable.com/pipelines/jobs/runCLI/) 
* When your job completes, you should see:
  * The images you pushed to Amazon ECR now deployed to your `test-01` environment
  * A new Amazon ECS task definition created and running in Amazon ECS
* Right-click on the runCLI job in the SPOG view named 'deploy-eb-docker-multi-
container-prod-deploy' and run the job to deploy to your `prod-01` environment
* Make a change to the `tomcat-app/index.jsp` file, commit it, and it to your 
source control repo
  * A CI job will automatically run and deploy the newly updated image to `test-01` 

Your end-to-end pipeline is complete! With this approach, your entire team can 
easily manage multi-stage pipeline deployments to Elastic Beanstalk, including 
multi-container deployments.

### CI console screenshot
![CI Console Log](https://github.com/shippableSamples/java-ecr-runcli-elasticbeanstalk/blob/master/resources/images/java-ecr-runcli-elasticbeanstalk-CI.png)

### AWS integration screenshot
![Integration View](https://github.com/shippableSamples/java-ecr-runcli-elasticbeanstalk/blob/master/resources/images/java-ecr-runcli-elasticbeanstalk-integration.png)

### CD Pipeline SPOG screenshot
![CD Pipeline](https://github.com/shippableSamples/java-ecr-runcli-elasticbeanstalk/blob/master/resources/images/java-ecr-runcli-elasticbeanstalk-CD.png)

