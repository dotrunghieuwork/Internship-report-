---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về NaturEra Green Banking

**NaturEra** là module Green Banking mở rộng trên nền tảng AWS Serverless, tích hợp vào luồng giao dịch POS của ngân hàng. Mỗi lần khách hàng quẹt thẻ, hệ thống tự động:

1. Tra cứu hệ số phát thải theo mã **MCC** của merchant
2. Tính lượng **CO2** tương ứng với số tiền giao dịch
3. Trừ tiền + ghi lịch sử giao dịch + cộng dồn CO2 tháng trong **một lệnh atomic** (`TransactWriteItems`)
4. Khóa thẻ ngay khi vượt hạn mức carbon tháng (giao dịch vượt ngưỡng vẫn được phép; giao dịch tiếp theo bị chặn)

Khách hàng theo dõi hồ sơ môi trường và biểu đồ carbon qua web app; nhân viên ngân hàng (role ADMIN) cập nhật hệ số CO2 / mapping MCC mà không cần deploy lại hệ thống. Cuối mỗi tháng, job batch tự động mở khóa thẻ và xét thưởng cho người dùng phát thải thấp.

{{% notice info %}}
Workshop này hướng dẫn bạn **triển khai MVP NaturEra** (backend SAM + frontend React/Vite), seed dữ liệu demo, gọi API giao dịch POS và dọn dẹp tài nguyên sau lab.
{{% /notice %}}

#### Tổng quan về workshop

Trong workshop, bạn sẽ:

+ Triển khai stack serverless bằng **AWS SAM** (Lambda, API Gateway, DynamoDB, Cognito, EventBridge, S3, CloudFront)
+ Cấu hình frontend React/Vite kết nối Cognito + API Gateway
+ Giả lập giao dịch quẹt thẻ POS (`POST /v1/transactions` với `x-api-key`)
+ Kiểm tra cộng dồn CO2, khóa thẻ real-time và dữ liệu trên DynamoDB / Dashboard

<img src="/Internship-report-/images/5-Workshop/5.1-Workshop-overview/naturera_architecture.jpg" width="80%" />

#### Tóm tắt kiến trúc

Nền tảng áp dụng kiến trúc **AWS-native serverless** hoàn toàn:

| Thành phần | Vai trò trong workshop |
| :--- | :--- |
| **Amazon Cognito** | User Pool + App Client; JWT authorizer cho API khách hàng / admin (`custom:role`) |
| **Amazon API Gateway** | REST API stage `v1`; Cognito Authorizer (mặc định) + API Key cho endpoint POS |
| **AWS Lambda** | 5 hàm core xử lý nghiệp vụ (xem bảng bên dưới) |
| **Amazon DynamoDB** | Single-table `NaturEraGreenBankingTable` + 2 GSI (`StatMonthIndex`, `LockedCardIndex`) |
| **Amazon EventBridge** | Lịch cron ngày 1 hàng tháng kích hoạt Monthly Offset Batch |
| **Amazon S3 + CloudFront** | Host frontend tĩnh (React/Vite build) qua OAC |
| **AWS SAM / CloudFormation** | Đóng gói và triển khai toàn bộ stack |

**Luồng nghiệp vụ chính (POS → carbon):**

```
POS Simulator  --(x-api-key)-->  API Gateway  -->  TransactionInterceptor Lambda
                                                        │
                                                        ▼
                                              DynamoDB TransactWriteItems
                                              (PROFILE + CARD check + TXN + STAT)
                                                        │
                                              nếu CO2 >= quota → LOCK card
```

**Các quyết định kiến trúc đáng nhớ (ADR):**

+ **ADR-001** — Core Banking ghi atomic bằng `TransactWriteItems` (không dùng Saga/Step Functions)
+ **ADR-002** — IAM least-privilege: không cấp `dynamodb:Scan`; truy vấn nhiều user qua GSI + `Query`
+ **ADR-003** — Khóa thẻ real-time khi vượt hạn mức (giọt nước tràn ly: giao dịch vượt ngưỡng vẫn thành công)

Backend tổ chức **4 lớp**: `functions/` → `services/` → `repositories/` → `models/` + `utils/` + `configs/`.

#### Các hàm Lambda core

| Lambda | Trigger / Route | Chức năng |
| :--- | :--- | :--- |
| **TransactionInterceptor** | `POST /v1/transactions` (Auth: **NONE** + **API Key**) | Nhận giao dịch POS, tính CO2 theo MCC, trừ tiền + ghi log + cộng dồn STAT trong 1 `TransactWriteItems`; khóa thẻ nếu vượt quota |
| **DashboardApi** | `GET /v1/dashboard` (Cognito) | Trả thống kê carbon tháng + giao dịch gần nhất cho UI khách hàng |
| **GreenProfileCardApi** | `GET /v1/profile/{requestId}` (Cognito) | Xem hồ sơ môi trường / trạng thái thẻ; phân quyền theo `custom:role` |
| **AdminRuleConfigApi** | `GET\|PUT /v1/admin/config/co2-rules`<br>`GET\|PUT /v1/admin/config/mcc-mapping` (Cognito + role ADMIN) | Đọc/cập nhật hệ số CO2 và từ điển mapping MCC (`CONFIG#*`) không cần redeploy |
| **MonthlyOffsetBatch** | EventBridge `cron(0 0 1 * ? *)` | Đầu tháng: mở khóa toàn bộ thẻ LOCKED + xét thưởng user dưới ngưỡng `REWARD_THRESHOLD` (Query GSI, không Scan) |

{{% notice tip %}}
Endpoint POS dùng **API Key** (máy-to-máy), còn Dashboard / Profile / Admin dùng **JWT Cognito**. Đây là điểm cần nắm khi test API ở phần sau của workshop.
{{% /notice %}}
