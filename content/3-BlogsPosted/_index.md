---
title: "Published Blogs"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section lists and introduces the blogs published on the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj).

###  [Blog 1 - HANDLING RACE CONDITIONS IN A SERVERLESS TRANSACTION SYSTEM WITH AMAZON DYNAMODB](3.1-Blog1/)
This blog shares a real-world problem our team encountered during the NaturEra Green Banking project, where concurrent payment requests caused balance discrepancies. The article introduces our solution of offloading data integrity management to the Database tier using Amazon DynamoDB's `ConditionExpression` and `TransactWriteItems`, completely eliminating Race Conditions in a Serverless architecture.