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



### Jobs

In GitLab CI/CD, jobs are the individual tasks that run within each stage of your pipeline. 

A job can be anything from running tests to building your site or deploying code.

`Basic Job Structure`

```
job_name:
  stage: stage_name
  script:
    - command 1
    - command 2
```

job_name : Unique identifier for the job.

stage : Specifies which stage the job belongs to.

script : List of shell commands to execute.


`Example`


```
stages:
  - build
  - test

build_app:
  stage: build
  script:
    - echo "Building app..."

unit_tests:
  stage: test
  script:
    - echo "Running tests..."
```

`Useful Job Options`


| Option            | Description                                                       |
| ----------------- | ----------------------------------------------------------------- |
| `script`          | Commands the job runs.                                            |
| `stage`           | Which pipeline stage the job is in.                               |
| `only` / `except` | Run this job **only** on certain branches or conditions.          |
| `artifacts`       | Save files from a job to pass to later jobs.                      |
| `dependencies`    | Define which previous jobs this one relies on for artifacts.      |
| `tags`            | Use when running on specific GitLab runners with tags.            |
| `rules`           | More flexible job conditions than `only/except`.                  |
| `when`            | When the job should run (e.g., `on_success`, `manual`, `always`). |
| `allow_failure`   | Let the pipeline continue even if this job fails.                 |


### Runners

In GitLab CI/CD, a runner is the agent (or server) that executes your pipeline jobs. 

Runners are what actually run the scripts defined in your .gitlab-ci.yml file.

`Types`

1. Shared Runners
-----------------------
   
Managed by GitLab (especially on GitLab.com).

Automatically available to all projects.

Great for general-purpose CI/CD needs.


2. Specific Runners
------------------------

Installed and configured by you.

Registered to a specific project or group.

Useful when you need :

   - Custom dependencies
   - Access to internal resources (e.g., databases, servers)
   - Faster execution

`Runner Executors`


Each runner uses an executor to run jobs. 

 - shell : Runs directly on the host machine shell
 - docker : Spins up a Docker container for each job
 - docker+machine : Automatically provisions Docker machines
 - kubernetes : Uses a Kubernetes cluster to run jobs
 - virtualbox, ssh, etc. (less common)


`Registering a GitLab Runner`

Install GitLab Runner on your server :- sudo apt install gitlab-runner

Register it :- gitlab-runner register

You'll be prompted for :

 - GitLab URL
 - Registration token (from GitLab UI under Settings → CI/CD → Runners)
 - Executor (e.g., docker, shell, etc.)


`View and Manage Runners`

Go to your GitLab project :- Settings → CI/CD → Runners


### Artifacts

In GitLab CI/CD, artifacts are files or directories generated by a job that are passed to later stages or made available for download from the pipeline UI.

Files generated by jobs that can be passed to other jobs or downloaded.

Use Case: Build results, test reports.

Artifacts are used to :-

 - Share build outputs between jobs (e.g., compiled files, reports).
 - Store logs, test results, or binaries.
 - Archive data for review (e.g., a ZIP of an HTML site).


`Basic Example`

```
build:
  stage: build
  script:
    - mkdir dist
    - echo "Hello World" > dist/index.html
  artifacts:
    paths:
      - dist/
```

This job creates a dist/ directory and saves it as an artifact. 

You’ll see a "Download artifacts" button in the pipeline UI when the job completes.


`Artifact Expiration`

By default, artifacts are kept for 30 days, but you can change it

```
artifacts:
  paths:
    - dist/
  expire_in: 1 hour
```

`Controlling Artifact Flow`

If you want a later job to use an artifact from an earlier job

```
test:
  stage: test
  dependencies:
    - build
```


### Cache

Cache is used to speed up your pipelines by reusing files between jobs and pipeline runs — typically for things like dependencies or build outputs.

GitLab saves the cache after a job runs, and reuses it in subsequent jobs or pipelines (if the same cache key is matched).


Used to speed up job execution by storing commonly used files (e.g., dependencies).


`Key Differences Between Cache and Artifacts`

| Feature  | **Cache**                           | **Artifacts**                       |
| -------- | ----------------------------------- | ----------------------------------- |
| Scope    | Can persist **across pipelines**    | Exists only **within one pipeline** |
| Use case | Speeds up job setup (e.g., `npm i`) | Transfers files between jobs/stages |
| Expiry   | Optional manual configuration       | Can expire after a set time         |



