---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# NaturEra Platform - Green Banking Model
## Unified AWS Serverless Solution for Banking Transaction Processing with CO2 Footprint Calculation

### 1. Executive Summary
NaturEra is a Green Banking module designed by team *, serving as an integrated extension layer for an existing Core Banking system. It automatically calculates the CO2 emissions generated from each POS card transaction, enforces real-time monthly carbon limits, and encourages eco-friendly spending behavior through end-of-month reward mechanisms. The platform aims to transform daily spending data into a tool for environmental awareness without requiring customers to manually enter data or use any third-party applications.

### 2. Problem Statement
*Current Problem*
Environmental protection is an urgent global issue. In the banking industry, the Green Banking model conveys a mission-driven message of environmental protection through financial transactions. However, in Vietnam, this model is not yet widespread, and very few banks have actually implemented it. Current banks do not provide customers with visibility into the environmental impact of their spending habits. Third-party carbon tracking applications exist independently of actual banking data, forcing users to manually input data, lacking accuracy, and offering no binding or incentive mechanisms linked to real cash flows.

*Solution*
NaturEra integrates directly into the POS transaction processing flow: with each card swipe, the system automatically looks up the emission factor based on the merchant's MCC code, calculates the corresponding amount of CO2, and accumulates it into the customer's monthly carbon limit in a single data-writing operation alongside the money deduction — ensuring absolute consistency between account balances and carbon figures without needing complex orchestration infrastructure (such as Saga or Step Functions). When a customer exceeds their limit, the card is automatically locked immediately to create an instant reminder; at the end of each month, the system automatically unlocks cards and evaluates rewards for customers with low emissions.

### 3. Solution Architecture
The platform adopts a fully AWS-native Serverless architecture:
* **AWS Cognito**: Manages access permissions for user pools: users, staff, admins.
* **AWS Lambda**: Core logic operations handled by Lambda functions to execute model tasks, including:
    * **Transaction Interceptor API** — Receives POS transactions, calculates CO2 based on MCC, deducts funds + logs transaction + accumulates CO2, and checks card lock status within a single atomic `TransactWriteItems` operation (response SLA under 2 seconds).
    * **Dashboard API** — Returns carbon chart data categorized for the customer application.
    * **Green Profile & Card API** — Allows customers to view their environmental profile and manage card status.
    * **Admin Rule Config API** — Allows bank staff (ADMIN role) to update CO2 emission factors by MCC and display category dictionaries without redeploying the system.
    * **Special Task Lambdas** — Handles specialized tasks (monthly batch, log metrics, etc.).
* **AWS S3**: Hosts static frontend web assets for CloudFront.
* **AWS CloudFront**: Delivers static web content securely via HTTPS.
* **AWS Amplify**: npm backend library connecting to AWS API Gateway and AWS Cognito to build the frontend.
* **AWS API Gateway**: Handles incoming requests from the frontend and routes them to Lambda functions.
* **AWS DynamoDB**: Stores all data for the model.

<img src="/images/5-Workshop/5.1-Workshop-overview/naturera_architecture.jpg" width="80%" />

### 4. Technical Implementation
*Implementation Stages*
The project was implemented within the framework of the FCAJ internship, with an MVP delivery timeline of 1 month, divided into 4 stages:
1. *Architecture Design*: Identified 7 Lambda functions, designed the single-table DynamoDB schema, and established architectural decision records (ADR-001/ADR-002/ADR-003).
2. *Core Transaction Engine*: Developed the Transaction Interceptor using `TransactWriteItems` and real-time card locking mechanisms.
3. *Admin & Reporting Layer*: Built Admin Rule Config API, Dashboard API, and Monthly Offset Batch Job.
4. *Testing & Deployment*: Wrote mock tests for each layer (model/service/repository), configured least-privilege IAM policies, and deployed via AWS SAM.

*Technologies and Tools Used*
* AWS Services: AWS Lambda, AWS API Gateway, AWS S3, AWS CloudFront, AWS Amplify, AWS Cognito, AWS DynamoDB.
* AWS Tools: AWS SAM, AWS CDK, AWS CLI, AWS CloudFormation.
* Programming Languages & Frameworks: Node.js 20.x, JavaScript ES2020+, React + Vite + TailwindCSS.

### 5. Roadmap & Implementation Milestones
- *Pre-internship (Month 0)*: 1 month of planning and legacy evaluation.
- *Internship (Months 1–3)*:
    - Month 1: Learn AWS services and upgrade hardware/environment.
    - Month 2: Design and refine architecture.
    - Month 3: Implementation, testing, and deployment.
