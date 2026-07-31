---
title : "Prerequisite"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

Before starting the lab, make sure your machine and AWS account are ready with the technologies and tools below.

#### AWS account & permissions

+ An AWS account (prefer a student / sandbox account — **not** production)
+ An IAM user (or role) allowed to deploy the SAM stack: CloudFormation, Lambda, API Gateway, DynamoDB, Cognito, EventBridge, S3, CloudFront, IAM (create roles for Lambda), CloudWatch Logs
+ Recommended workshop region: **`ap-southeast-1`** (Singapore) — matches the project `SETUP_GUIDE` and current deploy settings

You can use the sample policy in the project repo at `backend/iam-user-policy.json` (adjust the S3 artefact bucket ARN for your environment).

{{% notice warning %}}
After the lab, complete the **Cleanup** step to delete the stack and avoid unexpected CloudFront / DynamoDB / Cognito charges.
{{% /notice %}}

#### Required local tools

| Tool | Suggested version | Purpose |
| :--- | :--- | :--- |
| **Git** | any stable release | Clone `naturEra-green-banking-web` |
| **Node.js** | **20.x+** (Lambda runtime on AWS is `nodejs24.x`) | Run Vite frontend and backend seed scripts |
| **npm** | bundled with Node.js | Install `apps/web` and `backend` dependencies |
| **AWS CLI v2** | configured via `aws configure` | Deploy, read stack outputs, call API / DynamoDB |
| **AWS SAM CLI** | latest | `sam build` / `sam deploy` / `sam delete` |
| **Docker Desktop** | running | SAM uses Docker when building/packaging Lambdas (if required) |
| **Editor** | VS Code / Cursor, etc. | Edit frontend `.env` and inspect logs |

**Quick checks:**

```bash
node -v
npm -v
aws --version
sam --version
docker info
aws sts get-caller-identity
```

`aws sts get-caller-identity` must return a valid Account / Arn for your identity.

#### Prior knowledge (recommended)

You do not need to be an expert, but you should be comfortable with:

+ **Serverless basics:** Lambda, API Gateway, DynamoDB (partition/sort key), Cognito JWT
+ **REST APIs:** method, path, `Authorization` / `x-api-key` headers, JSON body
+ **Basic CLI:** navigate folders, run npm / aws / sam commands
+ **React + Vite (basics):** `npm run dev`, `VITE_*` environment variables

#### Workshop source code

Clone (or open) the project repository:

```bash
git clone https://github.com/Kenjtermine/naturEra-green-banking-web.git
cd naturEra-green-banking-web
```

Main layout used in the lab:

```
naturEra-green-banking-web/
├── apps/web/          # React + Vite + TailwindCSS frontend
└── backend/           # SAM template + Lambda (Node.js ESM)
    ├── template.yaml
    ├── scripts/seed-data.js
    └── src/functions/ # 5 core Lambdas
```

#### Configure AWS CLI

```bash
aws configure
# AWS Access Key ID
# AWS Secret Access Key
# Default region: ap-southeast-1
# Default output format: json
```

#### Checklist before the next section

- [ ] AWS CLI authenticated (`sts get-caller-identity` OK)
- [ ] SAM CLI + Docker ready
- [ ] Node.js / npm installed
- [ ] `naturEra-green-banking-web` source available locally
- [ ] Region set to `ap-southeast-1` (or agreed with your team)

When ready, continue with **Backend setup** (SAM deploy), then **Frontend setup**.
