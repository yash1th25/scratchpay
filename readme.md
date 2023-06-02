# Create and Deploy an API

## Task 1: API

To verify the competency in writing code.

You will find a [swagger spec](https://gitlab.scratchpay.com/-/snippets/42/raw/main/swagger.yaml) defining an API that you must create. It is a simple user system with a single endpoint. Please use the specification and write an API in the language of your choosing. Keep in mind that you will need to store the user information.

### Process

* Created springboot application and pushed it to github (https://github.com/yash1th25/scratchpay) 

* To run it in your local, you can download it by cloning the directory to your local using git clone
  
  ```gh repo clone yash1th25/scratchpay```

* As a pre-req make sure to install and configure a database. Configure the database properties under src/main/resources/application.properties. 
  In my case I took a postgres docker image and deployed it on my environment
   
  Below are the command to run the docker image and execute the sql scripts to create schemas on postgres
  1. To download the postgres image from dockerhub
     
     ```docker pull postgres```
      
  2. Run the postgres container as below 
     
     ```docker container run --name postgresdb -e POSTGRES_PASSWORD=admin -d -p 5432:5432 postgres```
     
     --name - Assign a name to the container
     
     -e - to set the environmental variables
     
     -d - Run container in background and print container ID
     
     -p - Publish a container’s port(s) to the host
     
   
  3. Go to the python_database_scripts folder and run the below command to copy the userdb.sql file to the postgres container
     
     ```docker cp userdb.sql postgresdb:/```
   
  4. To execute the script in the docker container
     
     ```docker exec -it postgresdb psql -U postgres -f userdb.sql```

* To build the code, use the below commands
  
  ```./mvnw clean install```

* To run the application
  
  ```java -jar ./target/restapi-0.0.1-SNAPSHOT.jar```

* To hit the below APIs, you can use something like postman to test.

  POST - http://localhost:8080/v1/users (To create the users)
  
  ![alt text] (https://github.com/yash1th25/scratchpay/blob/main/images/postman.jpeg)
  
  GET - http://localhost:8080/v1/users (To fetch all user details)
  
  GET - http://localhost:8080/v1/users/{id} (To fetch particular user)

## Task 2: Local Setup

This step is to verify your competency in setting up a development workflow.

Create a local environment that can be used to verify the code. Please keep in mind that a large number of projects are done with various setups (Unix and Windows based), so on any local setup please take into consideration this limitation (i.e. make sure it works across platforms). There is a [CSV](https://gitlab.scratchpay.com/-/snippets/42/raw/main/data.csv) file containing data that should be loaded in order to test your setup. Please think of a creative way to make loading the data easier.

## Task 3: Containerization and Orchestration

This step is to test your understanding of containerization, automation and orchestration.

Please containerize your application and create the required manifests/configuration to deploy your application to a Kubernetes cluster. Please use best practices when setting this up (treat it as if it were going into production). Part of the process should include the automation of loading the data into the storage that you have chosen.

_NB:_ Scratchpay is a Fintech company, so while we believe in innovation, this should not be at the cost of compromising on security.