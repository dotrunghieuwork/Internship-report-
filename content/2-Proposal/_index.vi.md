---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Nền tảng NaturEra - Mô hình ngân hàng Green Banking 
## Giải pháp AWS Serverless hợp nhất cho mô hình giao dịch ngân hàng tính toán hệ số CO2

### 1. Tóm tắt điều hành  
NaturEra là một module ngân hàng xanh (Green Banking) được thiết kế bởi nhóm *, đóng vai trò là lớp mở rộng tích hợp vào một Core Banking hiện có, tự động tính toán lượng khí thải CO2 phát sinh từ mỗi giao dịch quẹt thẻ tại POS, thực thi hạn mức carbon hàng tháng theo thời gian thực, và khuyến khích hành vi tiêu dùng thân thiện môi trường thông qua cơ chế thưởng cuối tháng. Nền tảng hướng đến việc biến dữ liệu chi tiêu hàng ngày thành công cụ nâng cao nhận thức môi trường, mà không đòi hỏi khách hàng phải nhập liệu thủ công hay dùng thêm bất kỳ ứng dụng bên thứ ba nào.

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Bảo vệ môi trường là một vấn đề cấp thiết, trong ngành ngân hàng mô hình Green Banking mang đến một thông điệp sứ mệnh về bảo vệ môi trường thông qua giao dịch. Tuy vậy tại Việt Nam, mô hình này chưa phổ biến và ít có ngân hàng nào thực sự triển khai mô hình này. Các ngân hàng hiện nay không cung cấp cho khách hàng khả năng nhìn thấy tác động môi trường từ chính hành vi chi tiêu của mình. Các ứng dụng theo dõi carbon của bên thứ ba tồn tại độc lập với dữ liệu ngân hàng thật, buộc người dùng nhập liệu thủ công, thiếu độ chính xác, và không có cơ chế ràng buộc hay khuyến khích nào gắn liền với dòng tiền thực tế.

*Giải pháp*  
NaturEra tích hợp trực tiếp vào luồng xử lý giao dịch POS: mỗi lần quẹt thẻ, hệ thống tự động tra cứu hệ số phát thải theo mã MCC của merchant, tính ra lượng CO2 tương ứng, cộng dồn vào hạn mức carbon tháng của khách hàng trong cùng 1 thao tác ghi dữ liệu với việc trừ tiền — đảm bảo tính nhất quán tuyệt đối giữa số dư tài khoản và số liệu carbon mà không cần hạ tầng điều phối phức tạp (Saga/Step Functions). Khi khách hàng vượt hạn mức, thẻ tự động bị khóa ngay lập tức để tạo tác động nhắc nhở tức thời; cuối mỗi tháng, hệ thống tự động mở khóa và xét thưởng cho những khách hàng có mức phát thải thấp. 

### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AWS Serverless hoàn toàn (AWS-native):
* **AWS Cognito**: Quản lý quyền truy cập cho pool các người dùng: user, staff, admin.
* **AWS Lambda**: Các logic được xử lý bởi Lambda để xử lý các tác vụ của mô hình, bao gồm:
    * **Transaction Interceptor API** — nhận giao dịch POS, tính CO2 theo MCC, trừ tiền + ghi log + cộng dồn CO2
kiểm tra thẻ khóa trong 1 lệnh TransactWriteItems atomic duy nhất (SLA phản hồi dưới 2 giây).

    * **Dashboard API** — trả dữ liệu biểu đồ carbon theo danh mục cho ứng dụng khách hàng.
    * **Green Profile & Card API** — cho khách hàng xem hồ sơ môi trường và quản lý trạng thái thẻ.
    * **Admin Rule Config API** — cho nhân viên ngân hàng (role ADMIN) cập nhật hệ số CO2 theo MCC và từ điển danh mục hiển thị, không cần deploy lại hệ thống.
    * **Một số các lambda để xử lý các tác vụ đặc biệt** (monthly batch, log metrics, ...)
* **AWS S3**: Chuyển đổi frontend thành dữ liệu trang web tĩnh cho CloudFront.
* **AWS CloudFront**: Lưu trữ dữ liệu trang web tĩnh và truy cập qua HTTPS.
* **AWS Amplify**: Thư viện npm backend kết nối với AWS API Gateway, AWS Cognito để xây dựng frontend.
* **AWS API Gateway**: Xử lý các request từ frontend và đến Lambda.
* **AWS DynamoDB**: Lưu trữ dữ liệu của mô hình.


