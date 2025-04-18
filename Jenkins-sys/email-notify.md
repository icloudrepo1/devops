# Jenkins email notification
========================================

#### step-1 :- create an ec2-instance ( ubuntu ) & install jenkins on it

#### step-2 :- go to jenkins dashboard  -->  manage jenkins  --> plug-ins -->  installed plug-ins  --> ( Email Extension plugins ) ,,, if not then install


#### step-3 :- go to gmail & enable 2-step verification  --> go to home  --> search `app passwords`  --> app name = Jenkins ---> create  --> copy pw

  - go to manage jenkins  --> Credentials  --> add Credentials

        - Kind = username & password
        - Username = use your gmail id
        - password = use your app password
        - ID = mygmail
        - Description = gmail app pw
        - create
    
( Credentials created successfully )
               - 
     
#### step-4 :- go to manage jenkins  --> system  --> scroll down & go to `Extended E-mail Notification`

  - SMTP server  = smtp.gmail.com
  - SMTP Port  = 465
  - Go to advance  --> Credentials = use your created Credentials
  - Use SSL  = allow
  - Default Recipients  = use your gmail add

  - `scroll down & go to E-mail Notification`
    
        - SMTP server  = smtp.gmail.com
    
        - click advanced  -->  Use SMTP Authentication  -->  User Name = your gmail add   -->  Password  = use your app password
        - SMTP Port = 465
        - Test e-mail recipient  = your gmail add ( test it )
    

  - save
    

#### step-5 :- create a pipeline project

  - new item  --->  Enter an item name = mymail-notification-proj  ---> select pipeline

  - go to pipeline and paste below script  and save it , then `build now`

```
pipeline {
      agent any
      stages {
          stage('Build') {
              steps {
                  echo 'Building...'
              }
          }
          stage('Test') {
              steps {
                  echo 'Testing...'
              }
          }
          stage('Deploy') {
              steps {
                  echo 'Deploying...'
              }
          }
      }
      post {
          success {
              emailext (
                  to: 'cloud90807060@gmail.com',
                  subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                  body: """<p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' succeeded.</p><p>Check console output at <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
                  mimeType: 'text/html'
              )
          }
          failure {
              emailext (
                  to: 'cloud90807060@gmail.com',
                  subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                  body: """<p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' failed.</p><p>Check console output at <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
                  mimeType: 'text/html'
              )
          }
      }
  }
```


- go to mail and check it



=========================================end====================================
