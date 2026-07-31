---
title : "Setup Backend"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Backend Folder Structure

```bash
naturera-green-banking-backend/
├── events/                   # Contains .json files simulating requests for local testing
├── functions/                # Handler Layer (Entrypoints)
│   ├── dashboard/            # Lambda: Handles GET /dashboard API
│   ├── get-profile/          # Lambda: Handles GET /profile API
│   └── process-transaction/  # Lambda: Handles POST /transactions API
├── src/                      # Business Logic & Database Layer (Shared)
│   ├── configs/              # Environment configurations, constants
│   ├── models/               # Data structure definitions
│   ├── repositories/         # DynamoDB communication layer (Data Access)
│   ├── services/             # Business logic layer (Calculate CO2 points, deduct balance...)
│   └── utils/                # Helper functions (Format response, CORS...)
├── scripts/                  # Contains script files (e.g., seed-data.js)
├── template.yaml             # The heart of SAM: Defines the entire AWS infrastructure
└── package.json              # Library management (aws-sdk, uuid...)
```
## Using SAM CLI to initialize backend

To build the Serverless architecture for the **NaturEra Green Banking** project, we will use the **AWS SAM (Serverless Application Model) CLI**. This is a CLI tool that helps you define, test (locally), and deploy the entire AWS infrastructure (Lambda, API Gateway, DynamoDB, Cognito) in a single command.
```bash
sam version
```
All setup commands, configurations, and templates for AWS Lambda, Cognito, Cloudfront, S3 are written in the template.yaml file.

### Steps to initialize backend using SAM CLI

#### Step 1
Open your terminal in the directory containing project you cloned.
Move to the backend folder
```bash
cd backend
```
#### Step 2
Run the `sam build` command to start the SAM deployment process:
```bash
sam build
```
Then, run the `sam deploy --guided` command to start the deployment process, where you can answer the questions as follows:
```bash
sam deploy --guided
```
At the end of the terminal, you will see the following questions:

 Stack name: naturera-green-banking-dev

 Region: ap-southeast-1 (or 2 depending on your region)
 
 Parameter TableNameParam: NaturEraGreenBankingTable

 Confirm changes before deploy: Y

 Allow SAM CLI to create IAM roles: Y

 Disable rollback: N

 Save parameters: Y

 SAM configuration file: samconfig.toml