- *Post-deployment*: Continued research over the next year.

### 6. Budget Estimation
Costs are separated into two tiers due to fundamentally different operational purposes: *Workshop/Demo Tier* (for technical presentation with dozens of test transactions) and *Production Tier* (simulating real bank operation with 1,000 active users).

*6.1. Workshop/Demo Tier (Current MVP)*
At demo scale (a few dozen test transactions during presentations), almost all costs fall within the permanent AWS Free Tier for AWS Lambda (1 million requests/month) and Cognito (50,000 MAUs) — total actual cost is below ~$1 USD/month.

*6.2. Production Tier (~1,000 Active Users)*
Assuming each user performs ~30 POS transactions/month (~1 transaction/day) and checks the Dashboard ~10 times/month — estimated total workload is ~80,000 Lambda invocations/month and ~240,000 DynamoDB WCUs/month (since `TransactWriteItems` consumes double the write capacity compared to standard writes for each item in an atomic transaction).

| Service | Estimated Volume | Monthly Cost |
|---|---|---|
| AWS Lambda | ~80,000 invocations (Interceptor, Dashboard, Card, Aggregator, Batch) | $0.00 USD *(within permanent free tier)* |
| Amazon DynamoDB (On-Demand) | ~240,000 WCU + ~55,000 RCU | ~$0.50 USD |
| Amazon API Gateway (REST) | ~45,000 requests | ~$0.20 USD |
| Amazon Cognito | 1,000 MAUs | $0.00 USD *(free tier up to 50,000 MAUs)* |
| Amazon CloudWatch (Logs + Alarms) | Application logs + budget alarms | ~$0.30 USD |
| Amazon SNS (Push Notifications) | Limit warnings, card lock/unlock alerts | ~$0.05 USD |
| AWS WAF *(Recommended for financial APIs)* | Web ACL + basic rules | ~$7.00 USD |
| Amazon Route 53 *(Custom domain, optional)* | Hosted zone + query requests | ~$0.80 USD |

*Total Estimated Cost*: ~$8.85 USD/month at a scale of 1,000 active users, including AWS WAF protection — a strongly recommended mandatory security component for any financial transaction API before going into production.

*Why this is significantly lower than AI-native platforms (e.g., ~$60 USD/month for 1,000 users in models with Generative AI integration):* The Green Banking architecture involves zero AI/ML inference calls (no Amazon Bedrock, no ECS Fargate for Vision AI processing, no NAT Gateway for services outside VPC) — the entire business logic consists of CO2 calculations and structured data operations, which are inherently much cheaper than language or vision model inferences. This is a key architectural advantage worth highlighting in the cost comparison section of the report, not a calculation oversight or omission.
* Note: The table above provides estimates at the time of writing; actual costs may vary over time.

### 7. Risk Assessment

**Risk Matrix & Mitigation Strategies**

| Risk Group | Risk Description | Severity | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **Integration & Business Logic** | Third-party APIs (VISA/Core Banking) respond slowly or go offline. | Medium | Apply Adapter Pattern and asynchronous processing (EventBridge/SQS) to prevent system blocking. |
| **Security & Compliance** | Cyberattacks (DDoS) or stolen JWT tokens. | High | Delegate identity management to AWS Cognito. Protect APIs using AWS WAF and configure API Gateway Throttling. |
| **Financial & Budget** | Code errors (infinite loops) or API spamming lead to surging AWS costs. | High | Set up AWS Budgets Alerts (triggers when exceeding $5/month) and apply Usage Plans with API Keys for POS terminals. |
| **Data Integrity** | Floating-point errors or network dropouts cause accounting mismatches. | Very High | Enforce integer formatting for monetary amounts. Mandate DynamoDB Transactions (`TransactWriteItems`) to guarantee ACID properties. |

### 8. Expected Outcomes

*Demo Product*: A complete flow from POS card swipe transaction → automatic CO2 calculation → monthly limit accumulation → real-time card locking upon limit breach → automatic unlocking and rewards evaluation at the start of the next month, along with a dashboard displaying carbon footprints categorized for customers.

*Technical Development*: Production-ready completion, with potential contract integrations with real banks for future standard KYB and KYC transaction deployment.

*Long-term Value*: Demonstrates serverless architecture design capabilities for financial systems — from architectural trade-off evaluations (ADRs) and NoSQL single-table data design to least-privilege security principles — making it ideal content for portfolio (CV) and internship graduation reports.