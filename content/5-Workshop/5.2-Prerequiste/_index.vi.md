---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

Trước khi bắt đầu lab, hãy đảm bảo máy tính và tài khoản AWS của bạn đã sẵn sàng các công nghệ / công cụ dưới đây.

#### Tài khoản & quyền AWS

+ Tài khoản AWS (nên dùng tài khoản học viên / sandbox, **không** dùng production)
+ IAM user (hoặc role) có quyền triển khai stack SAM: CloudFormation, Lambda, API Gateway, DynamoDB, Cognito, EventBridge, S3, CloudFront, IAM (tạo role cho Lambda), CloudWatch Logs (tùy chọn cho nhóm nhiều người sử dụng chung tài khoản)
+ Region khuyến nghị cho workshop: **`ap-southeast-1`** (Singapore) hoặc **`ap-southeast-2`** (Sydney) — khớp `SETUP_GUIDE` và cấu hình deploy hiện tại của dự án

Bạn có thể tham khảo policy mẫu trong repo dự án tại `backend/iam-user-policy.json` (điều chỉnh resource ARN S3 artefact bucket theo môi trường của bạn).

{{% notice warning %}}
Sau khi lab xong, hãy làm bước **Cleanup** để xóa stack và tránh phát sinh chi phí CloudFront / DynamoDB / Cognito ngoài ý muốn.
{{% /notice %}}

#### Công cụ bắt buộc trên máy local

| Công cụ | Phiên bản gợi ý | Mục đích |
| :--- | :--- | :--- |
| **Git** | bất kỳ bản ổn định | Clone source `naturEra-green-banking-web` |
| **Node.js** | **20.x** trở lên (runtime Lambda trên AWS là `nodejs24.x`) | Chạy frontend Vite và script seed backend |
| **npm** | đi kèm Node.js | Cài dependency `apps/web` và `backend` |
| **AWS CLI v2** | đã `aws configure` | Deploy, lấy output stack, gọi API / DynamoDB |
| **AWS SAM CLI** | bản mới nhất | `sam build` / `sam deploy` / `sam delete` |
| **Docker Desktop** | đang chạy | SAM dùng Docker khi build/package Lambda (nếu môi trường yêu cầu) |
| **Trình soạn thảo** | VS Code / Cursor, … | Chỉnh `.env` frontend và xem log |

**Kiểm tra nhanh:**

```bash
node -v
npm -v
aws --version
sam --version
docker info
aws sts get-caller-identity
```

`aws sts get-caller-identity` phải trả về Account / Arn hợp lệ của bạn.

#### Kiến thức tiên quyết (nên biết trước lab)

Bạn không cần là chuyên gia, nhưng nên nắm các khái niệm sau để theo kịp các bước:

+ **Serverless cơ bản:** Lambda, API Gateway, DynamoDB (partition/sort key), Cognito JWT
+ **REST API:** method, path, header `Authorization` / `x-api-key`, JSON body
+ **CLI cơ bản:** điều hướng thư mục, chạy lệnh npm / aws / sam
+ **React + Vite (cơ bản):** chạy `npm run dev`, biến môi trường `VITE_*`

#### Source code workshop

Clone (hoặc mở sẵn) repository dự án:

```bash
git clone https://github.com/Kenjtermine/naturEra-green-banking-web.git
cd naturEra-green-banking-web
```

Cấu trúc chính bạn sẽ dùng trong lab:

```
naturEra-green-banking-web/
├── apps/web/          # Frontend React + Vite + TailwindCSS
└── backend/           # SAM template + Lambda (Node.js ESM)
    ├── template.yaml
    ├── scripts/seed-data.js
    └── src/functions/ # 5 Lambda core
```

#### Cấu hình AWS CLI

```bash
aws configure
# AWS Access Key ID
# AWS Secret Access Key
# Default region: ap-southeast-1
# Default output format: json
```

#### Checklist trước khi sang phần tiếp theo

- [ ] AWS CLI đã authenticate (`sts get-caller-identity` OK)
- [ ] SAM CLI + Docker sẵn sàng
- [ ] Node.js / npm đã cài
- [ ] Đã có source `naturEra-green-banking-web` trên máy
- [ ] Đã chọn region `ap-southeast-1` (hoặc thống nhất region với cả nhóm)

Khi hoàn tất, chuyển sang phần **Backend setup** (deploy SAM) rồi **Frontend setup**.
