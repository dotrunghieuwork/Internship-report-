---
title: "Thực hành triển khai (Workshop)"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai mô hình Green Banking Serverless (AWS SAM) với NaturEra

#### Tổng quan

Trong phần Workshop này, chúng ta sẽ bắt tay vào việc thực hành thiết lập và triển khai toàn bộ hệ thống **Backend Serverless** cho dự án **NaturEra Green Banking**. Thay vì tạo tài nguyên thủ công qua giao diện AWS Console (dễ gây ra sai sót và khó tái sử dụng), chúng ta sẽ áp dụng **Infrastructure as Code (IaC)** với **AWS SAM (Serverless Application Model)**.

Mô hình Serverless sẽ mang đến khả năng mở rộng tự động (auto-scaling), tính toán theo yêu cầu (pay-as-you-go) và đặc biệt là tích hợp tính năng bảo mật mức Enterprise. Kiến trúc này đóng vai trò "xương sống" để kết nối với Frontend React và tính toán lượng CO2 trong thời gian thực (real-time).

Bạn sẽ được hướng dẫn qua một vòng lặp phát triển hoàn chỉnh: từ khâu khởi tạo dự án, thiết kế cơ sở dữ liệu NoSQL (DynamoDB), viết mã Backend (Lambda), đến việc triển khai các lớp bảo mật API và quản lý tài khoản người dùng với Cognito.

#### Nội dung thực hành

1. [Giới thiệu về workshop](5.1-Introduction/)
2. [Chuẩn bị môi trường & Cài đặt công cụ](5.2-Prerequiste/)
3. [Khởi tạo Backend với AWS SAM CLI](5.3-Backend-setup/)
4. [Khởi tạo Frontend với React & Vite](5.4-Frontend-setup/)
5. [Dọn dẹp tài nguyên (Clean up)](5.5-Cleanup/)