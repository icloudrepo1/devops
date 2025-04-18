# Jenkins Install & Set up on Ubuntu
=============================================

### 1. Create an ubuntu instance & Connect

AMI = Ubuntu , Instance types = T2.micro , Keypair = jenkinskey.pem , SG = All traffic (Anywhere)


### 2. Installation of Java

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
java --version
```


### 3. Installation of Jenkins

Follow this 👉 https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null


sudo apt-get update

sudo apt-get install jenkins -y
jenkins --version
```


### 4. How to connect(login) Jenkins

A. copy Your system (instance) public-ip & paste it on browser

ex = 65.0.139.252:8080

B. 

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

copy password & paste it on Administrator password

C. Customize Jenkins

install suggested plug-ins


### 5. Access Jenkins Now

Create First Admin User 

( Update info ) and Start using Jenkins

=================END===========================================



# Jenkins Install & Set up on Windows
==============================================

#### 1. Download java

`https://www.oracle.com/in/java/technologies/downloads/#jdk21-windows`

Install java

`java --version`

#### 2. Download Jenkins

`https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/`

Install


`login and access` =====>  `localhost:8080`
