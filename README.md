# 🚀 Serverless Contact Form on AWS

A fully serverless contact form application built using Amazon Web Services (AWS). The application allows users to submit messages through a web interface hosted on Amazon S3. The submitted data is processed by AWS Lambda through Amazon API Gateway, stored in Amazon DynamoDB, and an email notification is sent using Amazon Simple Email Service (SES).

---

# 📖 Project Overview

This project demonstrates how to build a complete serverless web application using AWS managed services. Instead of running traditional web servers, AWS services automatically handle hosting, request processing, database storage, and email notifications.

The solution is scalable, cost-effective, and requires no server management.

---

# 🏗️ Project Architecture

```text
               User
                 │
                 ▼
      Amazon S3 Static Website
                 │
                 ▼
      Amazon API Gateway (REST API)
                 │
                 ▼
         AWS Lambda (Python)
        ┌─────────┴─────────┐
        ▼                   ▼
 Amazon DynamoDB       Amazon SES
(Store Submission)    (Send Email)
```

---

# ☁️ AWS Services Used

- Amazon S3
- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB
- Amazon Simple Email Service (SES)
- AWS Identity and Access Management (IAM)
- Amazon CloudWatch

---

# 📂 Project Structure

```text
Serverless-Contact-Form/
│── README.md
│── index.html
│── style.css
│── app.js
│── lambda_function.py
│── assets/
│── images/
```

---

# ⚙️ Implementation Steps

## Step 1 — Create the DynamoDB Table

The first component created was an Amazon DynamoDB table to store every contact form submission.

### Configuration

- Table Name: `ContactFormSubmissions`
- Partition Key: `submission_id`
- Data Type: String

The table stores:

- Submission ID
- Name
- Email
- Subject
- Message
- Submission Date
- Source IP Address

---

## Step 2 — Create the AWS Lambda Function

A Lambda function was created to process incoming requests.

### Configuration

- Function Name: `ContactFormFunction`
- Runtime: Python 3.x
- Architecture: x86_64

The Lambda function acts as the backend of the application.

---

## Step 3 — Configure IAM Permissions

The Lambda execution role was granted permission to interact with AWS services.

The following IAM policies were attached:

- AWSLambdaBasicExecutionRole
- AmazonDynamoDBFullAccess
- AmazonSESFullAccess

These permissions allow Lambda to:

- Write data into DynamoDB.
- Send email notifications through Amazon SES.
- Generate CloudWatch logs.

---

## Step 4 — Develop the Lambda Function

The Lambda function was written in Python.

The function performs the following tasks:

- Receives HTTP POST requests.
- Reads JSON data from API Gateway.
- Validates user input.
- Generates a unique submission ID.
- Saves the data into DynamoDB.
- Sends an email notification using Amazon SES.
- Returns a JSON response to the frontend.

### Input Validation

The application validates:

- Name
- Email
- Subject
- Message

Email addresses are validated using a regular expression before processing.

---

## Step 5 — Configure Amazon SES

Amazon Simple Email Service (SES) was configured to send email notifications.

Configuration included:

- Verifying the sender email address.
- Configuring the recipient email address.
- Testing email delivery.
- Using the same AWS Region as the Lambda function.

---

## Step 6 — Create the REST API

A REST API was created using Amazon API Gateway.

### API Configuration

API Name:

```
ContactFormAPI
```

Endpoint Type:

```
Regional
```

Created Resource:

```
/contact
```

Methods:

- POST
- OPTIONS (CORS)

The POST method was integrated with the Lambda function using Lambda Proxy Integration.

---

## Step 7 — Deploy the REST API

The API was deployed using a deployment stage.

### Stage Name

```
prod
```

Deployment generated the API Invoke URL used by the frontend.

---

## Step 8 — Host the Website on Amazon S3

A static website was hosted using Amazon S3.

### Bucket Name

```
godfrey-contact-website-2026
```

Configuration included:

- Static Website Hosting
- Public Read Access
- Bucket Policy
- Index Document
- Uploading HTML, CSS, JavaScript, and asset files

---

## Step 9 — Configure Static Website Hosting

Static Website Hosting was enabled.

Configuration:

- Hosting Enabled
- Index Document:

```
index.html
```

- Error Document:

```
index.html
```

Amazon S3 generated a Website Endpoint used to access the application.

---

## Step 10 — Connect the Frontend

The JavaScript frontend was updated to communicate with the deployed REST API.

Configuration:

```javascript
const API_URL = "https://izb1j1g2sj.execute-api.us-east-1.amazonaws.com/prod";
```

Every form submission is sent to:

```
POST /contact
```

through Amazon API Gateway.

---

# 🧪 Application Testing

The complete application was tested successfully.

Testing included:

- Opening the hosted website.
- Entering contact information.
- Submitting the contact form.
- Verifying API Gateway request processing.
- Confirming Lambda execution.
- Confirming data storage in DynamoDB.
- Confirming email delivery through Amazon SES.
- Verifying successful responses on the frontend.

---

# 📊 Workflow

```text
User submits contact form
          │
          ▼
Amazon S3 Website
          │
          ▼
Amazon API Gateway
          │
          ▼
AWS Lambda
     ┌──────────────┴──────────────┐
     ▼                             ▼
Amazon DynamoDB             Amazon SES
(Store Data)             (Send Notification)
```

---

# ✅ Project Outcome

The project successfully demonstrates a complete serverless architecture capable of:

- Hosting a static website.
- Receiving user input.
- Processing requests through AWS Lambda.
- Storing records in DynamoDB.
- Sending email notifications using Amazon SES.
- Returning responses through API Gateway.

The solution eliminates the need to provision or manage traditional servers while providing a scalable and reliable architecture.

---

# 💡 Skills Demonstrated

- AWS Lambda
- Amazon API Gateway
- Amazon S3 Static Website Hosting
- Amazon DynamoDB
- Amazon SES
- AWS IAM
- Amazon CloudWatch
- REST API Development
- Python Backend Development
- Serverless Computing
- Cloud Application Deployment
- Input Validation
- CORS Configuration

---

# 📚 Technologies Used

- Python
- HTML5
- CSS3
- JavaScript
- AWS Lambda
- Amazon S3
- Amazon API Gateway
- Amazon DynamoDB
- Amazon SES
- AWS IAM

---

# 🔮 Future Improvements

Potential enhancements include:

- Sending confirmation emails to users.
- Adding CAPTCHA for spam prevention.
- Implementing authentication.
- Restricting CORS to specific domains.
- Adding CloudWatch dashboards and alarms.
- Creating a custom domain with HTTPS using Amazon CloudFront and AWS Certificate Manager (ACM).

---

# 📄 Conclusion

This project demonstrates the successful design and implementation of a serverless contact form application using AWS managed services. By integrating Amazon S3, API Gateway, AWS Lambda, DynamoDB, and Amazon SES, the application provides a scalable, secure, and cost-effective solution for processing contact form submissions without requiring traditional server infrastructure.