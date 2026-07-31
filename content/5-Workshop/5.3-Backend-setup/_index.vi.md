---
title : "Thiết lập Backend"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---
Nếu bước trước bạn chưa clone dự án, hãy tạo một repo mới và clone vào thư mục thực hiện workshop:
```bash
git clone [https://github.com/Kenjtermine/naturEra-green-banking-web.git](https://github.com/Kenjtermine/naturEra-green-banking-web.git)
cd naturEra-green-banking-web
```
## Cấu trúc của thư mục backend

```bash
backend/
├── events/                   # Chứa các file .json giả lập request để test local
├── functions/                # Tầng Handler (Entrypoints)
│   ├── dashboard/            # Lambda: Xử lý API GET /dashboard
│   ├── get-profile/          # Lambda: Xử lý API GET /profile
│   └── process-transaction/  # Lambda: Xử lý API POST /transactions
├── src/                      # Tầng Business Logic & Database (Dùng chung)
│   ├── configs/              # Cấu hình môi trường, hằng số
│   ├── models/               # Định nghĩa cấu trúc dữ liệu
│   ├── repositories/         # Tầng giao tiếp DynamoDB (Data Access)
│   ├── services/             # Tầng nghiệp vụ (Tính điểm CO2, trừ tiền...)
│   └── utils/                # Các hàm hỗ trợ (Format response, CORS...)
├── scripts/                  # Chứa file script (VD: seed-data.js)
├── template.yaml             # Trái tim của SAM: Định nghĩa toàn bộ hạ tầng AWS
└── package.json              # Quản lý thư viện (aws-sdk, uuid...)
```

## Sử dụng SAM CLI để bắt đầu khởi tạo backend

Để xây dựng kiến trúc Serverless cho dự án **NaturEra Green Banking**, chúng ta sẽ sử dụng **AWS SAM (Serverless Application Model) CLI**. Đây là công cụ đắc lực của AWS giúp định nghĩa, kiểm thử (local) và triển khai toàn bộ hạ tầng (Lambda, API Gateway, DynamoDB, Cognito) hoàn toàn bằng mã nguồn (Infrastructure as Code - IaC).

Dưới đây là quy trình chuẩn để thiết lập Backend cho dự án:

Kiểm tra phiên bản của sam đảm bảo bạn đã cài đặt sam, nếu chưa có hãy tiến hành cài đặt trước:
```bash
sam version
```
Toàn bộ cài đặt thông số, chính sách, setup của các dịch AWS: Lambda, Cognito, Cloudfront, S3 đều được viết trong file template.yaml


### Các bước để bắt đầu khởi tạo Backend bằng SAM
#### Bước 1
Mở terminal tại folder chứa repo dự án bạn đã clone.
Di chuyển đến thư mục backend
```bash
cd backend
```
#### Bước 2
Chạy lệnh  `sam build` để SAM bắt đầu khởi tạo dự án:
```bash
sam build
```
Sau đó là `sam deploy --guided` để tiến hành deploy dự án lần đầu, ở các lần sau bạn có thể chỉ cần là `sam deploy`:
```bash
sam deploy --guided
```
Cuối cùng khi terminal hiện lên các câu hỏi bạn trả lời như sau:

 Stack name: naturera-green-banking-dev

 Region: ap-southeast-1 (hoặc 2 tùy theo khu vực bạn chọn)
 
 Parameter TableNameParam: NaturEraGreenBankingTable

 Confirm changes before deploy: Y

 Allow SAM CLI to create IAM roles: Y

 Disable rollback: N

 Save parameters: Y

 SAM configuration file: samconfig.toml