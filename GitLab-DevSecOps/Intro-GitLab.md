## Introduction to GitLab
============================


GitLab is a web-based DevOps lifecycle tool. 

It provides a Git repository manager offering source code management (SCM), CI/CD, and various DevOps capabilities in a single application. 

It's widely used for managing software development workflows from planning to monitoring.

It enabling teams to collaborate efficiently and deliver software faster.

GitLab combines the ability to :-

 - Host Git repositories (like GitHub)
 - Manage source code with features like branches, merge requests, and issues
 - Collaborate through code reviews and project planning tools
 - Integrate DevOps tools for CI/CD, security, and monitoring

### components of GitLab



#### 1. Version Control

GitLab is built on Git, allowing teams to store and manage their source code in repositories. 

It supports branching, merging, and other common version control features that allow multiple developers to work on the same project simultaneously.

#### 2. Continuous Integration/Continuous Deployment (CI/CD)

GitLab has powerful CI/CD tools built-in, enabling developers to automate the process of testing, building, and deploying applications. 

Whenever code is pushed to the repository, GitLab can automatically run tests, build the project, and deploy it to different environments.

#### 3. Issue Tracking

GitLab provides an integrated issue tracking system, allowing teams to track bugs, tasks, and feature requests within the platform. 

Developers can link issues to commits, branches, and merge requests, creating a seamless workflow for managing development tasks.

#### 4. Merge Requests (MRs)

GitLab’s Merge Requests are similar to "pull requests" in other systems. 

They allow team members to propose changes to the codebase. 

Other team members can review the changes, discuss them, and approve or suggest improvements before they are merged into the main codebase.

#### 5. Project Management Tools

GitLab has built-in tools for project management, such as Kanban boards, milestones, and epics. 

This allows teams to organize their work, track progress, and manage releases in a structured way.

#### 6. Security and Compliance

GitLab includes features like static code analysis, dependency scanning, and container scanning to help teams identify security vulnerabilities in their code and dependencies. 

It also includes compliance tools to help with audit trails and regulatory requirements.

#### 7. Auto DevOps

Auto DevOps is a feature in GitLab that helps automate the entire DevOps lifecycle, from code creation and testing to deployment and monitoring, using best practices.

#### 8. Self-hosted and Cloud-hosted

GitLab is available both as a self-hosted version (where you can install and manage GitLab on your own infrastructure) and as a cloud-hosted version (GitLab.com, where GitLab takes care of the hosting).

#### 9. Collaboration Tools

GitLab provides collaboration features like wikis, code reviews, and discussions to help teams communicate and collaborate better while working on the same codebase.

#### 10. Integrations

GitLab integrates with a wide range of tools and services like Slack, Kubernetes, Jira, and more to provide a smooth and connected development workflow.



### Why Use GitLab ?



`All-in-one platform` GitLab offers a comprehensive suite of tools that cover all stages of the software development lifecycle.

`DevOps capabilities` GitLab is tailored for DevOps practices, allowing teams to automate builds, tests, and deployments, reducing manual overhead.

`Collaboration` GitLab makes it easy for multiple developers to work together on the same project, providing tools for code review, issue tracking, and team communication.

`Flexibility` GitLab can be self-hosted or used as a cloud-based service, giving teams flexibility depending on their needs.


`GitLab is a powerful, all-in-one platform for managing software development projects, providing a full set of tools for version control, collaboration, CI/CD, security, and more.`



## GitLab Premium/Ultimate vs. Free tiers
===============================================


Free Tier is great for individuals, hobby projects, or simple CI/CD workflows.

Premium Tier targets teams needing collaboration tools, pipeline flexibility, and moderate security.

Ultimate Tier is designed for enterprises with strict security, compliance, and governance requirements—especially for full DevSecOps.



## GitLab Install
======================


To install and set up GitLab, you can choose between:

 - GitLab.com (cloud-hosted) – No setup required, just sign up.
 - Self-managed GitLab (self-hosted) – You install it on your server (e.g., Ubuntu, CentOS, or Docker).



`cloud-hosted :- Use GitLab.com (Recommended for Most Users)`

##### Steps :-

Go to https://gitlab.com

Click "Register" and create an account.

Create a new project/repository.

Start using GitLab’s features (repository, issues, CI/CD, etc.).


`self-hosted`

##### Steps :-

##### 1. Update Your System

```
sudo apt update
sudo apt upgrade
```

##### 2. Install Dependencies

```
sudo apt install -y curl openssh-server ca-certificates
```

##### 3. Install Postfix (Optional)

```
sudo apt install -y postfix
```

##### 4. Download and Install GitLab

```
curl https://packages.gitlab.com/gpg.key | sudo apt-key add -
```

##### 5. Add the GitLab repository

```
sudo sh -c 'echo "deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ $(lsb_release -c | awk "{print $2}") main" > /etc/apt/sources.list.d/gitlab_gitlab-ce.list'
```

##### 6. Update the package list again

```
sudo apt update
```

##### 7. Now, install GitLab Community Edition

```
sudo apt install -y gitlab-ce
```

##### 8. Configure GitLab

```
sudo gitlab-ctl reconfigure
```

##### 9. Access GitLab

Once the configuration is complete, open your web browser and navigate to the server’s IP address or domain name.

If you’re using the IP address, it will look something like `http://<your-server-ip>/`

You should see the GitLab setup page. The default login is:

  - `Username: root`

  - Password: The password was set during installation or can be found in

    ```
    sudo cat /etc/gitlab/initial_root_password
    ```

##### 10. Set Up GitLab

Once logged in, you can change the root password and configure GitLab further.


================END===================
