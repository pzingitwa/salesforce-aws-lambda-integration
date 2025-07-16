# Salesforce + AWS Lambda Integration

This project demonstrates how to integrate Salesforce with AWS Lambda via API Gateway.  
When a custom button or Apex trigger in Salesforce is clicked, it sends record data (e.g. from a Case object) to a Lambda function, which processes the data and returns a response.

# Tech Stack**
- **Salesforce:** Apex HTTP Callout, Named Credentials
- **AWS:** Lambda, API Gateway, API Key for security
- **Tools:** Postman, GitHub

## ⚙️ **How it Works**
1. Salesforce sends a POST request (via Apex callout) to API Gateway.
2. API Gateway triggers the Lambda function.
3. Lambda processes the data and sends back a response.
4. Response is logged in Salesforce debug logs (can be extended to update records).

## 🔑 **Security**
- API Gateway secured with an API Key.
- Key is passed as a header (`x-api-key`) from Salesforce.

## 🪜 **Setup Guide**

1️⃣ AWS Lambda
- Create a Lambda function (Python or Node.js)
- Sample code:
```python
import json

def lambda_handler(event, context):
    print("Received:", event)
    return {
        'statusCode': 200,
        'body': json.dumps({'message': 'Success'})
    }

2️⃣ API Gateway
Create HTTP API → route: POST /salesforce

Integration target: your Lambda function

Deploy and copy the Invoke URL

3️⃣ API Key
Create API Key → attach to Usage Plan → link to your API

Copy the key for use in Salesforce

4️⃣ Salesforce
Create Named Credential:

URL: your API Gateway Invoke URL

Identity Type: Anonymous

Authentication Protocol: None

Add Apex class LambdaCallout to make the callout

## 🧪 Sample Lambda Output
```json
{
  "message": "Success from Lambda"
}

Screenshots

1. Salesforce Custom Button
<img width="1817" height="564" alt="Success callout - sf" src="https://github.com/user-attachments/assets/2f903a86-7fa6-463d-8fb2-e5a20eea879d" />
<img width="1364" height="412" alt="Screenshot (42)" src="https://github.com/user-attachments/assets/64fe1b52-21a8-4a5c-862a-b57fa4e8af6c" />


2. Lambda Console Logs
<img width="1796" height="755" alt="Screenshot (35)" src="https://github.com/user-attachments/assets/e4251270-35b0-47e0-98f9-f28b5dfbc161" />

<img width="1850" height="723" alt="CloudWatch Logs" src="https://github.com/user-attachments/assets/7e939621-8fd3-44a8-833f-d9fa047e32ff" />

3. Named Credentials
<img width="1422" height="652" alt="Named credential setup" src="https://github.com/user-attachments/assets/bbd54ff9-0202-49f8-85f1-4fc50c94e9d4" />

4. API Gateway
<img width="972" height="464" alt="routes" src="https://github.com/user-attachments/assets/81a8da34-e5e4-4536-bae6-aaf66ae42937" />
 Route

✅ What I Learned
	•	How to create secure Apex callouts to external APIs
	•	How to expose and secure a Lambda function using API Gateway
	•	Real-world integration patterns between CRM and Cloud
	•	Hands-on debugging across two cloud platforms

