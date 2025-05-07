## deploy a shell executor on AWS
==========================================

1. launch instance > ubuntu
2. connect it and run below commands

 ```
 sudo apt update
 ```


3. Install GitLab Runner


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

