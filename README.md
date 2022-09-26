# documentation

## Amplify configuration for existing application:

Before start using amplify needs to install aws-amplify module in our directory. run below command

`` npm i -g @aws-amplify/cli ``

Make connection with existing amplify using below command:

`` amplify configure  ``

after successfully configured needs to take amplify pull for that go to amplify in aws console.

console: https://us-east-2.console.aws.amazon.com/amplify/home?region=us-east-2#/

click on the listed app that you want to configure: 

- select the table called Backend enviournment:

  ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/imagecn1.png?raw=true)

- in this picture you can see Back-end environment and then you need to run below amplify command


## Amplify configuration for new application

first you need to create amplify application using below command

  `` npx create-react-app <application name> ``

while running this command you need to enter following details:

  `` Enter a name for the project (application name) ``

  `` Enter a name for the environment (dev) ``

  `` Choose your default editor (VS Code) ``

  `` Choose the type of app that you're building (javascript) ``

  `` What JavaScript framework are you using (react) ``

  `` Source directory path (src) ``

  `` Distribution directory path (build) ``

  `` Build command (npm build) ``

  `` Start command (npm start) ``

  `` Do you want to use an AWS profile (Y) ``

- now amplify application created successfully

- now if you want to add authentication then you need to run below command:

    ``` amplify add auth ```

- if you want to add graphql then you need to run below command

  ``` amplify add api ```
- after adding above command you need to add graphql schema. for that you need to go

  ```  ./amplify/backend/api/<application name>/schema.graphql ```

- Sample model:

    ```
    type Todo @model {
      id: ID!
      name: String!
      done: Boolean!
    }
 
    type TodoList {
      id: ID
      name: String
      done: Boolean
    }
 
    type Query {
      SearchTodo(Word: String): TodoList
    }
    ```
- after this you need to write react code for front-end. then you need to use below command to deploy amplify application.

  ``` amplify push ```

- Once Amplify deployed following resources are created in AWS Console.

 ```
    Amplify Application for UI
    AppSync for GraphQL
    Cognito for Authentication
```

## Lambda Function for AppSync

1. Now you need to create one lambda function that interact with DB. for example:

```
   exports.handler = async (event) => {
       // business logic
       console.log(event['arguments'].Word)
 
       return {id:"46",name:"456",done:"dd"};
   };
```
2. after creating lambda function you need to go to the AWS appSync: 
https://ap-south-1.console.aws.amazon.com/appsync/home?region=ap-south-1#/apis

3. select your API that you have created using amplify.select your API that you have created using amplify.

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/imagecn2.png?raw=true)

4. go to Data Sources.

5. Then create a new data source.

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/imagecn22.1.png?raw=true)

6. Fill all the details with lambda function ARN that you have created recently.

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/2.3.png?raw=true)

7. After adding data source select the schema from left penal.
8. After selecting the schema from right you need to search `query`.

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/2.2.png?raw=true)

9. Then click on attack:

10. Then Click on Create & Save.

11. Now go to the Setting from left penal:

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/2.4.png?raw=true)

12. here you can get your graphQL endpoint.

## Database Connectivity (RDS)

1. Before connect with RDS instance first you need to check ec2 connectivity.

2. for that you need to go the EC2 console and go to the security tab and add your public IP address.

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/Db1.png?raw=true)

3. after Adding IP address you need to verify connection for that you need .pem file to connect ec2 instance.

4. file Name: `` serverless-tunnel.pem``

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/db2.png?raw=true)

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/db3.png?raw=true)

    ![alt text](https://github.com/rahulcapitaln/documentation/blob/main/images/db4.png?raw=true)

5. Now RDS connected Successfully.

## NodeJS Lambda Application Serverless Deployment

### Base Serverless Framework Template

## MUST INSTALL
* install node.js and npm 
* download amazon-cli on youu machine : https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### install serverless globelly
```
 npm i -g serverless
``` 
* fetch User access key,secret key in aws

### Configuration
```
aws configure
```

## CREATE PROJECT
```
serverless create --template aws-nodejs --path YOUR_PROJECT_NAME

cd YOUR_PROJECT_NAME
npm install
```

* For deployment use below command
```
sls deploy -v
```
* for changes only file & you want to deploy single file instead use below command
```
sls deploy -f YOUR_FILE_NAME
```

* for invoke specific files use below command
```
sls invoke -f YOUR_FUNCTION_NAME -l
```

* check logs for file or function
```
sls logs -f YOUR_FILE_NAME -t
```
