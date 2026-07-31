---
title: "Blog 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# XỬ LÝ LỖI RACE CONDITION TRONG HỆ THỐNG GIAO DỊCH SERVERLESS VỚI AMAZON DYNAMODB

Chào mọi người trong group,

Trong tuần vừa qua, khi thực hiện dự án thực tập NaturEra Green Banking trên AWS, nhóm mình đã đụng phải một bài toán cổ điển nhưng rất thú vị khi làm việc với hệ thống phân tán: Race Condition.

### Bài toán đặt ra
Chức năng cốt lõi của dự án là khi người dùng thanh toán, hệ thống sẽ trừ tiền trong ví và đồng thời cộng một lượng "Tín chỉ Carbon" (CO2) vào hồ sơ. Mọi thứ hoạt động hoàn hảo khi test từng request đơn lẻ. Nhưng khi nhóm thử test với nhiều request (load test) được gửi đến cùng một tích tắc, vấn đề bắt đầu xuất hiện.

### Nguyên nhân gây lỗi
Với kiến trúc Serverless, AWS API Gateway sẽ tự động scale và kích hoạt nhiều hàm Lambda chạy song song. 
* Giả sử ví user có 100k. Có 2 request thanh toán món 50k đến cùng lúc. 
* Hai hàm Lambda độc lập sẽ cùng đọc database tại một thời điểm và đều thấy số dư là 100k. 
* Cả hai cùng thực hiện phép trừ và cùng ghi đè con số 50k xuống database. 
* Hậu quả: User thực hiện 2 giao dịch thành công, nhưng chỉ bị trừ tiền 1 lần.

### Giải pháp của nhóm
Ban đầu, nhóm tính dùng code để lock luồng ở tầng Lambda. Tuy nhiên, do các function trong Serverless chạy hoàn toàn độc lập và phi trạng thái (stateless), việc này không khả thi. Nhóm quyết định đẩy việc quản lý toàn vẹn dữ liệu xuống cho tầng Database (Amazon DynamoDB).

Nhóm mình áp dụng kết hợp hai cơ chế của DynamoDB:
* **ConditionExpression:** Khi cập nhật số dư, nhóm gắn thêm một điều kiện kiểm tra (ví dụ: `ConditionExpression: "Balance >= :cost"`). DynamoDB sẽ cấp phép cho request đến trước. Request song song đến sau sẽ lập tức bị từ chối với lỗi `ConditionalCheckFailedException` vì không còn thỏa điều kiện số dư.
* **TransactWriteItems:** Để đảm bảo việc trừ tiền và cộng tín chỉ Carbon luôn đi liền với nhau, nhóm đưa cả hai vào chung một Transaction. Nếu một thao tác thất bại, toàn bộ quá trình sẽ được tự động rollback, giúp hệ thống không bao giờ rơi vào trạng thái dữ liệu lấp lửng.

### Kiến trúc hệ thống sử dụng
* Triển khai hạ tầng (IaC): AWS SAM
* Backend: AWS Lambda, Amazon API Gateway
* Database: Amazon DynamoDB

### Những gì nhóm học được
* Không nên xử lý đồng bộ bằng code ở tầng Application khi dùng Serverless.
* DynamoDB không chỉ lưu trữ tốt mà `ConditionExpression` của nó là một công cụ cực kỳ hiệu quả để giải quyết bài toán đồng thời (concurrency).
* Test tải (truy cập đồng thời) là bước bắt buộc để phát hiện lỗi logic trong các luồng giao dịch tài chính.

### Kết luận
Project lần này mang lại cho nhóm một góc nhìn thực tế hơn rất nhiều về cách quản lý dữ liệu an toàn trên Cloud. Cảm ơn mọi người đã đọc bài viết, rất mong nhận được thêm chia sẻ hoặc góp ý từ các bạn về cách xử lý luồng giao dịch ở các kiến trúc khác.

<img src="/Internship-report-/images/3-BlogsPosted/Blog.png" width="80%" />
