---
title: "Week 5 worklog"
date: 2026-07-13
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 objectives:
* Build an event-driven automation flow using EventBridge.
* Integrate error handling and user authentication mechanisms.

### Tasks to be implemented this week:

| Day | Task | Start Date | End Date | References |
| :---: | :--- | :---: | :---: | :--- |
| Mon - Tue | Monthly task automation: <br> - Configure Amazon EventBridge to trigger a lambda function at 00:00 on the first day of every month. <br> - Write logic to scan users exceeding the CO2 limit to reward trees or unlock cards. | 07/13/2026 | 07/14/2026 | Project requirements |
| Wed - Thu | Error handling setup: <br> - Create an Amazon SQS queue. <br> - Configure SQS as a dead-letter queue (DLQ) to catch failed events from the batch job function. | 07/15/2026 | 07/16/2026 | AWS SQS docs |
| Fri | Authentication integration: <br> - Provision an Amazon Cognito user pool. <br> - Attach a cognito authorizer to API Gateway to protect internal endpoints. | 07/17/2026 | 07/17/2026 | AWS Cognito docs |

### Week 5 achievements:
* Successfully built an event-driven architecture, allowing the system to run background tasks automatically without consuming 24/7 server resources.
* Ensured system reliability by capturing and storing failed requests via SQS DLQ.
* Successfully secured API endpoints, preventing unauthorized access using Cognito.