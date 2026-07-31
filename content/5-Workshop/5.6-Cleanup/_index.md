---
title : "Clean up"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
#### Clean Up Resources

Congratulations on successfully completing this lab! 

In this lab, you learned how to deploy a modern Serverless architecture for a digital banking project using Infrastructure as Code (IaC). You automated the creation of AWS Lambda, API Gateway, Amazon DynamoDB, and Amazon Cognito with just a few CLI commands.

To avoid unexpected charges (exceeding the Free Tier), it is crucial to clean up your infrastructure after you finish. Thanks to AWS SAM, this process is incredibly quick.

#### Cleanup Steps

1. **Delete the entire Stack using SAM CLI**
   Open your Terminal in the directory containing your `template.yaml` file and run the following command:
   ```bash
   sam delete