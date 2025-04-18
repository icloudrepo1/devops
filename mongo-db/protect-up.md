### install

```
apt install docker.io -y
apt install docker-compose -y
```

```
apt install aws-cli -y
```

```
apt install jq -y
```


## steps:


1. Go to aws secrets manager
2. click store a new secret    ------>   Secret type  = Other type of secret
3. add key-value pairs (plain-text)

```
{
  "username": "devbabu",
  "password": "devbabu123"
}
```

(YOU CAN USE `"database": "mydb"`)

4. next
5. Secret name = mongo/root/creds
6. next
7. store

8. Set Up an IAM Role or Access Credentials (To allow your app or script to access the secret, you need) :- 

   - An IAM role (if running in ECS/EC2)
   - Or AWS access keys (if running locally)    -----> `vi .aws/credentials`
  
     

9. AWS Secrets Manager isn’t directly supported in `docker-compose.yml`, so you can use a startup `script` to fetch the secrets and pass them as environment variables.


vi mystart.sh

```
#!/bin/bash

# Fetch credentials from AWS Secrets Manager
SECRET_JSON=$(aws secretsmanager get-secret-value --secret-id mongo/root/creds --query SecretString --output text)

export MONGO_USER=$(echo $SECRET_JSON | jq -r .username)
export MONGO_PASS=$(echo $SECRET_JSON | jq -r .password)

# Start Docker Compose
docker-compose up -d

```

(YOU CAN USE `export MONGO_DB=$(echo $SECRET_JSON | jq -r .database)`)

`chmod +x mystart.sh`



10. vi docker-compose.yml


```
version: '3.8'

services:
  mongodb:
    image: mongo:latest
    container_name: mongo-container
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USER}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASS}
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:

```

(YOU CAN USE `MONGO_INITDB_ROOT_DATABASE: ${MONGO_DATABASE}`)

`docker-compose up -d`

`docker-compose ps`


11. Connect to MongoDB
    
```
mongosh
```

12. List all databases
    
```
show dbs
```

13. Switch to / create a database

```
use mydb
```

14. Show current database

```
db
```

15. Delete the current database

```
db.dropDatabase()
```
=============END===================
