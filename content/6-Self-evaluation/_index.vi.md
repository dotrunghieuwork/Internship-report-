---
title: Tự đánh giá
date: 2026-07-30
weight: 6
chapter: false
pre: <b> 6. </b>
---


## Tự đánh giá

Trong thời gian thực tập tại **Amazon Web Services Viet Nam Company Limited** trong chương trình **Workforce Bootcamp - First Cloud AI Journey** từ **20/06/2026 đến 31/07/2026**, tôi có cơ hội tìm hiểu hệ sinh thái các dịch vụ AWS, tham gia các sự kiện kỹ thuật và trực tiếp xây dựng project cá nhân mang tên **NaturEra - Green Banking (Ứng dụng ngân hàng số Serverless tích hợp tính toán lượng khí thải Carbon)**.

Kỳ thực tập giúp tôi kết nối kiến thức lập trình nền tảng ở trường với một workflow triển khai Cloud thực tế. Tôi đã hoàn thiện thành công luồng xử lý End-to-End: từ giao diện người dùng (ReactJS) tích hợp xác thực bảo mật JWT qua **AWS Cognito**, định tuyến và xử lý CORS qua **API Gateway**, thực thi logic tính toán giao dịch bằng **AWS Lambda**, và lưu trữ dữ liệu bền vững trên cơ sở dữ liệu NoSQL **DynamoDB**. Đồng thời, tôi đã thiết lập thành công quy trình giám sát hệ thống và phân tích log thông qua **Amazon CloudWatch**.

Về thái độ làm việc, tôi tự triển khai kiến trúc cá nhân nhưng vẫn liên tục học hỏi qua việc thảo luận nhóm, tra cứu tài liệu AWS (AWS Documentation), và thực hành thử - sai liên tục. Tôi tập trung vào việc xử lý triệt để các lỗi tích hợp, tối ưu cấu hình bảo mật, duy trì tính minh bạch của payload và kiểm soát chi phí trong giới hạn tài nguyên cho phép.

## Bảng tiêu chí tự đánh giá

| STT | Tiêu chí | Mô tả | Tốt | Khá | Trung bình |
|---|---|---|---|---|---|
| 1 | **Kiến thức và kỹ năng chuyên môn** | Hiểu AWS services, Cloud-native workflow, API integration và áp dụng vào project thực tế. | ✅ | ☐ | ☐ |
| 2 | **Khả năng học hỏi** | Khả năng tự đọc AWS documentation, phân tích log trên CloudWatch và rút kinh nghiệm từ lỗi (Troubleshooting). | ✅ | ☐ | ☐ |
| 3 | **Tính chủ động** | Chủ động chọn topic thực tế (Green Banking), xác định cấu trúc dữ liệu và tự giải quyết các block kỹ thuật. | ✅ | ☐ | ☐ |
| 4 | **Tinh thần trách nhiệm** | Hoàn thành toàn bộ luồng E2E, quản lý tốt tài nguyên AWS để kiểm soát chi phí thực hành. | ✅ | ☐ | ☐ |
| 5 | **Kỷ luật** | Bám theo timeline thực tập, duy trì tiến độ hoàn thiện từng service (Auth, Database, API). | ☐ | ✅ | ☐ |
| 6 | **Tinh thần cầu tiến** | Sẵn sàng tiếp nhận feedback, sửa đổi payload logic, cấu hình lại hệ thống khi phát sinh lỗi bảo mật. | ✅ | ☐ | ☐ |
| 7 | **Giao tiếp** | Trình bày luồng kiến trúc, các lỗi kỹ thuật (CORS, Cognito Permission) và cách giải quyết một cách rành mạch. | ☐ | ✅ | ☐ |
| 8 | **Làm việc nhóm** | Tích cực trao đổi, cùng team phân tích nguyên nhân gốc rễ (root cause) của các lỗi hệ thống phức tạp. | ☐ | ✅ | ☐ |
| 9 | **Tác phong chuyên nghiệp** | Tôn trọng môi trường học tập, tuân thủ các quy định bảo mật của AWS khi thiết lập quyền hạn (IAM/Cognito). | ✅ | ☐ | ☐ |
| 10 | **Kỹ năng giải quyết vấn đề** | Xử lý triệt để các blocker như lỗi quyền ghi Attribute của Cognito, lỗi 400 Payload Mismatch, và 403 CORS Preflight. | ✅ | ☐ | ☐ |
| 11 | **Đóng góp cho project/team** | Xây dựng thành công kiến trúc Serverless có tính ứng dụng cao, chuẩn bị báo cáo dự án minh bạch, rõ ràng. | ✅ | ☐ | ☐ |
| 12 | **Đánh giá tổng thể** | Đánh giá chung về thái độ học tập, nỗ lực giải quyết vấn đề và chất lượng ứng dụng hoàn thiện trong kỳ thực tập. | ✅ | ☐ | ☐ |

