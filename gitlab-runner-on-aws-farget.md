## GitLab Runner on AWS Fargate

This process Setting up a GitLab Runner on AWS Fargate which allows us to run CI/CD jobs in a serverless environment, reducing the need for managing EC2 instances.


#### Requirements


AWS account with permissions to create ECS resources.

GitLab account with admin access to your repository.

Docker installed locally (for building images).

GitLab Runner registered to your GitLab instance.


### Steps


#### 1. Set Up AWS IAM Role for ECS Fargate

     - Go to the IAM console in AWS.
     - Create a new role.
     - Select the ECS service and choose Fargate as the use case.
     - Attach policies such as `AmazonECSTaskExecutionRolePolicy` and `AmazonECRReadOnly`.
     - Name this role `ecsTaskExecutionRole`.


( Create another IAM role that the GitLab Runner will use, with permissions for interacting with ECS, CloudWatch, and any other services needed by your jobs.)

#### 2. Create Docker Image for GitLab Runner
   
( You can use the official GitLab Runner Docker image or create a custom one.)


`vi Dockerfile`

```
FROM gitlab/gitlab-runner:alpine

# Optional: Install additional dependencies
RUN apk add --no-cache curl bash

# Set environment variables for GitLab Runner
ENV CI_SERVER_URL="https://gitlab.com"
```


Push this Docker image to Amazon ECR.


#### 3. Set Up ECS Cluster for Fargate

     - Open the Amazon ECS console.
     - Create a new cluster, choosing Networking only (Fargate).
     - Set the cluster name (e.g., gitlab-runner-cluster).
     - Leave the other options as default and create the cluster.

Create ECS Task Definition:

You need to define a task definition for your GitLab Runner container.

Go to the Task Definitions section in ECS and click Create new Task Definition.

Select FARGATE as the launch type.

Define a name for the task (e.g., gitlab-runner-task).

Under Task Role, use the IAM role you created earlier (ecsTaskExecutionRole).

Add a container to this task definition:

Container name: gitlab-runner

Image: the URL to your ECR GitLab Runner image (or the official image if you're using it).

Set memory and CPU according to your needs (e.g., 1 GB memory, 0.5 CPU).

Set up logging with AWS CloudWatch Logs.
     
     
#### 4. Register GitLab Runner

To register your GitLab Runner with the GitLab instance, run the following command on your local machine or in an EC2 instance.

```
docker run --rm -it gitlab/gitlab-runner register \
  --non-interactive \
  --url "https://gitlab.com/" \
  --registration-token "YOUR_REGISTRATION_TOKEN" \
  --executor "docker" \
  --docker-image "docker:latest" \
  --description "fargate-runner" \
  --tag-list "fargate" \
  --run-untagged="true" \
  --locked="false"
```

( Replace YOUR_REGISTRATION_TOKEN with the token you get from GitLab.)









