---
title: "Week 4 worklog"
date: 2026-07-06
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 objectives:
* Establish the foundational infrastructure for the final project.
* Apply AWS SAM (IaC) to build APIs and handle data integrity.

### Tasks to be implemented this week:

| Day | Task | Start Date | End Date | References |
| :---: | :--- | :---: | :---: | :--- |
| Mon - Tue | Project initialization with AWS SAM: <br> - Write the template.yaml configuration for Lambda functions and API Gateway. <br> - Set up DynamoDB tables for storing transaction history and user profiles. | 07/06/2026 | 07/07/2026 | AWS SAM docs |
| Wed - Thu | Core logic programming: <br> - Code the transaction interceptor function to process POS transactions. <br> - Implement the transact write items feature in DynamoDB to prevent race conditions when deducting balance and adding CO2. | 07/08/2026 | 07/09/2026 | Project requirements |
| Fri | Security and connection troubleshooting: <br> - Configure IAM policies following the principle of least privilege for Lambda. <br> - Resolve CORS errors when calling the API from a local environment. | 07/10/2026 | 07/10/2026 | AWS IAM docs |

### Week 4 achievements:
* Introduced infrastructure as code (IaC) into the project using AWS SAM, enabling fully automated builds and deployments.
* Successfully solved the race condition issue in financial transactions using DynamoDB's atomic transactions.
* Completely resolved CORS errors and established secure IAM permissions for the backend system.