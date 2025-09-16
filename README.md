#aws-Lambda

****Build a Serverless CRUD Microservice with API Gateway, Lambda, DynamoDB, and Python****


This project implements an AWS Lambda function that serves a simple contact form page and processes form submissions using DynamoDB as the backend.

📌 Features

GET Request → Serves the contactus.html page.

POST Request → Stores submitted form data into a DynamoDB table and serves a success.html page.

Handles errors gracefully with meaningful HTTP responses.



📂 Project Structure


├── lambda_function.py   # Main Lambda function 
├── contactus.html       # Contact form HTML page
├── success.html         # Success confirmation HTML page
└── README.md            # Documentation



  ⚙️ How It Works


Lambda Entry Point → lambda_handler(event, context)

Routes the request to page_router() based on HTTP method.

GET /contactus

Returns contactus.html with Content-Type: text/html.

POST /contactus

Parses form body and inserts data into DynamoDB using PartiQL (execute_statement).

Returns success.html page if the insertion succeeds.

Error Handling

Returns 500 Internal Server Error with details in JSON format if any step fails.



🛠️ Setup Instructions


1. Create a DynamoDB Table

Table Name: lambdamd

Make sure it supports execute_statement (PartiQL).

2. Package the Lambda Deployment

Zip the Lambda code and HTML files:

zip -r lambda_package.zip lambda_function.py contactus.html success.html

3. Deploy to AWS Lambda

Go to AWS Lambda Console.

Create a function (Python 3.x runtime).

Upload lambda_package.zip.

Configure an API Gateway trigger for the Lambda function.

4. IAM Permissions

The Lambda function requires DynamoDB permissions:

{
  "Effect": "Allow",
  "Action": [
    "dynamodb:ExecuteStatement"
  ],
  "Resource": "*"
}


Attach this policy to the Lambda execution role.

📤 API Usage
GET Request
GET /contactus


Response: contactus.html

POST Request
POST /contactus
Content-Type: application/x-www-form-urlencoded

name=John+Doe&email=john@example.com&message=Hello


Response: success.html