## Điểm mạnh

- **Kỹ năng Troubleshooting & Tự học:** Tôi có khả năng tự phân tích log từ CloudWatch để bắt đúng thủ phạm gây lỗi thay vì đoán mò. 
- **Triển khai kỹ thuật Serverless:** Nắm vững và cấu hình thành công các dịch vụ nòng cốt. Từ việc thiết lập App Client trong Cognito (cấp quyền Write Attributes), cho đến việc setup Integration Response Headers (Access-Control-Allow-Origin, Methods, Headers) để vượt qua rào cản bảo mật CORS trên API Gateway.
- **Tư duy thiết kế hệ thống:** Đảm bảo được tính toàn vẹn dữ liệu (Data Integrity) giữa đầu phát (Frontend) và đầu thu (Backend). Hiểu rõ sự khác biệt giữa việc tạo Mock API để test giao diện và việc kết nối Live API thực tế để ghi dữ liệu cứng xuống DynamoDB.
- **Tính kiên nhẫn và chi tiết:** Bám sát từng bước cấu hình nhỏ nhất (như việc Deploy API sau mỗi lần thay đổi cấu hình Stage) để đảm bảo hệ thống Cloud cập nhật trạng thái chính xác.

## Điểm cần cải thiện

- **Sự tự tin khi trình bày kiến trúc (Architecture):** Cần cải thiện kỹ năng diễn đạt bằng lời nói khi giải thích các quyết định kỹ thuật (Technical trade-offs) – ví dụ tại sao lại dùng JWT Token lưu ở sessionStorage thay vì localStorage, hoặc logic đằng sau CORS Preflight.
- **Quản lý thời gian & Setup ban đầu:** Đôi lúc còn mất nhiều thời gian kẹt lại ở các bước cấu hình quyền hạn (IAM/Cognito). Cần lên kế hoạch đọc kỹ Documentation về Security Rules trước khi code để rút ngắn thời gian debug.
- **Tối ưu hóa Database (DynamoDB):** Dự án hiện tại đã ghi dữ liệu thành công, nhưng để mở rộng (scale), tôi cần đào sâu thêm về cách thiết kế Partition Key và Sort Key để tối ưu hóa chi phí truy vấn.
- **Bảo mật Endpoint nâng cao:** Cần tìm hiểu thêm về Rate Limiting hoặc gắn AWS WAF vào API Gateway để bảo vệ endpoint chuyển tiền khỏi rủi ro bị spam request trong môi trường thực tế.

## Nhận xét tổng quan

Kỳ thực tập tại FCAJ đã giúp tôi nhận ra rằng: xây dựng một hệ thống phần mềm trên Cloud không chỉ đơn thuần là viết code. Một hệ thống Serverless hoàn chỉnh đòi hỏi sự kết hợp chặt chẽ giữa thiết lập bảo mật mạng (CORS), xác thực người dùng (Auth), quản lý quyền hạn (IAM), xử lý API, tối ưu hóa cơ sở dữ liệu và giám sát log liên tục.

Bài học giá trị nhất của tôi là kỹ năng kết nối các điểm mấu chốt (connecting the dots) giữa các dịch vụ Cloud độc lập và tư duy chuẩn đoán lỗi (Troubleshooting). Việc tự tay gỡ từng nút thắt từ Frontend đến Backend và chứng kiến dữ liệu giao dịch chạy xuyên suốt, lưu trữ thành công trên AWS đã giúp tôi định hình rõ nét tư duy của một Kỹ sư Hệ thống chuyên nghiệp.