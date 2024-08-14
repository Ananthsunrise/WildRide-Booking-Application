# WildRide-Booking-Application
In this, Users can able to book unicorns to their preferred locations for travel. For that they have to go our web page and register and login.Then they can choose their prefered locations via map and unicorn will arrive that location accordingly.

The following AWS Services I used in this project.
1.AWS Amplify(for hosting web page)
2.AWS Cognito(for authentication)
3.AWS Codecommit(having css,html,js files)
4.AWS APi gateway(to build api's to invoke lambda)
5.AWS lambda(to automatically run code)
6.AWS Dynnamodb(to store results)
7.AWS S3(to store code files)


Procedure:  
1.We need to copy html, css , js files from s3 and put it on AWS Codecommit. 
 Go to aws codecommit-create empty repo-add aws codecommitpoweruserpolicy to your IAM user-Generate git credentials for your IAM user to clone repo
 Go to codecomit-click created repo-click clone url and https connections- copy the url
 Open cloudshell- type cloudshell commands which is attched in this git repository.
After executing all commands, files are copied from s3 to aws codecommit.

2.We need to host webpage.
go to aws amplify-click hostapp-click aws codecommit-select repo-enable allow amplify automatically deploy files-save and deploy
copy the url and open in new tab.This is your web page

3.To arrange users to register and login in our web page
go to aws cognito-create userpool-copy userpool id and cient id and paste it on the config.js which is in the aws codecomit.

4.To store rideresults we need dynamodb table.
go to dynamodb-create table- copy the arn of table
go to iam-click role-create new role-selcet lamda-click add permission-select awslambdabasicexecutionrole-create
open the created role-click add permission - click add inline policy- select dynamodb- select putitem action-click add arn-paste the arn of dynamodb table
go to aws lambda- create function-slect node.js 16.x - paste our lamda code in dashboard which is attached in this repo-click deploy
you can also test lambda code by using attched file in this repo

5.we need api gateway url to invoke lambda
go to aws apigateway-create api-select restapi-select edge optimized as endpoint type-create
go to created api-create authorizer-select cognito-select region- create
go to created api-create resource-enable cores-create
go to created api-create method as post-enable proxy integration-selct our lambda function-create
aelect method request-click edit-select cognito-click save
Finally deploy api.copy the url after deploying and paste it on config.js file which is o aws codecomit

Now refresh your webpage and make use on it...
