## Container Scanning using GitLab
=============================================

Container scanning in GitLab is an important practice for ensuring that your containerized applications are secure. 

GitLab provides tools for scanning Docker images for known vulnerabilities and other security issues.

By setting up container scanning in GitLab, you can ensure that your Docker images are secure and free from known vulnerabilities. 

Integrating it into your CI/CD pipeline is straightforward, and GitLab provides an automated way to track and mitigate vulnerabilities as part of the development process.

#### 1. Enable Container Scanning in GitLab CI/CD

GitLab uses the Container Scanning feature as part of its built-in security scanning tools. 

This is done through GitLab CI/CD pipelines. 

To enable container scanning in your pipeline, you need to add the appropriate configuration in the `.gitlab-ci.yml file`.

`Steps`

A. Create or update your .gitlab-ci.yml file.

B. Add the container_scanning job to your pipeline configuration. The job will automatically scan your Docker image for vulnerabilities when it runs.

```
stages:
  - build
  - test
  - container_scan
  - deploy

container_scan:
  stage: container_scan
  image: docker:latest
  script:
    - docker build -t myimage .
    - docker push myimage
  allow_failure: true
  artifacts:
    reports:
      container_scanning: gl-container-scanning-report.json
```


In the above example, we have a container_scan job that runs after the build and test stages.

The docker image is used in the job to build the container image (docker build -t myimage .) and then push it to a container registry.

#### 2. GitLab Container Scanning Features

GitLab uses the GitLab Container Scanning feature to scan Docker images for vulnerabilities. This is powered by Trivy (an open-source vulnerability scanner).

GitLab checks the security of both the base image and the application dependencies in your Dockerfile.

It identifies vulnerabilities listed in multiple databases like NVD, Red Hat CVE database, etc.

GitLab creates a report in the pipeline, so you can review and address vulnerabilities.

#### 3. Reviewing the Scan Results 

After the container scanning job runs, GitLab generates a detailed report of the security vulnerabilities found in the Docker image. 

You can view the results from :-

`Merge request` GitLab will show security scan results directly in the merge request.

`Pipeline view` Results are also available in the pipeline’s job output.

You can view the security vulnerabilities, categorized by severity (Low, Medium, High, Critical), and take action to resolve them.

#### 4. Configure Vulnerability Management

GitLab provides integrated vulnerability management tools, so once vulnerabilities are found, you can track and manage them within GitLab:

You can integrate with GitLab’s Security Dashboard to get an overview of all detected vulnerabilities.

GitLab allows you to set policies to block merging of code that introduces vulnerabilities.

#### 5. Running Container Scanning on Self-Hosted GitLab

If you're running GitLab on your own infrastructure (self-hosted), you need to ensure that you have the appropriate GitLab Runner installed and configured to use container scanning features. 

This typically involves ensuring the runner is capable of running Docker commands and has access to Docker images.

#### 6. Allow Failure

In the .gitlab-ci.yml file, you can configure the container scanning job to allow failure, meaning the pipeline will continue even if vulnerabilities are found.

This might be useful during development, but for production, it's recommended to fail the job if vulnerabilities are detected.

```
allow_failure: false
```

#### 7. Additional Scanning with Other Tools

If you'd like to perform additional scanning beyond container scanning, GitLab integrates with tools like :-

  - SAST (Static Application Security Testing): For source code analysis.
  - DAST (Dynamic Application Security Testing): For runtime analysis of web applications.



## Kubernetes security scanning


Kubernetes security scanning involves assessing the security posture of your Kubernetes clusters, workloads, and containerized applications running within them. 

It focuses on detecting vulnerabilities, misconfigurations, and best practice violations that could lead to security breaches. 

Below are various tools and strategies you can employ to perform Kubernetes security scanning :-

#### 1. Kubernetes Security Scanning Tools

Several security tools are available to scan Kubernetes clusters for vulnerabilities, misconfigurations, and adherence to best practices. 

##### 1.1 Kube-bench

Kube-bench is an open-source tool for checking whether your Kubernetes cluster is configured according to the CIS Kubernetes Benchmark. 

