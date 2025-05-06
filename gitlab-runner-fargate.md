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
