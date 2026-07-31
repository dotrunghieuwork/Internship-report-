---
title: "Worklog tuần 4"
date: 2026-07-06
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Thiết lập hạ tầng nền tảng cho dự án cuối kỳ.
* Ứng dụng AWS SAM (IaC) để xây dựng API và xử lý tính toàn vẹn dữ liệu.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :---: | :--- | :---: | :---: | :--- |
| 2 - 3 | Khởi tạo dự án với AWS SAM: <br> - Viết cấu hình template.yaml cho các hàm Lambda và API Gateway. <br> - Thiết lập bảng DynamoDB lưu trữ lịch sử giao dịch và profile người dùng. | 06/07/2026 | 07/07/2026 | Tài liệu AWS SAM |
| 4 - 5 | Lập trình logic cốt lõi: <br> - Lập trình hàm transaction interceptor xử lý giao dịch POS. <br> - Triển khai tính năng transact write items của DynamoDB để chống race condition khi trừ tiền và cộng CO2. | 08/07/2026 | 09/07/2026 | Yêu cầu dự án |
| 6 | Xử lý lỗi bảo mật và kết nối: <br> - Cấu hình IAM policy theo nguyên tắc đặc quyền tối thiểu cho hàm Lambda. <br> - Sửa lỗi CORS khi gọi API từ môi trường local. | 10/07/2026 | 10/07/2026 | Tài liệu AWS IAM |

### Kết quả đạt được tuần 4:
* Đưa phương pháp infrastructure as code (IaC) vào dự án bằng AWS SAM, giúp việc build và deploy tự động hóa hoàn toàn.
* Giải quyết thành công bài toán race condition trong giao dịch tài chính bằng tính năng atomic transaction của DynamoDB.
* Khắc phục triệt để lỗi CORS và thiết lập quyền IAM an toàn cho hệ thống backend.