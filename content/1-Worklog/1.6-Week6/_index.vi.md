---
title: "Worklog tuần 6"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* Phát triển và triển khai các thành phần frontend.
* Tích hợp frontend với backend và kiểm thử toàn bộ luồng ứng dụng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :---: | :--- | :---: | :---: | :--- |
| 2 - 3 | Triển khai giao diện frontend: <br> - Build dự án React và tải tĩnh lên Amazon S3. <br> - Cấu hình S3 bucket cho static website hosting và phân phối bằng CloudFront. | 20/07/2026 | 21/07/2026 | Yêu cầu dự án |
| 4 - 5 | Tăng cường bảo mật và giám sát: <br> - Tích hợp AWS WAF chặn trước API gateway để phòng chống các luồng traffic độc hại. <br> - Cấu hình Amazon CloudWatch để giám sát và thu thập log. <br> - Tạo alarm cảnh báo chi phí (billing) và cảnh báo lỗi Lambda. | 22/07/2026 | 23/07/2026 | Tài liệu AWS WAF |
| 6 | Kiểm thử toàn hệ thống: <br> - Đóng vai thiết bị POS gọi API thực tế vào hệ thống. <br> - Kiểm tra luồng cấp phát token từ Cognito và luồng ghi nhận dữ liệu xuống DynamoDB. | 24/07/2026 | 24/07/2026 | Đặc tả API |

### Kết quả đạt được tuần 6:
* Frontend được phân phối tốc độ cao qua CloudFront với chi phí hosting gần như bằng không.
* Hệ thống đạt chuẩn bảo mật doanh nghiệp với sự bảo vệ của AWS WAF và IAM policy nghiêm ngặt.
* Tích hợp thành công công cụ giám sát CloudWatch, sẵn sàng gửi cảnh báo tự động khi có bất thường.