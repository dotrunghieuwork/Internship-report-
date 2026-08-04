---
title : "Triển khai Frontend lên AWS"
date : 2026-07-30
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Triển khai Frontend lên AWS

Sau khi đã chạy thử thành công giao diện tại máy cá nhân, bước tiếp theo là đưa mã nguồn lên môi trường đám mây để người dùng thực tế có thể truy cập. Chúng ta sẽ sử dụng kiến trúc lưu trữ tĩnh với Amazon S3 và mạng phân phối nội dung (CDN) Amazon CloudFront.

---

### 1. Khởi tạo Amazon S3 Bucket (Lưu trữ tĩnh)

Thay vì thuê một máy chủ (EC2) đắt đỏ chỉ để chạy giao diện web, chúng ta sẽ sử dụng S3 kết hợp CloudFront. Kiến trúc này mang lại hiệu năng cao nhất với chi phí gần như bằng 0.

**Tại sao chọn kiến trúc này?**

| QUYẾT ĐỊNH | LÝ DO |
| :--- | :--- |
| **Amazon S3** | Lưu trữ các file tĩnh (HTML, CSS, JS) sau khi build cực kỳ rẻ. |
| **Amazon CloudFront** | Mạng phân phối nội dung (CDN) toàn cầu, giúp web tải nhanh và tự động có HTTPS. |
| **Origin Access Control (OAC)** | Khóa chặt S3, không cho ai truy cập trực tiếp từ Internet, mọi luồng phải đi qua CloudFront. |
| **Custom Error Pages** | Điểm mấu chốt để fix lỗi 404 khi người dùng bấm F5 (Refresh) trang trên React SPA. |

**Các bước tạo Bucket:**

1. Đăng nhập AWS Console, tìm dịch vụ **S3** và chọn Region `ap-southeast-2` (Sydney).
2. Nhấn **Create bucket**.
3. **Bucket name**: Đặt tên duy nhất (Ví dụ: `naturera-green-banking-dev-frontendbucket-...`).
4. **Block Public Access settings for this bucket**: Đảm bảo **BẬT (Check)** dòng *Block all public access*. (Chúng ta sẽ dùng OAC của CloudFront để truy cập thay vì mở public).
5. Cuộn xuống cuối và nhấn **Create bucket**.

> <img src="/Internship-report-/images/5-Workshop/5.5-hosting/s3.png" width="80%" />


---

### 2. Cấu hình Amazon CloudFront (Phân phối & Tối ưu)

Sau khi có nơi lưu trữ, chúng ta cần một "cánh cửa" CDN để phân phối web ra toàn thế giới.

**2.1. Tạo Distribution & Kết nối S3 (OAC)**
1. Chuyển sang dịch vụ **CloudFront** → Nhấn **Create Distribution**.
2. **Origin domain**: Chọn tên S3 bucket bạn vừa tạo ở bước 1.
3. **Origin access**: Chọn **Origin access control settings (recommended)**.
   * Nhấn *Create control setting* và giữ nguyên mặc định.
4. **Viewer protocol policy**: Chọn **Redirect HTTP to HTTPS** để bắt buộc dùng kết nối bảo mật.
5. **Web Application Firewall (WAF)**: Chọn *Do not enable security protections* (để tiết kiệm chi phí cho môi trường Dev).
6. Nhấn **Create distribution**.

> **QUAN TRỌNG:** Sau khi tạo xong, CloudFront sẽ hiện một cảnh báo màu vàng yêu cầu cập nhật S3 Bucket Policy. Hãy nhấn **Copy policy**, quay lại S3 Bucket → tab *Permissions* → *Bucket Policy* → Dán đoạn JSON đó vào và lưu lại. Nếu bỏ qua bước này, CloudFront sẽ bị lỗi 403 Access Denied.


**2.2. Cấu hình Custom Error Responses (Fix lỗi F5 của React SPA)**
Vì ứng dụng dùng React Router, nếu người dùng truy cập thẳng đường dẫn con (VD: `/dashboard`) hoặc nhấn F5, S3 sẽ không tìm thấy thư mục `/dashboard` và trả về lỗi 403/404.

1. Trong giao diện CloudFront Distribution của bạn, chuyển sang tab **Error pages**.
2. Nhấn **Create custom error response**.
3. Cấu hình xử lý lỗi 403:
   * **HTTP error code**: `403: Forbidden`
   * **Customize error response**: Yes
   * **Response page path**: `/index.html`
   * **HTTP Response Code**: `200: OK`
4. Lặp lại bước trên để tạo thêm một rule tương tự cho **HTTP error code**: `404: Not Found`.

---

### 3. Build & Deploy ứng dụng

Trước khi build code đẩy lên S3, chúng ta cần đảm bảo Frontend đã được kết nối đúng với Backend API Gateway (từ bài Lab trước) để không bị lỗi CORS.

**Bước 1: Kiểm tra Biến môi trường**
Mở mã nguồn thư mục Frontend bằng VS Code. Kiểm tra file `.env.local` và đảm bảo các biến trỏ đúng về URL của API Gateway:

```env
VITE_API_GATEWAY_URL=https://<api-id>[.execute-api.ap-southeast-2.amazonaws.com/Prod](https://.execute-api.ap-southeast-2.amazonaws.com/Prod)
VITE_COGNITO_USER_POOL_ID=ap-southeast-2_<pool-id>
```
*(Lưu ý: Để gọi được API thành công, hãy chắc chắn rằng trong source code AWS Lambda của Backend, các hàm đều trả về Header: `"Access-Control-Allow-Origin": "*" `).*

**Bước 2: Build mã nguồn React/Vite**
Mở Terminal tại thư mục gốc của frontend và chạy lệnh:
```bash
npm run build
```
*(Lệnh này sẽ nén toàn bộ code và sinh ra thư mục `dist/`)*

**Bước 3: Deploy lên S3 bằng AWS CLI**
Sử dụng lệnh `s3 sync` để tự động đối chiếu và đồng bộ các file mới lên Bucket của bạn:
```bash
aws s3 sync dist/ s3://<tên-bucket-của-bạn> --delete
```
*(Tham số `--delete` giúp xóa các file cũ trên S3 không còn tồn tại trong thư mục `dist` nội bộ, giữ cho Bucket luôn sạch sẽ).*

**Hoàn tất!** Bây giờ bạn có thể lấy **Distribution domain name** (VD: `d21mxs1a....cloudfront.net`) từ CloudFront Console, dán vào trình duyệt và chiêm ngưỡng ứng dụng NaturEra Green Banking của mình đang chạy trực tiếp trên AWS!