<!-- ![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg) -->

<img src="/images/5-Workshop/5.1-Workshop-overview/naturera_architecture.jpg" width="80%" />


### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*
Dự án được triển khai trong khuôn khổ thực tập FCAJ, thời hạn hoàn thiện MVP: 1 tháng, chia làm 4 giai đoạn:
1. *Thiết kế kiến trúc*: xác định 7 Lambda, thiết kế schema DynamoDB single-table, ra quyết định ADR-001/
   ADR-002/ADR-003.
2. *Xây dựng lõi giao dịch*: Transaction Interceptor với `TransactWriteItems`, cơ chế khóa thẻ real-time.
3. *Xây dựng lớp quản trị & báo cáo*: Admin Rule Config API, Dashboard API, Monthly Offset Batch Job.
4. *Kiểm thử & triển khai*: viết test giả lập cho từng lớp (model/service/repository), cấu hình IAM
   least-privilege, deploy qua AWS SAM.

*Công nghệ và công cụ sử dụng*
* Các công nghệ AWS: AWS Lambda, AWS API Gateway, AWS S3, AWS CloudFront, AWS Amplify, AWS Cognito, AWS DynamoDB.
* Các công cụ AWS: AWS SAM, AWS CDK, AWS CLI, AWS CloudFormation.
* Ngôn ngữ lập trình: Node.js 20.x, JavaScript ES2020+, React + Vite + TailwindCSS.

### 5. Lộ trình & Mốc triển khai  
- *Trước thực tập (Tháng 0)*: 1 tháng lên kế hoạch và đánh giá trạm cũ.  
- *Thực tập (Tháng 1–3)*:  
    - Tháng 1: Học AWS và nâng cấp phần cứng.  
    - Tháng 2: Thiết kế và điều chỉnh kiến trúc.  
    - Tháng 3: Triển khai, kiểm thử, đưa vào sử dụng.  
- *Sau triển khai*: Nghiên cứu thêm trong vòng 1 năm.  

### 6. Ước tính ngân sách  
Chi phí được tách thành 2 mức, vì bản chất khác nhau hoàn toàn về mục đích: mức *Workshop/Demo* chỉ để
trình bày kỹ thuật (vài chục giao dịch thử nghiệm), còn mức *Vận hành thực tế* mô phỏng quy mô ngân hàng
thật đưa vào sử dụng với 1.000 người dùng hoạt động
 
*6.1. Mức Workshop/Demo (MVP hiện tại)*
 
Ở quy mô demo (vài chục giao dịch thử nghiệm trong buổi trình bày), gần như toàn bộ chi phí nằm trong các
mốc miễn phí vĩnh viễn của AWS Lambda (1 triệu request/tháng) và Cognito (50.000 MAU) — tổng chi phí thực tế dưới ~ 1 USD/tháng.

*6.2. Mức vận hành thực tế (~1.000 người dùng hoạt động)*
 
Giả định mỗi người dùng thực hiện ~30 giao dịch POS/tháng (khoảng 1 lần/ngày) và kiểm tra Dashboard ~10
lần/tháng — tổng khối lượng xử lý ước tính ~80.000 lượt gọi Lambda/tháng và ~240.000 WCU DynamoDB/tháng
(do `TransactWriteItems` tiêu tốn gấp đôi write-capacity so với ghi thông thường cho mỗi item trong giao
dịch atomic).
 
| Dịch vụ | Khối lượng ước tính | Chi phí/tháng |
|---|---|---|
| AWS Lambda | ~80.000 lượt gọi (Interceptor, Dashboard, Card, Aggregator, Batch) | 0,00 USD *(trong free tier vĩnh viễn)* |
| Amazon DynamoDB (On-Demand) | ~240.000 WCU + ~55.000 RCU | ~0,50 USD |
| Amazon API Gateway (REST) | ~45.000 request | ~0,20 USD |
| Amazon Cognito | 1.000 MAU | 0,00 USD *(free tier tới 50.000 MAU)* |
| Amazon CloudWatch (Logs + Alarms) | Log ứng dụng + cảnh báo ngân sách | ~0,30 USD |
| Amazon SNS (thông báo push) | Cảnh báo hạn mức, khóa/mở thẻ | ~0,05 USD |
| AWS WAF *(khuyến nghị cho API tài chính)* | Web ACL + rule cơ bản | ~7,00 USD |
| Amazon Route 53 *(tên miền riêng, tùy chọn)* | Hosted zone + truy vấn | ~0,80 USD |
 
