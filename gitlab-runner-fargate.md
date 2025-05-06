## steps :-


#### 1. Install Docker

```
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

#### 2. Create a gitlab personal access token

Go to Project(fargate-proj) :- Settings > CI/CD > Runners > New project runner

Tags = mynewtoken1  >  Create Runner

Register runner = Linux

( Copy token > ex- `glrt-U_1HhC3Nk13dYeMq1f8pnW86MQpwOjE1Zzd0MQp0OjMKdTpmcWVxOBg.01.1j0mbss14` )


#### 3. Create ECS Cluster And Fargate Task Defination

Go to ECS -> create cluster -> choose aws fargate as launch type

create task defination = Create task definition with JSON


```
{
  "family": "gitlab-runner",
  "networkMode": "awsvpc",
  "requiresCompatibilities": ["FARGATE"],
  "cpu": "512",
  "memory": "1024",
  "containerDefinitions": [
    {
      "name": "gitlab-runner",
      "image": "gitlab/gitlab-runner:latest",
      "essential": true,
      "environment": [
        { "name": "REGISTRATION_TOKEN", "value": "<Your Runner Token>" },
        { "name": "CI_SERVER_URL", "value": "https://gitlab.com/" }
      ]
    }
  ]
}
```

( Replace: <REGISTRATION_TOKEN> with your actual token )


#### 4. Run the Registration Command

Install GitLab Runner on your system

```
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
sudo chmod +x /usr/local/bin/gitlab-runner
gitlab-runner --version
```

Now, open your terminal and run this full command

```
docker run --rm -it gitlab/gitlab-runner register \
  --non-interactive \
  --url "https://gitlab.com/" \
  --registration-token "<REGISTRATION_TOKEN>" \
  --executor "docker" \
  --docker-image "alpine:latest" \
  --description "fargate-runner" \
  --tag-list "fargate" \
  --run-untagged="true" \
  --locked="false"
```

( Replace: <REGISTRATION_TOKEN> with your actual token )

This will register the runner with GitLab using Docker as the execution environment.
