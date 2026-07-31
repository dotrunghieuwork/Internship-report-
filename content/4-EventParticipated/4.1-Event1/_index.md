---
title: "Event 1: Cloud Operations, Agentic Security & AWS Exam Strategy"
date: 2026-06-20
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

### Event Objectives
* Debunk myths about system monitoring and understand the gap between hardware metrics and actual user experience.
* Explore the power of Agentic AI in automated security testing (Pentesting) via Frontier Agent.
* Build an effective learning roadmap and strategy to conquer the AWS Certified Cloud Practitioner (CLF-C02) exam.

### Speakers
* **Mr. Ngo Le Tan Huy** – Presenter of "Inside The Exam: AWS Cloud Practitioner"
* **Mr. Thinh Nguyen** – DevOps/DevSecOps/Cloud Engineer @ Styl Solutions & FCAJ
* **Mr. Nguyen Huynh Son** – Member of AWS Student Builder Group HUFLIT, Ex Infrastructure Reliability Engineer @ SPS

### Key Highlights
* **The Illusion of "Green Dashboards":** Stable CPU/RAM metrics do not guarantee smooth user operations. A live demo showed that while API Gateway returned HTTP 200 OK, the underlying database transaction was broken, preventing users from logging in.
* **Automated Security with Frontier Agent:** Instead of spending tens of thousands of dollars and waiting weeks for manual pentests, Frontier Agent (powered by Amazon Bedrock) can autonomously reason, scan source code, and execute real-world attack scenarios to find vulnerabilities.
* **"Keyword Thinking" Strategy:** Conquering the CLF-C02 exam doesn't require memorizing deep configurations. It requires the ability to map keywords (e.g., "Decouple" = SQS) and effectively use the process of elimination.

### Key Takeaways
* **True SLA Mindset:** Monitoring is not just looking at hardware graphs. It must follow a "Monitoring Pyramid," starting from infrastructure up to the end-user experience, to detect anomalies before customers complain.
* **The Limits of AI in Security:** Although Frontier Agent can autonomously chain complex vulnerabilities (like IDOR + XSS) similar to a real hacker, it is still halted by hard physical or logical barriers like Multi-Factor Authentication (MFA). Humans remain the ultimate controllers.
* **Exam Room Tactics:** Maximize the 30-minute extension granted to non-native English speakers and efficiently utilize the "Flag for review" feature for better time management.

### Applying to Work
* **Redesigning Project Alert Systems:** Applying the "Green Dashboard" lesson, I configured Amazon CloudWatch Alarms to focus on the error rates of transaction-processing Lambda functions and the number of messages sent to the SQS Dead-letter Queue (DLQ), rather than just measuring execution duration.
* **Securing Serverless APIs:** Integrated hard security boundaries like Amazon Cognito (to prevent unauthorized access) and AWS WAF in front of the API Gateway, inspired by how MFA can block automated agent sweeps.
* **AWS Certification Preparation:** Fully utilized the AWS Free Tier to get hands-on experience deploying services rather than just studying theory, applying "Keyword Thinking" to speed up CLF-C02 practice tests.

### Event Experience
Attending this event provided me with insights that completely shifted my mindset regarding system operations.
* **Learning from Experts:** The speakers' raw stories about late-night on-call emergencies helped me vividly visualize the real-world pressure of Cloud/DevOps roles.
* **Technological Perspective:** Watching Frontier Agent automatically map out a complex attack vector on a live demo screen truly opened my eyes to how fast the DevSecOps industry is evolving.
* **Pragmatic Discussions:** The speakers were highly transparent about the tool's limitations (e.g., API token costs, MFA barriers), providing an objective and practical view of the technology rather than just hype.

### Lessons Learned
* Never blindly trust system metrics without verifying the actual end-user journey.
* Security must be automated and deeply embedded into the Software Development Life Cycle (SDLC), rather than treated as an afterthought.
* An AWS certification is not just a badge; it is a standardization framework that forces you to learn Cloud architecture in the most scientific and methodical way.

### Event Photos
<img src="/Internship-report-/images/4-EventParticipated/day20.jpg" width="80%" />
