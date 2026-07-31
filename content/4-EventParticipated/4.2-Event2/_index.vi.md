---
title: "Event 2: Agentic AI Build Week & Hackathon Showcase"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

### Mục tiêu sự kiện (Event Objectives)
* Thúc đẩy cộng đồng phát triển Trí tuệ nhân tạo tác tử (Agentic AI) và ứng dụng thực tiễn trên nền tảng AWS.
* Trình diễn các giải pháp công nghệ xuất sắc bước ra từ cuộc thi Hackathon 24 giờ.
* Kết nối mạng lưới chuyên gia AWS, chia sẻ kinh nghiệm xây dựng MVP (Minimum Viable Product), tối ưu chi phí và triển khai hệ thống chịu tải cao.

### Các đội thi và dự án tiêu biểu (Featured Teams & Projects)
* **Team AI-Powered Conversation Ordering** *(Anh Duy, Trần Đông, v.v.)*: Giải pháp KFC Bot Agent xử lý đơn hàng bằng ngôn ngữ tự nhiên.
* **Team SA Professional Native App** *(Thuận Phát, Hoàng Long, v.v.)*: Ứng dụng AI tự động hóa thiết kế kiến trúc AWS và sinh mã IaC.
* **Team Signal Scout** *(Tấn Lực, Hoàng Hiếu, v.v.)*: Nền tảng AI giám sát tín hiệu doanh nghiệp và tự động hóa CI/CD.
* **Team Hackathon Journey** *(An Khương, Quốc Huy, v.v.)*: Dự án S.H.E.P.H.E.R.D giám sát đám đông, đúc kết kinh nghiệm làm việc nhóm dưới áp lực cao.

### Những điểm nhấn quan trọng (Key Highlights)
* **Tự động hóa thiết kế hạ tầng (IaC):** Dự án SA Professional Native App gây ấn tượng mạnh khi sử dụng AI để thay thế các bước thủ công trong việc thu thập yêu cầu, vẽ sơ đồ kiến trúc và tự động sinh ra mã cơ sở hạ tầng (Infrastructure as Code), giúp tiết kiệm hàng chục giờ làm việc.
* **Tối ưu chi phí và Observability:** Đội Signal Scout mang đến bài toán thực tế về Service Discovery và giám sát hệ thống. Họ trình bày chi tiết về chi phí vận hành các dịch vụ AWS và cách kết hợp với các tool bên thứ 3 (LangFuse, Apify) để giảm thiểu phí duy trì hệ thống.
* **Độ chính xác của Agent:** Thông qua KFC Bot, sự kiện nhấn mạnh vào ranh giới giữa việc AI "hiểu" ngôn ngữ tự nhiên và việc AI "áp dụng đúng quy tắc kinh doanh" (business rules) để xác nhận đơn hàng mà không gây thất thoát tài chính.

### Bài học đúc kết (Key Takeaways)
* **Tư duy xây dựng MVP (Minimum Viable Product):** Trong khuôn khổ 24 giờ của Hackathon, các đội thi không cố gắng làm mọi thứ. Họ tập trung vào luồng tính năng cốt lõi nhất để chứng minh giải pháp hoạt động được, sau đó mới tính đến việc mở rộng.
* **Chiến lược quản trị chi phí Cloud:** Triển khai AI hay Serverless không chỉ là bài toán công nghệ, mà là bài toán kinh tế. Việc tính toán và dự báo chi phí (Cost Estimation) ngay từ bước thiết kế kiến trúc là bắt buộc.
* **Sức mạnh của làm việc nhóm:** Áp lực thời gian đòi hỏi sự phân chia rành mạch giữa người lo hạ tầng Cloud, người lo tích hợp AI và người chuẩn bị pitching.

### Ứng dụng vào thực tế (Applying to Work)
* **Cấu hình IaC cho dự án Serverless:** Lấy cảm hứng từ ý tưởng sinh mã hạ tầng của dự án SA Native App, tôi đã chủ động loại bỏ việc thao tác thủ công trên AWS Console. Thay vào đó, toàn bộ hạ tầng dự án **NaturEra Green Banking** được tôi đóng gói hoàn toàn thông qua file `template.yaml` của công cụ AWS SAM, đảm bảo khả năng triển khai nhất quán và tự động.
* **Tối ưu chi phí hạ tầng Green Banking:** Áp dụng tư duy phân tích chi phí từ đội Signal Scout, tôi đã thiết kế các bảng DynamoDB ở chế độ *On-Demand* và thiết lập mức dung lượng bộ nhớ phù hợp cho các hàm Lambda, giúp hệ thống tận dụng tối đa gói AWS Free Tier mà vẫn đảm bảo hiệu suất.
* **Quy trình phát triển tinh gọn:** Học hỏi tinh thần Hackathon, nhóm chúng tôi quyết định dồn toàn lực xử lý triệt để luồng API cốt lõi (luồng TransactWriteItems trừ tiền và cộng tín chỉ carbon) trước khi rẽ nhánh sang làm các tính năng phụ như EventBridge hay Cognito.

### Trải nghiệm sự kiện (Event Experience)
Được trực tiếp lắng nghe các kỹ sư trình bày thành quả sau 24 giờ code liên tục là một trải nghiệm cực kỳ truyền cảm hứng.
* **Khả năng giải quyết vấn đề:** Những khó khăn mà các đội gặp phải (lỗi phân quyền IAM, cấu hình sai bộ nhớ, tích hợp AI bị timeout) cũng chính là những lỗi tôi gặp phải khi làm đồ án. Việc nghe họ trình bày cách "Troubleshooting" giúp tôi có thêm rất nhiều góc nhìn mới.
* **Kỹ năng Pitching:** Không chỉ code giỏi, cách các đội truyền đạt ý tưởng, mô tả luồng Architecture một cách trực quan trước hội đồng giám khảo là kỹ năng mềm cực kỳ quý giá mà tôi học hỏi được để chuẩn bị cho buổi bảo vệ Workshop cuối kỳ.

### Tổng kết (Lessons Learned)
* Kiến trúc Cloud tốt nhất không phải là kiến trúc dùng nhiều công nghệ xịn nhất, mà là kiến trúc giải quyết được bài toán kinh doanh với chi phí vận hành tối ưu nhất.
* Kỹ năng làm việc nhóm và giao tiếp (khớp nối API, phân chia resource) quyết định 80% sự sống còn của dự án khi đối mặt với Deadline ngắn.
* Việc áp dụng Infrastructure as Code (IaC) là xu hướng tất yếu mà bất kỳ kỹ sư hệ thống nào cũng phải nắm vững để không bị tụt hậu.

### Hình ảnh tham gia
<img src="/images/4-EventParticipated/day25.jpg" width="80%" />
