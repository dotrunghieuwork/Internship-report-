---
title: "Event 2: Agentic AI Build Week & Hackathon Showcase"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

### Event Objectives
* Promote the Agentic AI development community and practical applications on the AWS platform.
* Showcase outstanding technological solutions emerging from a 24-hour Hackathon.
* Connect the AWS expert network, sharing experiences in building MVPs (Minimum Viable Products), optimizing costs, and deploying high-load systems.

### Featured Teams & Projects
* **Team AI-Powered Conversation Ordering** *(Anh Duy, Tran Dong, etc.)*: KFC Bot Agent solution for processing natural language orders.
* **Team SA Professional Native App** *(Thuan Phat, Hoang Long, etc.)*: AI application automating AWS architecture design and IaC generation.
* **Team Signal Scout** *(Tan Luc, Hoang Hieu, etc.)*: AI platform monitoring business signals and automating CI/CD.
* **Team Hackathon Journey** *(An Khuong, Quoc Huy, etc.)*: S.H.E.P.H.E.R.D project for crowd monitoring, summarizing teamwork experiences under intense pressure.

### Key Highlights
* **Infrastructure as Code (IaC) Automation:** The SA Professional Native App left a strong impression by using AI to replace manual steps in gathering requirements, drawing architecture diagrams, and generating IaC, saving dozens of working hours.
* **Cost Optimization and Observability:** Team Signal Scout brought a real-world problem regarding Service Discovery and system monitoring. They detailed the operational costs of AWS services and how to combine them with 3rd-party tools (LangFuse, Apify) to minimize maintenance fees.
* **Agent Accuracy:** Through the KFC Bot, the event emphasized the boundary between an AI "understanding" natural language and it correctly "applying business rules" to confirm orders without causing financial discrepancies.

### Key Takeaways
* **MVP (Minimum Viable Product) Mindset:** Within the 24-hour Hackathon timeframe, teams didn't try to build everything. They focused on the most core feature flow to prove the solution worked before considering scaling.
* **Cloud Cost Management Strategy:** Deploying AI or Serverless is not just a technological challenge, but an economic one. Cost estimation right from the architecture design phase is mandatory.
* **The Power of Teamwork:** Time pressure required strict division of labor between those handling Cloud infrastructure, those integrating AI, and those preparing for the pitch.

### Applying to Work
* **IaC Configuration for Serverless Project:** Inspired by the infrastructure code generation of the SA Native App, I proactively eliminated manual operations on the AWS Console. Instead, the entire infrastructure for the **NaturEra Green Banking** project was fully packaged via the AWS SAM `template.yaml` file, ensuring consistent and automated deployment.
* **Green Banking Infrastructure Cost Optimization:** Applying the cost analysis mindset from team Signal Scout, I designed DynamoDB tables in *On-Demand* mode and allocated appropriate memory capacity for Lambda functions, maximizing the AWS Free Tier while maintaining performance.
* **Lean Development Process:** Learning from the Hackathon spirit, our team decided to dedicate all efforts to fully resolving the core API flow (the TransactWriteItems flow for balance deduction and carbon credit addition) before branching out to secondary features like EventBridge or Cognito.

### Event Experience
Listening directly to engineers present their results after 24 continuous hours of coding was an incredibly inspiring experience.
* **Problem-Solving Ability:** The challenges the teams faced (IAM permission errors, memory misconfigurations, AI integration timeouts) were the exact bugs I encountered during my project. Hearing their troubleshooting methods provided me with many new perspectives.
* **Pitching Skills:** Beyond coding proficiency, how the teams conveyed their ideas and visually described their Architecture flow to the judges was an invaluable soft skill I learned to prepare for our final Workshop defense.

### Lessons Learned
* The best Cloud architecture is not the one using the most cutting-edge tech, but the one that solves the business problem with the most optimal operational cost.
* Teamwork and communication skills (API integration, resource division) determine 80% of a project's survival when facing tight deadlines.
* Adopting Infrastructure as Code (IaC) is an inevitable trend that every system engineer must master to avoid falling behind.

### Event Photos
<img src="/Internship-report-/images/4-EventParticipated/day25.jpg" width="80%" />
