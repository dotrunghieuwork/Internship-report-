---
title: "Blog 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# HANDLING RACE CONDITIONS IN A SERVERLESS TRANSACTION SYSTEM WITH AMAZON DYNAMODB

Hello everyone in the group,

During the past week, while working on the NaturEra Green Banking internship project on AWS, our team encountered a classic yet fascinating problem when dealing with distributed systems: The Race Condition.

### The Problem
The core feature of our project is that upon a user's payment, the system deducts money from their wallet and simultaneously adds a specific amount of "Carbon Credits" (CO2) to their profile. Everything worked perfectly when testing individual requests. However, when we load-tested by sending multiple requests at the exact same millisecond, the issue surfaced.

### The Root Cause
With a Serverless architecture, AWS API Gateway automatically scales and invokes multiple Lambda functions to run in parallel. 
* Suppose a user's wallet has 100k. Two payment requests for 50k arrive simultaneously.
* Two independent Lambda functions read the database at the exact same time and both see a balance of 100k.
* Both execute the deduction and overwrite the database with the new balance of 50k.
* The Consequence: The user successfully completes two transactions but is only charged for one.

### Our Solution
Initially, the team considered using application-level code to lock the execution thread. However, since Serverless functions run completely independently and are stateless, this approach was unfeasible. We decided to offload the responsibility of data integrity to the Database tier (Amazon DynamoDB).

Our team applied a combination of two DynamoDB mechanisms:
* **ConditionExpression:** When updating the balance, we attached a conditional check (e.g., `ConditionExpression: "Balance >= :cost"`). DynamoDB grants permission to the first request that arrives. The concurrent request arriving moments later is immediately rejected with a `ConditionalCheckFailedException` because the balance condition is no longer met.
* **TransactWriteItems:** To ensure that the money deduction and the Carbon Credit addition always occur together, we bundled both into a single Transaction. If one operation fails, the entire process is automatically rolled back, ensuring the system never enters an inconsistent data state.

### System Architecture
* Infrastructure as Code (IaC): AWS SAM
* Backend: AWS Lambda, Amazon API Gateway
* Database: Amazon DynamoDB

### Key Takeaways
* Do not handle synchronization via application code when building Serverless systems.
* DynamoDB is not just great for storage; its `ConditionExpression` is a highly effective tool for solving concurrency problems.
* Load testing (concurrent access testing) is a mandatory step to detect logical flaws in financial transaction flows.

### Conclusion
This project has provided our team with a much more practical perspective on how to securely manage data in the Cloud. Thank you all for reading, and we look forward to hearing your insights or suggestions on how you handle transaction flows in other architectures.

<img src="/images/3-BlogsPosted/Blog.png" width="80%" />