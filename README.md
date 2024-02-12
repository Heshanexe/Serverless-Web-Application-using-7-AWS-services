**Serverless-Web-Application-using-7-AWS-services**

**Overview**

As my first AWS Cloud Project, I will create a simple serverless web application that enables users 
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




**STEP 01**

**Overview**

In this module, you will configure AWS Amplify to host the static resources for your 
web application with continuous deployment built in. The Amplify Console provides 
a git-based workflow for continuous deployment and hosting of full-stack web apps. 
In subsequent modules, you will add dynamic functionality to these pages using 
JavaScript to call remote RESTful APIs built with AWS Lambda and Amazon API Gateway.


**Architecture overview**

![image](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/78b48017-e51e-44d1-ba76-b2ce09a3112d)


The architecture for this module is straightforward. All of your static web content 
including HTML, CSS, JavaScript, images, and other files will be managed by AWS
Amplify Console. Your end users will then access your site using the public website 
URL exposed by AWS Amplify Console. You don't need to run any web servers or use 
other services to make your site available.

For most real applications you'll want to use a custom domain to host your site. If 
you're interested in using your own domain, follow the instructions for setting up a 
custom domain on Amplify.




**STEP 02**

**Overview**


In this module you'll create an Amazon Cognito user pool to manage your users' 
accounts. You'll deploy pages that enable customers to register as a new user, verify 
their email address, and sign into the site.

**Architecture overview**

![image](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/579f392c-59bd-471f-86f2-bdde6d315bff)


When users visit your website they will first register a new user account. For the 
purposes of this workshop we'll only require them to provide an email address and 
password to register. However, you can configure Amazon Cognito to require 
additional attributes in your own applications.

After users submit their registration, Amazon Cognito will send a confirmation email 
with a verification code to the address they provided. To confirm their account, users
will return to your site and enter their email address and the verification code they 
received. You can also confirm user accounts using the Amazon Cognito console with 
a fake email addresses for testing.

After users have a confirmed account (either using the email verification process or a 
manual confirmation through the console), they will be able to sign in. When users
sign in, they enter their username (or email) and password. A JavaScript function 
then communicates with Amazon Cognito, authenticates using the Secure Remote 
Password protocol (SRP), and receives back a set of JSON Web Tokens (JWT). The 
JWTs contain claims about the identity of the user and will be used in the next 
module to authenticate against the RESTful API you build with Amazon API Gateway.




**STEP 03**

**Overview** 


In this module, you will use AWS Lambda and Amazon DynamoDB to build a backend 
process for handling requests for your web application. The browser application that
you deployed in the first module allows users to request that a unicorn be sent to a 
location of their choice. To fulfill those requests, the 
JavaScript running in the browser will need to invoke a service running in the cloud.


**Architecture overview**


![image](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/35476a29-f686-4c53-9ac9-3705a0ab2c8e)


You will implement a Lambda function that will be invoked each time a user requests 
a unicorn. The function will select a unicorn from the fleet, record the request in a 
DynamoDB table, and then respond to the frontend application with details about 
the unicorn being dispatched.

The function is invoked from the browser using Amazon API Gateway. You'll 
implement that connection in the next module. For this module, you will just test your function in isolation.


**STEP 04**

**Overview**


In this module, you will use Amazon API Gateway to expose the Lambda function you 
built in the previous module as a RESTful API. This API will be accessible on the 
public Internet. It will be secured using the Amazon Cognito user pool you created in 
the previous module. Using this configuration, you will then turn your statically 
hosted website into a dynamic web application by adding client-side JavaScript that 
makes AJAX calls to the exposed APIs.


**Architecture overview**

![image](https://github.com/Heshanexe/Serverless-Web-Application-using-7-AWS-services/assets/153348700/793a45d0-ffbb-43ec-b154-4579b84544ad)


The diagram above shows how the API Gateway component you will build in this 
module integrates with the existing components you built previously. The grayed out 
items are pieces you have already implemented in previous steps.

The static website you deployed in the first module already has a page configured to 
interact with the API you will build in this module. The page at /ride.html has a 
simple map-based interface for requesting a unicorn ride. After authenticating using 
the /signin.html page, your users will be able to select their pickup location by 
clicking a point on the map and then requesting a ride by choosing the 
"Request Unicorn" button in the upper right corner.

This module will focus on the steps required to build the cloud components of the 
API, but if you're interested in how the browser code works that calls this API, you 
can inspect the ride.js file of the website. In this case, the application uses jQuery's 
ajax() method to make the remote request.



