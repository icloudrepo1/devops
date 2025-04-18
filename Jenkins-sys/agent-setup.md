# Jenkins agent set-up
===============================


### STEPS

#### 1. create two ec2- instances ( ubuntu )
   
   - ubuntu-24 ami
   - t2.micro
   - keypair = agent_key.pem
   - security group = new security-group ----> all traffic ( anywhere )
   - number of instances ---> 2 ( jenkins-master , jenkins-worker )
   - launch instances

#### 2. connect jenkins-master ec2-instance and install jenkins

   - ( follow , how to install jenkins on ubuntu machine )

     
#### 3. connect jenkins-slave ec2-instance and install java

   - sudo apt update
   - sudo apt install fontconfig openjdk-17-jre -y
   - sudo apt install docker.io -y
   - sudo usermod -aG docker $USER
     
   - sudo reboot


#### 4. Go to jenkins-master ec2-instance

   - ssh-keygen -b 1024 -t rsa
   - cd .ssh
   - ls
   - cat id_rsa.pub ( copy public key )


#### 5. Go to jenkins-slave ec2-instance 

   - vi /home/ubuntu/.ssh/authorized_keys ( paste the public key you copied from Jenkins Master )


#### 6. Go to jenkins-master ec2-instance

   - ssh ubuntu@PUB-IP-SLAVE
   - Are you sure you want to continue connecting (yes/no/[fingerprint])? ------> yes

 ( Now you can access the slave machine )

  - exit


#### 7. Open jenkins for Setting up a Node agent

   - jenkins-master ec2-instance:8080
   - sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   - install suggested plug-ins

   - Go to Manage Jenkins  --->  nodes  --->  New node ---> node name = jenkins agent ( Permanent Agent )  ----> create

   - description = this is jenkins agent as slave  ---->  Remote root directory = /home/ubuntu

   - Labels = jenkins agent   ---->  Launch method = launch agents via ssh  ---> host = slave-node-pub-ip

   - Jenkins Credentials Provider: Jenkins
     
         - ssh user name with pvt key
         - id = key
         - desc. = myslavenode1
         - username = ubuntu
         - pvt key = paste it ( cat id_rsa )

     
   - Host Key Verification Strategy = non verifying

   - save
     


## Running a Pipeline Job for Nodejs App on a Jenkins Agent

In the Jenkins master server, we will define a pipeline and create a job and the execution will be on the agent instance.

### Step 1: Go to your Jenkins Dashboard and click on "Create a Job" or "New Item"

### Step 2: Enter the Job name "agent-project" and select Pipeline

### Step 3: Give the Description and select "GitHub Project"

### Step 4: In the "Project url" section copy the GitHub URL of the project repository and paste it.

`https://github.com/icloudrepo1/jenkins-project-repo.git`

### Step 5: Scroll down to the "Pipeline" section copy this pipeline and paste it in the Pipeline script & build

follow jenkinsfile

### Access the Application in the web browser using SlavePublicip:8000


--------------------------end---------------------------
