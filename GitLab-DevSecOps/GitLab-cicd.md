## GitLab CI/CD Pipeline Basics
====================================

GitLab CI/CD is a built-in continuous integration and continuous deployment system. 

It’s tightly integrated into the GitLab platform and configured through a single YAML file in your repository.

A CI/CD pipeline is an automated sequence of steps that takes code from version control and It automates :-

 - Building your application
 - Testing it for bugs or security issues
 - Deploying it to production or staging environments

This process reduces manual work and helps teams deliver reliable software faster.


`CI vs. CD`

CI (Continuous Integration)	= Automatically builds and tests code when changes are pushed.

CD (Continuous Delivery)	= Automatically prepares or delivers code to production or staging after successful CI.

CD (Continuous Deployment)	= Code is automatically deployed to users once tests pass—no manual approval needed.


### Key Components

1. .gitlab-ci.yml File
2. Pipelines
3. Stages
4. Jobs
5. Runners
6. Artifacts
7. Cache
8. Environments & Deployments
9. Triggers & Schedules
10. Variables

===========END=========================