It performs a series of checks on your cluster to ensure it adheres to Kubernetes security best practices.

Key Features :-

Checks against the CIS Kubernetes benchmark.

Provides detailed recommendations on how to resolve security issues.

Runs both as a standalone tool or as part of a CI/CD pipeline.

##### 1.2 Kube-hunter

Kube-hunter is a tool for penetration testing and vulnerability scanning for Kubernetes clusters. 

It helps to identify security vulnerabilities in your Kubernetes setup.

Key Features :-

Scans Kubernetes clusters for open ports, misconfigurations, and exposed secrets.

Finds security flaws in your cluster setup.

Can be run as a Kubernetes job or locally.

Works both for cloud-based and on-premises clusters.

##### 1.3 Trivy (for Kubernetes images)

Trivy is an open-source vulnerability scanner for container images, file systems, and Git repositories. 

It can be integrated into CI/CD pipelines to scan container images before deployment to a Kubernetes cluster.

Key Features :-

Identifies vulnerabilities in container images (including Kubernetes pods).

Integrates with CI/CD workflows for continuous scanning.

Supports multiple vulnerability databases (e.g., NVD, Red Hat CVE).

Can be used for container scanning, which is essential for securing Kubernetes workloads.

##### 1.4 Falco

Falco is a runtime security tool for Kubernetes that focuses on detecting abnormal behavior and security threats during runtime.

Key Features :-

Monitors system calls and Kubernetes events in real-time.

Detects suspicious activity such as privilege escalation, access to sensitive data, or unexpected network traffic.

Can be integrated with Kubernetes to monitor container activity and network behavior.

##### 1.5 KubeLinter

KubeLinter is a static analysis tool for Kubernetes resources. It helps to identify potential security issues in Kubernetes YAML files.

Key Features :-

Scans Kubernetes resource files (such as Deployments, Pods, etc.) for security issues before deployment.

Identifies risks like missing securityContext, use of privileged containers, and improper resource limits.

Helps to enforce security best practices in code before Kubernetes deployment.

##### 1.6 Open Policy Agent (OPA) + Gatekeeper

OPA is a general-purpose policy engine that works with Kubernetes to enforce security policies. 

Gatekeeper is the Kubernetes-native implementation of OPA, which allows you to define policies that Kubernetes resources must adhere to.

Key Features :-

Define and enforce policies for Kubernetes workloads.

Enforce security policies such as restricting the use of privileged containers or enforcing specific image sources.

Integration with Kubernetes Admission Control to prevent the creation of insecure resources.

#### 2. Kubernetes Vulnerability Scanning in CI/CD

In addition to scanning your Kubernetes cluster, it’s critical to scan your container images and Helm charts as part of your CI/CD pipeline. 

Some tools that integrate with CI/CD workflows include:

##### 2.1 GitLab CI/CD with Kubernetes Security Scanning

GitLab provides a native integration with Kubernetes security scanning for container images, which can be extended to Kubernetes deployments. 

You can integrate vulnerability scanning with GitLab CI/CD pipelines to scan Kubernetes manifests, Helm charts, and Docker images.

Steps :-

Use GitLab CI/CD pipelines to automate the scanning of your container images.

Enable Kubernetes security scanning within the pipeline using GitLab's Auto DevOps templates.

Integrate tools like Trivy or Kube-bench into the CI/CD pipeline for further vulnerability detection.

##### 2.2 Sonatype Nexus Lifecycle

Nexus Lifecycle can be integrated into your CI/CD pipelines to scan the open-source dependencies, container images, and Kubernetes manifests for vulnerabilities.

Key Features :-

Automatically scans container images for known vulnerabilities before deployment.

Allows for governance of dependencies used in Kubernetes deployments.


#### 3. Continuous Monitoring and Incident Response

After deployment, continuously monitor your Kubernetes cluster using tools like Falco and Sysdig to detect abnormal behavior in real-time. 

You should also have an incident response plan in place for mitigating any discovered vulnerabilities.

Falco can help detect security incidents during runtime and alert you in real time when suspicious activity occurs.

Integrate Kubernetes monitoring tools like Prometheus and Grafana for proactive monitoring of cluster health and security.