`Cache Example`

```
cache:
  paths:
    - node_modules/

install:
  stage: build
  script:
    - npm install
```

This caches the node_modules folder. On the next run, GitLab will reuse the cached directory if the runner supports it.


### Environments & Deployments

Environments and Deployments let you define where and how your application is released — such as staging, production, or any custom target environment.


`What is an Environment`

An environment represents a deployment target — like :-

 - development
 - staging
 - production

GitLab tracks each environment, displays deployment history, and supports manual rollbacks and monitoring.


`What is a Deployment`

A deployment is the action of pushing code to an environment, triggered by a CI job.


`Example with Environments`

```
deploy_to_production:
  stage: deploy
  script:
    - echo "Deploying to production server..."
  environment:
    name: production
    url: https://example.com
  only:
    - main
```

GitLab shows this as a deployment to the production environment. A "View Environment" button will appear in the UI with the URL provided.


`Example with Staging and Manual Deploy`

```
stages:
  - test
  - deploy

test:
  stage: test
  script:
    - echo "Running tests..."

deploy_staging:
  stage: deploy
  script:
    - echo "Deploying to staging..."
  environment:
    name: staging
    url: https://staging.example.com
  only:
    - develop

deploy_production:
  stage: deploy
  script:
    - echo "Deploying to production..."
  environment:
    name: production
    url: https://example.com
  only:
    - main
  when: manual
```

deploy_production runs only on main and must be triggered manually. You’ll see both environments listed in Deployments → Environments in GitLab.


`Rollback & Stop Environments`

```
stop_production:
  stage: deploy
  script:
    - echo "Shutting down production..."
  environment:
    name: production
    action: stop
```


### Triggers & Schedules

Triggers and Schedules provide ways to automatically start pipelines outside of the usual push/MR events.

It is ideal for automation, integrations, or regular tasks like backups and updates.


`Triggers`

Triggers allow external systems or scripts to start pipelines in GitLab.

Common Use Cases :-

Start a pipeline from another GitLab project.

Trigger from a webhook or third-party tool (e.g., Zapier, Jenkins).

Automate builds after external events.

How to Use Triggers :-

Create a Trigger = Go to your project → Settings → CI/CD → Pipeline triggers , Add a trigger and copy the token.

In .gitlab-ci.yml (optional)
```
trigger_deploy:
  stage: deploy
  trigger:
    project: other/project
    branch: main
```


`Schedules`


Pipeline Schedules run pipelines on a recurring basis (like a cron job).

Common Use Cases :-

Nightly builds

Weekly security scans

Automated backups

How to Set Up a Schedule :-

Go to your project → CI/CD → Schedules , Click “New schedule” , Set: Cron format (0 3 * * * → daily at 3am) , Branch , Optional variables


```
nightly_job:
  script:
    - echo "Running nightly task..."
  only:
    - schedules
```

### Variables

Definition: Used to define environment-specific or secret values (API keys, environment names).

Defined in :-

.gitlab-ci.yml

GitLab UI (CI/CD settings)

Group/project level


## Host a webapp using pipeline
=====================================


`Step 1 :- Create Your GitLab Project`

  - Go to https://gitlab.com.
  - Create a new project
  - Name it = e.g., my-webapp-repo
  - Visibility = set to Public if you want your site accessible to everyone.


`Step 2 :- Add Your Web Files in a public/ Folder`

  - Create a folder named public
  - Inside folder(Public)
  - create index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mywebapp-25</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Hello i am GitLab-webapp!</h1>
</body>
</html>
```

  - create style.css


```
body {
  background-color: #e0f7fa;
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 50px;
}
```

`Step 3 :- Create .gitlab-ci.yml`

```
pages:
  stage: deploy
  script:
    - echo "Deploying to GitLab Pages"
  artifacts:
    paths:
      - public
  only:
    - main  # or 'master' depending on your branch
```


`Step 4 :- Wait for GitLab CI/CD to Deploy`

  - Go to your project in GitLab
  - Click on Build > Pipelines
  ( You should see a list of pipeline runs. A successful pipeline will display a green checkmark )
  - 

`Step 5 :- Access it`

  - In your project, go to Deploy > Pages
  - You'll find the URL to your live site

=========END=============

===========END=========================
