---
title : "Introduction"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### About NaturEra Green Banking

**NaturEra** is a Green Banking module on AWS Serverless that plugs into the bank POS transaction flow. On every card swipe, the system:

1. Looks up the emission factor by merchant **MCC**
2. Calculates **CO2** for the transaction amount
3. Debits the balance, writes the transaction log, and accumulates monthly CO2 in a single atomic **`TransactWriteItems`**
4. Locks the card when the monthly carbon quota is exceeded (the overflowing transaction is still allowed; the next one is blocked)

Customers track their environmental profile and carbon charts in the web app. Bank staff (ADMIN role) update CO2 factors / MCC mappings without redeploying. At the start of each month, a batch job unlocks cards and rewards low-emission users.

{{% notice info %}}
This workshop walks you through deploying the **NaturEra MVP** (SAM backend + React/Vite frontend), seeding demo data, calling the POS transaction API, and cleaning up resources afterward.
{{% /notice %}}

#### Workshop overview

In this workshop you will:

+ Deploy the serverless stack with **AWS SAM** (Lambda, API Gateway, DynamoDB, Cognito, EventBridge, S3, CloudFront)
+ Configure the React/Vite frontend against Cognito + API Gateway
+ Simulate POS card swipes (`POST /v1/transactions` with `x-api-key`)
+ Verify CO2 accumulation, real-time card lock, and data in DynamoDB / Dashboard

![NaturEra Architecture](/fcaj-intership-report-workshop/images/2-Proposal/naturera_architecture.jpg)

#### Architecture summary

The platform is fully **AWS-native serverless**:

| Component | Role in the workshop |
| :--- | :--- |
| **Amazon Cognito** | User Pool + App Client; JWT authorizer for customer/admin APIs (`custom:role`) |
| **Amazon API Gateway** | REST API stage `v1`; Cognito Authorizer (default) + API Key for the POS endpoint |
| **AWS Lambda** | Five core functions (see table below) |
| **Amazon DynamoDB** | Single-table `NaturEraGreenBankingTable` + 2 GSIs (`StatMonthIndex`, `LockedCardIndex`) |
| **Amazon EventBridge** | Cron on the 1st of each month triggers Monthly Offset Batch |
| **Amazon S3 + CloudFront** | Host the static frontend (React/Vite build) via OAC |
| **AWS SAM / CloudFormation** | Package and deploy the full stack |

**Main business flow (POS → carbon):**

```
POS Simulator  --(x-api-key)-->  API Gateway  -->  TransactionInterceptor Lambda
                                                        │
                                              DynamoDB TransactWriteItems
                                              (PROFILE + CARD check + TXN + STAT)
                                                        │
                                              if CO2 >= quota → LOCK card
```

**Key architecture decisions (ADRs):**

+ **ADR-001** — Atomic Core Banking writes with `TransactWriteItems` (no Saga/Step Functions)
+ **ADR-002** — Least-privilege IAM: no `dynamodb:Scan`; multi-user reads via GSI + `Query`
+ **ADR-003** — Real-time card lock on quota breach (overflow drop allowed)

Backend layering: `functions/` → `services/` → `repositories/` → `models/` + `utils/` + `configs/`.

#### Core Lambda functions

| Lambda | Trigger / Route | Responsibility |
| :--- | :--- | :--- |
| **TransactionInterceptor** | `POST /v1/transactions` (Auth: **NONE** + **API Key**) | Ingest POS txn, compute CO2 by MCC, debit + log + accumulate STAT in one `TransactWriteItems`; lock card if over quota |
| **DashboardApi** | `GET /v1/dashboard` (Cognito) | Return monthly carbon stats + recent transactions for the customer UI |
| **GreenProfileCardApi** | `GET /v1/profile/{requestId}` (Cognito) | Environmental profile / card status; authorize by `custom:role` |
| **AdminRuleConfigApi** | `GET\|PUT /v1/admin/config/co2-rules`<br>`GET\|PUT /v1/admin/config/mcc-mapping` (Cognito + ADMIN) | Read/update CO2 rules and MCC mapping (`CONFIG#*`) without redeploy |
| **MonthlyOffsetBatch** | EventBridge `cron(0 0 1 * ? *)` | Month start: unlock LOCKED cards + reward users under `REWARD_THRESHOLD` (GSI Query, no Scan) |

{{% notice tip %}}
The POS endpoint uses an **API Key** (machine-to-machine). Dashboard / Profile / Admin use **Cognito JWT**. Keep this distinction in mind when you test APIs later in the workshop.
{{% /notice %}}
