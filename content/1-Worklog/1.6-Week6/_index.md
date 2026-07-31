---
title: "Week 6 worklog"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 objectives:
* Develop and deploy frontend components.
* Integrate the frontend with the backend and perform end-to-end testing of the application flow.

### Tasks to be implemented this week:

| Day | Task | Start Date | End Date | References |
| :---: | :--- | :---: | :---: | :--- |
| Mon - Tue | Frontend UI deployment: <br> - Build the React project and upload static files to Amazon S3. <br> - Configure the S3 bucket for static website hosting and distribution via CloudFront. | 07/20/2026 | 07/21/2026 | Project requirements |
| Wed - Thu | Security and monitoring enhancement: <br> - Integrate AWS WAF in front of the API gateway to block malicious traffic. <br> - Configure Amazon CloudWatch for monitoring and log collection. <br> - Create billing alarms and Lambda error alarms. | 07/22/2026 | 07/23/2026 | AWS WAF docs |
| Fri | System-wide testing: <br> - Act as a POS device making real API calls to the system. <br> - Test the token issuance flow from Cognito and the data writing flow to DynamoDB. | 07/24/2026 | 07/24/2026 | API specifications |

### Week 6 achievements:
* The frontend is delivered at high speed via CloudFront with near-zero hosting costs.
* The system achieved enterprise-grade security standards with AWS WAF protection and strict IAM policies.
* Successfully integrated CloudWatch monitoring tools, ready to send automated alerts upon detecting anomalies.