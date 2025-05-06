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


## Basic YAML Syntax for .gitlab-ci.yml
=========================================


```
stages:
  - build
  - test
  - deploy

variables:
  NODE_ENV: production

build_job:
  stage: build
  script:
    - echo "Installing dependencies"
    - npm install
    - echo "Building project"
    - npm run build
  artifacts:
    paths:
      - dist/

test_job:
  stage: test
  script:
    - npm test
  dependencies:
    - build_job

deploy_job:
  stage: deploy
  script:
    - echo "Deploying application"
  only:
    - main
```


## GitLab CI/CD Components
================================


GitLab CI/CD is a powerful continuous integration and continuous deployment system built into GitLab. 

It automates the process of building, testing, and deploying code. 

Here are the key components of GitLab CI/CD :-


### .gitlab-ci.yml File

A `.gitlab-ci.yml` file is used to define the CI/CD pipeline configuration for a project in GitLab. 

It specifies how GitLab should run tests, build, and deploy your code when changes are pushed to the repository.

Location :- Root of your repository.

Contents :- Jobs, stages, scripts, conditions, and other configurations.

Example of a .gitlab-ci.yml file for a Node.js project :-

```
stages:
  - install
  - test
  - deploy

install_dependencies:
  stage: install
  image: node:18
  script:
    - npm install

test:
  stage: test
  image: node:18
  script:
    - npm run test

deploy:
  stage: deploy
  image: node:18
  script:
    - echo "Deploying application..."
    # your deployment script here
  only:
    - main  # deploy only when changes are pushed to the main branch
```

### Pipelines

A collection of stages and jobs defined in the .gitlab-ci.yml file.

A pipeline is a series of stages, and each stage contains one or more jobs. Jobs are executed in the order defined by the stages.

Trigger :-  On events like push, merge request, or manual action.

Status :-  Can be passed, failed, canceled, or skipped.


`How Pipelines Work`

A pipeline is triggered when :-

  - Code is pushed
  - A merge request is created
  - Manually from the UI

Execution :- Each job runs in a fresh environment (like a Docker container).

Artifacts :- Jobs can pass files (like compiled assets) between stages.


`Viewing Pipelines`

In GitLab, you can view pipelines under :-

  - Project → CI/CD → Pipelines
  - Each pipeline will show = Status (passed, failed), Duration and Jobs and logs


Example Pipeline :-

```
stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "Building project..."

test_job:
  stage: test
  script:
    - echo "Running tests..."
    - exit 0  # simulate success

deploy_job:
  stage: deploy
  script:
    - echo "Deploying to production..."
  only:
    - main
```

### Stages

In GitLab CI/CD, stages define the sequential phases of your pipeline. 

Each stage can contain one or more jobs, and jobs in the same stage run in parallel. 

The stages themselves run in order, one after another.

Logical groupings of jobs (e.g., build, test, deploy).

You must define all stages in the stages :- block at the top.

If you skip declaring stages, GitLab uses a default : build, test, deploy.

Jobs without a stage : tag default to the test stage.

`Basic Structure of Stages`

```
stages:
  - build
  - test
  - deploy
```


build :- Compile code or generate static files.

test :- Run unit tests, linting, or other checks.

deploy :- Push to a server, cloud provider, or GitLab Pages.



`How it Executes`

install_dependencies runs first.

If it succeeds, run_tests runs.

If that succeeds and the commit is on the main branch, deploy_site runs.


===========END=========================
