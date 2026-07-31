---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploy Serverless Green Banking Backend (AWS SAM) with NaturEra

#### Overview
In this workshop, we will go through the process of setting up and deploying the entire backend system for the NaturEra Green Banking project. Instead of creating VPC endpoints via the AWS Console (difficult to use and hard to manage), we will use **Infrastructure as Code (IaC)** with **AWS SAM (Serverless Application Model)**.

The Serverless architecture will offer auto-scaling, pay-as-you-go pricing, and a number of other enterprise-grade features. This architecture "just works" to connect to the Frontend React and calculate CO2 in real-time.

You will be guided through a series of incremental development cycles: from creating the project, designing the NoSQL data store (DynamoDB), writing the Backend (Lambda), to configuring API security and user management with Cognito.

#### Content
1. [Introduction to workshop](5.1-Introduction/)
2. [Prerequisites & Setup](5.2-Prerequiste/)
3. [Create Backend with AWS SAM CLI](5.3-Backend-setup/)
4. [Create Frontend with React & Vite](5.4-Frontend-setup/)
5. [Clean up](5.5-Cleanup/)