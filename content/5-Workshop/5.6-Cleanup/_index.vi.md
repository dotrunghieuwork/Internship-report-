---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Dọn dẹp tài nguyên

Xin chúc mừng bạn đã hoàn thành xong bài thực hành này! 

Trong lab này, bạn đã học cách triển khai một kiến trúc Serverless hiện đại cho dự án ngân hàng số sử dụng Infrastructure as Code (IaC). Bạn đã tự động hóa việc tạo AWS Lambda, API Gateway, Amazon DynamoDB và Amazon Cognito chỉ bằng vài dòng lệnh.

Để tránh phát sinh chi phí ngoài ý muốn (vượt mức Free Tier), việc dọn dẹp hạ tầng sau khi hoàn thành là rất quan trọng. Nhờ sử dụng AWS SAM, quá trình này diễn ra vô cùng nhanh chóng.

#### Các bước dọn dẹp

1. **Xóa toàn bộ Stack bằng SAM CLI**
   Mở Terminal tại thư mục chứa file `template.yaml` của bạn và chạy lệnh sau:
   ```bash
   sam delete