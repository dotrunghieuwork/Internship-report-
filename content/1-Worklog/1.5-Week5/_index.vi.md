---
title: "Worklog tuần 5"
date: 2026-07-13
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Xây dựng luồng xử lý tự động (event-driven) bằng EventBridge.
* Tích hợp các cơ chế hứng lỗi và xác thực người dùng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :---: | :--- | :---: | :---: | :--- |
| 2 - 3 | Tự động hóa tác vụ hàng tháng: <br> - Cấu hình Amazon EventBridge kích hoạt hàm lambda vào 00:00 ngày đầu tháng. <br> - Viết logic quét người dùng vượt hạn mức CO2 để tặng cây hoặc mở khóa thẻ. | 13/07/2026 | 14/07/2026 | Yêu cầu dự án |
| 4 - 5 | Thiết lập cơ chế hứng lỗi: <br> - Tạo hàng đợi Amazon SQS. <br> - Cấu hình SQS làm dead-letter queue (DLQ) để hứng các event bị lỗi từ hàm batch job. | 15/07/2026 | 16/07/2026 | Tài liệu AWS SQS |
| 6 | Tích hợp xác thực: <br> - Khởi tạo Amazon Cognito user pool. <br> - Gắn cognito authorizer vào API gateway để bảo vệ các endpoint nội bộ. | 17/07/2026 | 17/07/2026 | Tài liệu AWS Cognito |

### Kết quả đạt được tuần 5:
* Xây dựng thành công kiến trúc hướng sự kiện (event-driven), giúp hệ thống chạy ngầm tự động mà không tốn tài nguyên máy chủ 24/7.
* Đảm bảo tính tin cậy (reliability) cho hệ thống nhờ cơ chế hứng và lưu trữ request lỗi qua SQS DLQ.
* Bảo mật thành công các API endpoint, ngăn chặn truy cập trái phép bằng Cognito.