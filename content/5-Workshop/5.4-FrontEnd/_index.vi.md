---
title : "Thiết lập Frontend"
date : 2026-07-30
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Thiết lập Frontend (React & Vite)

Để thuận tiện cho việc thực hành Workshop, phần Frontend giao diện người dùng (Customer Dashboard) và giao diện giả lập (Mock POS Terminal) đã được chuẩn bị sẵn dưới dạng skeleton code. Bạn sẽ tiến hành tải mã nguồn, cấu hình môi trường và chạy thử ứng dụng.

---

### 1. Cấu trúc thư mục (Directory Structure)

Dự án sử dụng kiến trúc Monorepo với **React kết hợp Vite** để tối ưu tốc độ build. Dưới đây là cấu trúc các thư mục quan trọng bạn cần nắm:

```text
naturEra-green-banking-web/
  +-- apps/
  |   \-- web/                  # Thư mục chính chứa phần Frontend
  |       +-- public/           # Chứa các file tĩnh chung
  |       +-- src/              # Thư mục chứa toàn bộ mã nguồn React
  |       |   +-- assets/       # Hình ảnh tĩnh (hero.png, react.svg, vite.svg)
  |       |   +-- apiService.js # Nơi xử lý gọi API (fetch/axios) tới Backend
  |       |   +-- App.jsx       # Root component, chứa khung giao diện chính
  |       |   +-- config.js     # Chứa các thông số cấu hình dự án
  |       |   +-- index.css     # File định dạng CSS toàn cục
  |       |   \-- main.jsx      # Entry point khởi chạy ứng dụng React
  |       +-- .env.local        # File cấu hình biến môi trường tại máy local
  |       +-- index.html        # File HTML gốc của ứng dụng Vite
  |       +-- package.json      # Danh sách thư viện (Dependencies) của ứng dụng
  |       \-- vite.config.js    # Cấu hình đóng gói Vite
  \-- package.json              # Cấu hình dependencies chung của toàn dự án
```


---

### 2. Tải mã nguồn và Cài đặt thư viện

Mở terminal tại thư mục làm việc của bạn và chạy các lệnh sau để tải source code và cài đặt các phụ thuộc (dependencies) cần thiết cho React:

#### Bước 1: Clone repository của dự án
```bash
git clone [https://github.com/Kenjtermine/naturEra-green-banking-web.git](https://github.com/Kenjtermine/naturEra-green-banking-web.git)
cd naturEra-green-banking-web
cd apps/web
```

#### Bước 2: Cài đặt các thư viện
Quá trình này mất khoảng 1-2 phút:
```bash
npm install
```

<img src="/Internship-report-/images/5-Workshop/5.5-FrontEnd/2-npm.png" width="80%" />

---

### 3. Cấu hình biến môi trường (Environment Variables)

Đây là bước cực kỳ quan trọng. Frontend cần biết địa chỉ của API Gateway và thông tin của Amazon Cognito (đã được tạo ra từ phần deploy Backend bằng AWS SAM) để có thể hoạt động.

Tại thư mục `apps/web/`, bạn hãy tạo một file có tên là `.env.local` (hoặc copy từ file mẫu nếu có).

Mở file `.env.local` lên và điền các giá trị Outputs mà bạn nhận được sau khi chạy lệnh `sam deploy` ở bước trước:

```env
# Địa chỉ API Gateway (Lấy từ Output của SAM)
VITE_API_GATEWAY_URL=https://<nhập-api-id>[.execute-api.ap-southeast-1.amazonaws.com/Stage](https://.execute-api.ap-southeast-1.amazonaws.com/Stage)

# Cấu hình AWS Cognito để Đăng nhập (Lấy từ Output của SAM)
VITE_COGNITO_USER_POOL_ID=ap-southeast-1_<nhập-pool-id>
VITE_COGNITO_CLIENT_ID=<nhập-app-client-id>

# API Key dùng để gọi endpoint quẹt thẻ POS
VITE_POS_API_KEY=<nhập-mã-api-key>
```

> ⚠️ **Lưu ý:** Bạn không được để trống các trường này, nếu không giao diện sẽ báo lỗi 404 hoặc không thể đăng nhập.

> <img src="/Internship-report-/images/5-Workshop/5.5-FrontEnd/3-env.png" width="80%" />

---

### 4. Chạy ứng dụng tại Local

Sau khi đã cấu hình xong biến môi trường, bạn tiến hành khởi động môi trường phát triển (Development Server):

```bash
npm run dev
```

Terminal sẽ hiển thị đường dẫn (thường là `http://localhost:5173`). Bạn bấm `Ctrl + Click` (hoặc `Cmd + Click` trên Mac) vào đường link đó để mở giao diện NaturEra Green Banking trên trình duyệt và bắt đầu trải nghiệm!

<img src="/Internship-report-/images/5-Workshop/5.5-FrontEnd/4-login.png" width="80%" />
<img src="/Internship-report-/images/5-Workshop/5.5-FrontEnd/5-web.png" width="80%" />