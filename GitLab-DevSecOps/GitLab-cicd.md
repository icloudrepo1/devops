## GitLab CI/CD
======================

GitLab CI/CD is a built-in continuous integration and continuous deployment system. 

It’s tightly integrated into the GitLab platform and configured through a single YAML file in your repository.

It automates :-

 - Building your application
 - Testing it for bugs or security issues
 - Deploying it to production or staging environments



### CI/CD Pipeline Basics


A CI/CD pipeline is an automated sequence of steps that takes code from version control and :-

 - Builds it
 - Tests it
 - Deploys it

This process reduces manual work and helps teams deliver reliable software faster.


`CI vs. CD`

CI (Continuous Integration)	= Automatically builds and tests code when changes are pushed.

CD (Continuous Delivery)	= Automatically prepares or delivers code to production or staging after successful CI.

CD (Continuous Deployment)	= Code is automatically deployed to users once tests pass—no manual approval needed.



### Pipeline Components

1. Stages
   
List of pipeline phases (in execution order)

These are the major phases in your pipeline.

```
stages:
  - build
  - test
  - deploy
```

2. Jobs
   

Each job runs scripts within a stage. Jobs in the same stage run in parallel; stages run in order.   

Tasks that run in each stage, such as :-

 - Installing dependencies
 - Running unit tests
 - Deploying to a server



