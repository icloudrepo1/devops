# Simple-declarative pipeline 👇

Declarative is a more recent and advanced implementation of a pipeline as a code.

##### jenkins-file

```
pipeline {
     agent any

     stages {
         stage('Jenkins for DevOps') {
             steps {
                 echo 'Hello World'
             }
         }
     }
 }

```

# steps :

1. Navigate to the Jenkins home page. Create a new Job and select Pipeline.
2. Now configure the project with valid description.
3. Now, navigate to the Pipeline section to write the groovy pipeline code(jenkinsfile)
4. Click on Save and then build now.
5. Let's see the output.

===================END====================================


# Docker-jenkins-declarative-pipeline😎👇

# steps :

1. Install & connect jenkins on your ubuntu system
2. Install docker on your ubuntu system

```
sudo apt install docker.io -y
docker --version
```

3. Apply docker permission

```
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
```
   
4. start Project
   
    - Go to jenkins dashboard
    - Create new item = myproject
    - Select pipeline project
    - Mention github project section = your github repo url
    - Pipeline = use jenkinsfile
    - Build now✌️✌️✌️✌️


##### Jenkins file :- docker deploy


```
pipeline {
    agent any

    stages {
        stage('code clone') {
            steps {
                echo "code cloned successfully"
                git url: "https://github.com/icloudrepo1/jenkins-project-repo.git"
            }
        }
        stage('code build') {
            steps {
                echo "code build successfully"
                sh "docker build . -t myappimg:latest"
            }
        }
        stage('code test') {
            steps {
                echo "code tested successfully"
            }
        }
        stage('code deploy') {
            steps {
                echo "code deployed successfully"
                sh "docker run -itd -p 8000:8000 myappimg:latest"
            }
        }
    }
}

```
=====================END=============================


# Docker-Compose & jenkins-declarative-pipeline 👇

# steps :

1. Install docker-compose on your ubuntu system

```
sudo apt install docker-compose -y
docker-compose --version
```


##### Jenkins file :- docker-compose deploy

create credentials

  - docker-hub username & pw
  - id = dockerHub

    
```
pipeline {
    agent any

    stages {
        stage('code clone') {
            steps {
                echo "code cloned successfully"
                git url: "https://github.com/icloudrepo1/jenkins-project-repo.git"
            }
        }
        stage('code build') {
            steps {
                echo "code build successfully"
                sh "docker build . -t mywebappimg:latest"
            }
        }
        stage('code test') {
            steps {
                echo "code testing successfully"
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag mywebappimg ${env.dockerHubUser}/mywebappimg:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/mywebappimg:latest"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "code deployed successfully"
                sh "docker-compose down && docker-compose up -d"
    }
}


```

===================END====================================
