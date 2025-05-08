## deploy a shell executor on AWS
==========================================

### 1. launch instance > ubuntu
### 2. connect it and run below commands

 ```
 sudo apt update
 ```


### 3. Install GitLab Runner


`https://docs.gitlab.com/runner/install/linux-repository/`

Add the official GitLab repository

```
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
```

Install the latest version of GitLab Runner

```
sudo apt install gitlab-runner -y
```

```
gitlab-runner --version
```

### 4. Register gitlab runner with shell executor

go to your gitlab > create a project repo (ex- myproj-on-shellexecutor)

select your project repo > settings > cicd > runner > New project runner > create it 

Copy and paste the following command into your command line to register the runner. EX:-

```
gitlab-runner register  --url https://gitlab.com  --token glrt-UzBlLJdTNiBo80nJlnqpWW86MQpwOjE1Z3R4Ygp0OjMKdTpmcWVxOBg.01.1j0tiimny
```

Enter the GitLab instance URL = https://gitlab.com

Enter a name for the runner = myrunnershell

Enter an executor = shell


check registered runners

```
sudo gitlab-runner list
```

start the runner

```
sudo systemctl enable gitlab-runner
sudo systemctl start gitlab-runner
```

verify status

```
sudo systemctl status gitlab-runner
```

### 5. test runner in gitlab

create `.gitlab-ci.yml`


==========END===========
