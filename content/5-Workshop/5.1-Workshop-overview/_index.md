---
title : "Introduction"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Introduction to NaturEra Green Banking

**NaturEra** is an extended Green Banking module built on the AWS Serverless platform, seamlessly integrated into the bank's POS transaction flow. Every time a customer swipes their card, the system automatically:

1. Looks up the emission factor based on the merchant's **MCC** (Merchant Category Code).
2. Calculates the **CO₂** equivalent corresponding to the transaction amount.
3. Deducts the balance + logs the transaction history + accumulates the monthly CO₂ in **a single atomic operation** (`TransactWriteItems`).
4. Locks the card immediately when the monthly carbon limit is exceeded (the transaction breaching the threshold is permitted; subsequent transactions are blocked).

Customers can track their environmental profiles and carbon charts via a web app; bank staff (ADMIN role) can update CO₂ factors / MCC mappings without redeploying the system. At the end of each month, a batch job automatically unlocks cards and evaluates rewards for low-emission users.

{{% notice info %}}
This workshop will guide you through **deploying the NaturEra MVP** (AWS SAM backend + React/Vite frontend), seeding demo data, invoking the POS transaction API, and cleaning up resources after the lab.
{{% /notice %}}

#### Workshop Overview

In this workshop, you will:

+ Deploy a serverless stack using **AWS SAM** (Lambda, API Gateway, DynamoDB, Cognito, EventBridge, S3, CloudFront).
+ Configure the React/Vite frontend to connect with Cognito + API Gateway.
+ Simulate a POS card swipe transaction (`POST /v1/transactions` using an `x-api-key`).
+ Verify CO₂ accumulation, real-time card locking, and data updates on DynamoDB / Dashboard.

<img src="/images/5-Workshop/5.1-Workshop-overview/naturera_architecture.jpg" width="80%" />

#### Architecture Summary

The platform strictly adheres to an **AWS-native serverless** architecture:

| Component | Role in the workshop |
| :--- | :--- |
| **Amazon Cognito** | User Pool + App Client; JWT authorizer for customer / admin APIs (`custom:role`). |
| **Amazon API Gateway** | REST API stage `v1`; Cognito Authorizer (default) + API Key for the POS endpoint. |
| **AWS Lambda** | 5 core functions handling business logic (see table below). |
| **Amazon DynamoDB** | Single-table design `NaturEraGreenBankingTable` + 2 GSIs (`StatMonthIndex`, `LockedCardIndex`). |
| **Amazon EventBridge** | Cron schedule on the 1st of every month to trigger the Monthly Offset Batch. |
| **Amazon S3 + CloudFront** | Hosting the static frontend (React/Vite build) via OAC. |
| **AWS SAM / CloudFormation** | Packaging and deploying the entire stack. |

**Main Business Flow (POS → Carbon):**