*Tổng ước tính*: ~8,85 USD/tháng ở quy mô 1.000 người dùng hoạt động, đã bao gồm WAF bảo vệ API — hạng mục
bảo mật khuyến nghị bắt buộc cho bất kỳ API xử lý giao dịch tài chính nào trước khi đưa vào vận hành thật.
 
*Vì sao thấp hơn nhiều so với các nền tảng AI-native (VD: ~60 USD/tháng cho 1.000 người dùng ở mô hình có
tích hợp Generative AI):* kiến trúc Green Banking không có bất kỳ lệnh gọi suy luận AI/ML nào (không dùng
Amazon Bedrock, không cần ECS Fargate xử lý Vision AI, không cần NAT Gateway cho service ngoài VPC) — toàn
bộ nghiệp vụ là các phép tính CO2 và thao tác dữ liệu có cấu trúc, vốn dĩ rẻ hơn rất nhiều so với suy luận
mô hình ngôn ngữ/thị giác. Đây là điểm mạnh kiến trúc đáng nêu trong phần so sánh chi phí của báo cáo, không
phải sai lệch/tính thiếu.
* Lưu ý: Bảng trên ước tính tại thời điểm viết báo cáo, chi phí thực tế có thể thay đổi sau này.
### 7. Đánh giá rủi ro (Risk Assessment)

**Ma trận rủi ro & Chiến lược giảm thiểu**

| Nhóm rủi ro | Mô tả rủi ro | Mức độ | Chiến lược giảm thiểu (Mitigation) |
| :--- | :--- | :--- | :--- |
| **Tích hợp & Nghiệp vụ** | API bên thứ 3 (VISA/Core Banking) phản hồi chậm hoặc sập mạng. | Trung bình | Áp dụng Adapter Pattern, xử lý bất đồng bộ (EventBridge/SQS) để không treo hệ thống. |
| **Bảo mật & Tuân thủ** | Hacker tấn công DDoS hoặc đánh cắp token JWT. | Cao | Ủy quyền quản lý danh tính cho AWS Cognito. Bọc API bằng AWS WAF và cấu hình API Gateway Throttling. |
| **Tài chính & Ngân sách** | Lỗi code (vòng lặp vô hạn) hoặc spam API làm chi phí AWS tăng vọt. | Cao | Thiết lập AWS Budgets Alert (cảnh báo khi vượt $5/tháng) và áp dụng UsagePlan kèm API Key cho máy POS. |
| **Toàn vẹn Dữ liệu** | Lỗi sai số thập phân hoặc gián đoạn mạng gây lệch sổ kế toán. | Rất Cao | Ép kiểu số nguyên (Integer) cho tiền tệ. Bắt buộc dùng DynamoDB Transactions (`TransactWriteItems`) để đảm bảo ACID. |

### 8. Kết quả kỳ vọng
 
*Sản phẩm demo*: một luồng hoàn chỉnh từ giao dịch quẹt thẻ POS → tính CO2 tự động → cộng dồn hạn mức
tháng → khóa thẻ real-time khi vượt ngưỡng → tự động mở khóa và xét thưởng đầu tháng sau, cùng dashboard
hiển thị carbon theo danh mục cho khách hàng.

*Phát trển kỹ thuật*: Hoàn chỉnh được production, có liên kết hợp đồng với các ngân hàng thật để có thể triển khai giao dịch chuẩn KYB, KYC trong tương lai.
 
*Giá trị dài hạn*: minh chứng năng lực thiết kế kiến trúc serverless cho hệ thống tài chính — từ tư duy
đánh đổi kiến trúc (ADR), thiết kế dữ liệu NoSQL single-table, đến bảo mật theo nguyên tắc least-privilege —
là nội dung phù hợp đưa vào hồ sơ năng lực (CV) và báo cáo tốt nghiệp thực tập.