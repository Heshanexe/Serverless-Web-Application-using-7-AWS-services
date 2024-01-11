**Serverless-Web-Application-using-7-AWS-services**

**Overview**

In this tutorial, I will create a simple serverless web application that enables users 
to request unicorn rides from the Wild Rydes fleet. The application will present users
with an HTML-based user interface for indicating the location where they would like 
to be picked up and will interact with a RESTful web service on the backend to 
submit the request and dispatch a nearby unicorn. The application will also provide 
facilities for users to register with the service and log in before requesting rides.

**Prerequisites**

To complete this tutorial, you will need an AWS account, AWS CLI installed, an 
account with ArcGIS to add mapping to your app, a text editor, and a web browser. 
If you don't already have an AWS account, you can follow the Setting Up Your 
AWS Environment getting started guide for a quick overview.

**Application architecture**

The application architecture uses AWS Lambda, Amazon API Gateway, Amazon DynamoDB, 
Amazon Cognito, and AWS Amplify Console. Amplify Console provides continuous deployment 
and hosting of the static web resources including HTML, CSS, JavaScript, and image 
files which are loaded in the user's browser. JavaScript executed in the browser sends 
and receives data from a public backend API built using Lambda and API Gateway. 
Amazon Cognito provides user management and authentication functions to secure the backend API. 
Finally, DynamoDB provides a persistence layer where data can be stored by the API's Lambda function.

![Serverless_Architecture d930970c77b382db6e0395198aacccd8a27fefb7](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/80da2271-f499-4fce-a96c-1d84402dcf33)

![image](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/f76e0b44-7365-4816-8bbf-36a57a2b5500)


                                     









