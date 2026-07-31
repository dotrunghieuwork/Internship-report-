---
title: Self-Assessment
date: 2026-07-30
weight: 6
chapter: false
pre: <b> 6. </b>
---


## Self-Assessment

During my internship at **Amazon Web Services Viet Nam Company Limited** in the **Workforce Bootcamp - First Cloud AI Journey** program from **20/06/2026 to 31/07/2026**, I had the opportunity to explore the AWS ecosystem, participate in technical events, and directly build a personal project named **NaturEra - Green Banking (A Serverless digital banking application integrated with Carbon footprint calculation)**.

This internship helped me connect my foundational programming knowledge from university with a practical Cloud deployment workflow. I successfully completed the End-to-End process: from the user interface (ReactJS) integrating secure JWT authentication via **AWS Cognito**, routing and handling CORS through **API Gateway**, executing transaction logic with **AWS Lambda**, and persistently storing data on the **DynamoDB** NoSQL database. Additionally, I successfully established system monitoring and log analysis using **Amazon CloudWatch**.

Regarding my work attitude, I implemented the personal architecture while continuously learning through group discussions, AWS Documentation research, and hands-on trial and error. I focused on thoroughly resolving integration issues, optimizing security configurations, maintaining payload transparency, and controlling costs within the allowed resource limits.

## Self-Assessment Criteria

| No. | Criteria | Description | Good | Fair | Average |
|---|---|---|---|---|---|
| 1 | **Professional Knowledge & Skills** | Understanding AWS services, Cloud-native workflow, API integration, and applying them to a real project. | ✅ | ☐ | ☐ |
| 2 | **Learning Ability** | Ability to independently read AWS documentation, analyze CloudWatch logs, and learn from errors (Troubleshooting). | ✅ | ☐ | ☐ |
| 3 | **Proactiveness** | Proactively choosing a practical topic (Green Banking), defining data structures, and independently resolving technical blockers. | ✅ | ☐ | ☐ |
| 4 | **Sense of Responsibility** | Completing the entire E2E workflow, effectively managing AWS resources to control practice costs. | ✅ | ☐ | ☐ |
| 5 | **Discipline** | Sticking to the internship timeline, maintaining the progress of completing each service (Auth, Database, API). | ☐ | ✅ | ☐ |
| 6 | **Progressive Spirit** | Willingness to receive feedback, modify payload logic, and reconfigure the system when security errors arise. | ✅ | ☐ | ☐ |
| 7 | **Communication** | Clearly presenting the architectural flow, technical issues (CORS, Cognito Permission), and their solutions. | ☐ | ✅ | ☐ |
| 8 | **Teamwork** | Actively communicating and analyzing the root causes of complex system errors with the team. | ☐ | ✅ | ☐ |
| 9 | **Professional Demeanor** | Respecting the learning environment, complying with AWS security regulations when setting up permissions (IAM/Cognito). | ✅ | ☐ | ☐ |
| 10 | **Problem Solving Skills** | Thoroughly resolving blockers such as Cognito Attribute write permission errors, 400 Payload Mismatch, and 403 CORS Preflight. | ✅ | ☐ | ☐ |
| 11 | **Contribution to Project/Team** | Successfully building a highly applicable Serverless architecture, preparing transparent and clear project reports. | ✅ | ☐ | ☐ |
| 12 | **Overall Assessment** | General evaluation of learning attitude, problem-solving efforts, and the quality of the completed application during the internship. | ✅ | ☐ | ☐ |

## Strengths

- **Troubleshooting & Self-Learning Skills:** I have the ability to independently analyze CloudWatch logs to catch the exact culprit causing errors rather than guessing.
- **Serverless Technical Implementation:** Mastering and successfully configuring core services. From setting up the App Client in Cognito (granting Write Attributes permissions) to configuring Integration Response Headers (Access-Control-Allow-Origin, Methods, Headers) to overcome CORS security barriers on API Gateway.
- **System Design Thinking:** Ensuring Data Integrity between the producer (Frontend) and consumer (Backend). Clearly understanding the difference between creating a Mock API for UI testing and connecting a Live API to persist hard data into DynamoDB.
- **Patience and Attention to Detail:** Closely following every minor configuration step (such as Deploying the API after every Stage configuration change) to ensure the Cloud system updates its state accurately.

## Areas for Improvement

- **Confidence in Presenting Architecture:** Need to improve verbal communication skills when explaining Technical trade-offs – for example, why JWT Tokens are stored in sessionStorage instead of localStorage, or the logic behind CORS Preflight.
- **Time Management & Initial Setup:** Sometimes spent too much time stuck on permission configuration steps (IAM/Cognito). Need to plan for carefully reading Security Rules Documentation before coding to shorten debugging time.
- **Database Optimization (DynamoDB):** The current project successfully writes data, but to scale, I need to dig deeper into how to design Partition Keys and Sort Keys to optimize query costs.
- **Advanced Endpoint Security:** Need to learn more about Rate Limiting or attaching AWS WAF to the API Gateway to protect the transfer endpoint from the risk of spam requests in a real-world environment.

## Overall Comments

The FCAJ internship helped me realize that building a software system on the Cloud is not just about writing code. A complete Serverless system requires a tight combination of network security setup (CORS), user authentication (Auth), permission management (IAM), API handling, database optimization, and continuous log monitoring.

My most valuable lesson is the skill of connecting the dots between independent Cloud services and troubleshooting mindset. Manually untangling every knot from Frontend to Backend and witnessing transaction data flow seamlessly and store successfully on AWS has helped me clearly shape the mindset of a professional Systems Engineer.