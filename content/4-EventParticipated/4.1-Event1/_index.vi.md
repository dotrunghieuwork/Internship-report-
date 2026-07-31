---
title: "Event 1: Cloud Operations, Agentic Security & AWS Exam Strategy"
date: 2026-06-20
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

### Mục tiêu sự kiện (Event Objectives)
* Xóa bỏ lầm tưởng về giám sát hệ thống, thấu hiểu ranh giới giữa thông số phần cứng và trải nghiệm thực tế của người dùng.
* Khám phá sức mạnh của Trí tuệ nhân tạo tác tử (Agentic AI) trong việc tự động hóa kiểm thử bảo mật (Pentest) qua công cụ Frontier Agent.
* Xây dựng lộ trình và chiến thuật ôn thi chứng chỉ AWS Certified Cloud Practitioner (CLF-C02) hiệu quả.

### Diễn giả (Speakers)
* **Anh Ngô Lê Tấn Huy** – Presenter of "Inside The Exam: AWS Cloud Practitioner"
* **Anh Thịnh Nguyễn** – DevOps/DevSecOps/Cloud Engineer @ Styl Solutions & FCAJ
* **Anh Nguyễn Huỳnh Sơn** – Member of AWS Student Builder Group HUFLIT, Ex Infrastructure Reliability Engineer @ SPS

### Những điểm nhấn quan trọng (Key Highlights)
* **Ảo ảnh của những "Dashboard màu xanh":** Một hệ thống có CPU/RAM hoàn toàn ổn định không có nghĩa là người dùng đang sử dụng trơn tru. Demo thực tế cho thấy API Gateway có thể trả về HTTP 200 OK, nhưng transaction bên dưới database đã bị đứt gãy khiến người dùng không thể đăng nhập.
* **Tự động hóa bảo mật với Frontier Agent:** Thay vì chi trả hàng chục ngàn đô la và chờ đợi nhiều tuần cho các đợt pentest thủ công, Frontier Agent (được trợ lực bởi Amazon Bedrock) có thể tự động suy luận, quét mã nguồn và thực thi các kịch bản tấn công thực tế để tìm lỗ hổng.
* **Chiến thuật "Keyword Thinking":** Để chinh phục chứng chỉ CLF-C02, không cần học thuộc lòng mọi cấu hình mà cần rèn luyện tư duy nối từ khóa (ví dụ: "Decouple" = SQS) và kỹ năng dùng phương pháp loại trừ.

### Bài học đúc kết (Key Takeaways)
* **Tư duy True SLA:** Giám sát không phải là nhìn vào đồ thị phần cứng. Nó phải là một "Kim tự tháp" (Monitoring Pyramid) đi từ hạ tầng lên đến trải nghiệm người dùng cuối để phát hiện lỗi trước khi khách hàng phàn nàn.
* **Giới hạn của AI trong bảo mật:** Dù Frontier Agent có thể tự động kết hợp các lỗi phức tạp (như IDOR + XSS) giống như một hacker thực thụ, nó vẫn phải "bó tay" trước các chốt chặn vật lý hoặc logic cứng như Xác thực đa yếu tố (MFA). Con người vẫn là người nắm quyền kiểm soát cuối cùng.
* **Chiến lược phòng thi:** Tận dụng tối đa quyền lợi gia hạn thêm 30 phút cho người dùng tiếng Anh như ngôn ngữ thứ hai và sử dụng hiệu quả tính năng "Flag for review" để quản lý thời gian.

### Ứng dụng vào thực tế (Applying to Work)
* **Tái thiết kế hệ thống cảnh báo cho dự án:** Áp dụng bài học "Dashboard màu xanh", tôi thiết lập Amazon CloudWatch Alarm tập trung vào tỷ lệ lỗi của hàm Lambda xử lý giao dịch và số lượng tin nhắn bị đẩy vào SQS Dead-letter Queue (DLQ), thay vì chỉ đo lường thời gian chạy (duration).
* **Bảo mật API Serverless:** Tích hợp các ranh giới bảo mật cứng như Amazon Cognito (chống unauthorized access) và AWS WAF trước API Gateway, lấy cảm hứng từ việc MFA có thể chặn đứng các đợt càn quét tự động của Agent.
* **Chuẩn bị cho chứng chỉ AWS:** Khai thác tối đa AWS Free Tier để tự tay triển khai các dịch vụ thay vì chỉ học lý thuyết suông, áp dụng kỹ thuật "Keyword Thinking" để tăng tốc độ giải đề CLF-C02.

### Trải nghiệm sự kiện (Event Experience)
Tham gia sự kiện này mang lại cho tôi những cú "twist" thay đổi hoàn toàn tư duy vận hành hệ thống. 
* **Học hỏi từ chuyên gia:** Những câu chuyện xương máu về các ca "trực on-call" rớt mạng giữa đêm của các diễn giả giúp tôi hình dung rõ ràng áp lực thực tế của nghề Cloud/DevOps.
* **Góc nhìn công nghệ:** Việc chứng kiến Frontier Agent tự động vẽ ra một sơ đồ tấn công phức tạp ngay trên màn hình live demo đã cho tôi thấy tương lai của ngành DevSecOps sẽ thay đổi nhanh như thế nào.
* **Thảo luận thực tế:** Các diễn giả rất cởi mở khi nói về những giới hạn của công cụ (chi phí token API, các rào cản MFA), mang lại một góc nhìn công nghệ rất công tâm và thực dụng chứ không hề sáo rỗng.

### Tổng kết (Lessons Learned)
* Không bao giờ tin tưởng tuyệt đối vào thông số hệ thống nếu chưa xác minh được luồng thao tác của người dùng cuối (End-user journey).
* Bảo mật (Security) phải được tự động hóa và nhúng sâu vào vòng đời phát triển phần mềm (SDLC) chứ không phải là bước "làm cho có" ở khâu cuối cùng.
* Chứng chỉ AWS không chỉ là một danh hiệu, mà là khung tiêu chuẩn ép bản thân phải học hỏi kiến trúc Cloud một cách khoa học, bài bản nhất.

### Hình ảnh tham gia
<img src="/Internship-report-/images/4-EventParticipated/day20.jpg" width="80%" />
