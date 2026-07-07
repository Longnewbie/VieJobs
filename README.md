# VieJobs - Nền Tảng Tuyển Dụng Tích Hợp AI

VieJobs là một ứng dụng web toàn diện dành cho tuyển dụng và tìm kiếm việc làm. Dự án nổi bật với việc ứng dụng AI vào quy trình tuyển dụng, giúp trích xuất thông tin từ CV và kết hợp với các mô hình AI để tối ưu hóa việc phân tích và đánh giá ứng viên.

---

## ✨ Tính năng Nổi bật (Key Features)

### Dành cho Ứng viên (Candidates)
- **Tìm kiếm & Lọc việc làm:** Tìm kiếm việc làm dễ dàng theo từ khóa, vị trí, ngành nghề và mức lương.
- **Quản lý Hồ sơ & CV:** Tạo CV trực tiếp trên nền tảng hoặc tải lên CV cá nhân.
- **Theo dõi Ứng tuyển:** Nộp đơn ứng tuyển và theo dõi trạng thái hồ sơ (Chờ duyệt, Được gọi phỏng vấn, Từ chối).
- **Gợi ý Việc làm:** Được đề xuất các công việc phù hợp dựa trên kỹ năng và hồ sơ cá nhân.

### Dành cho Nhà tuyển dụng (Recruiters)
- **Quản lý Tin tuyển dụng:** Tạo, chỉnh sửa, đóng/mở các tin tuyển dụng một cách nhanh chóng.
- **Quản lý Ứng viên:** Xem danh sách ứng viên nộp đơn, phân loại và thay đổi trạng thái tuyển dụng.
- **AI Phân tích & Đánh giá CV:** Sử dụng công nghệ OCR và LLM (OpenAI/Google GenAI) để tự động trích xuất thông tin từ CV (PDF), phân tích và chấm điểm mức độ phù hợp của ứng viên với yêu cầu công việc.

### Dành cho Quản trị viên (Admins)
- **Bảng điều khiển (Dashboard):** Xem các biểu đồ và thống kê trực quan về hoạt động của hệ thống (lượt ứng tuyển, số lượng tin đăng,...).
- **Quản lý Người dùng & Công ty:** Quản lý tài khoản, xét duyệt tư cách nhà tuyển dụng và kiểm duyệt nội dung tin đăng.

---

## 🏗 Kiến trúc Hệ Thống (Architecture)

VieJobs sử dụng kiến trúc **Client-Server**, vận hành thông qua các API RESTful:

- **Frontend:** 
  - Là một SPA xây dựng trên nền tảng React và Vite.
  - Xử lý toàn bộ giao diện người dùng, quản lý trạng thái và routing phía client.
  - Được phân chia module rõ ràng cho các vai trò khác nhau như: Ứng viên, Nhà tuyển dụng và Quản trị viên.
  
- **Backend:** 
  - Xây dựng bằng Node.js và Express, đóng vai trò cung cấp RESTful API.
  - Xử lý logic nghiệp vụ, xác thực người dùng (JWT), xử lý file uploads và quản lý tương tác với cơ sở dữ liệu.
  - **Tích hợp AI & Xử lý tài liệu:** Cung cấp các pipeline đặc biệt để đọc file PDF, nhận dạng ký tự quang học, và giao tiếp với các dịch vụ AI như OpenAI và Google GenAI để đánh giá CV tự động.

- **Cơ sở dữ liệu (Database):**
  - **MongoDB**: Là cơ sở dữ liệu chính lưu trữ thông tin user, job, application, etc.

---

## 💻 Công nghệ Sử dụng (Tech Stack)

### 🎨 Frontend
- **Core:** React 19, TypeScript, Vite
- **Styling & UI Components:** 
  - Tailwind CSS v4, Framer Motion (Animations)
  - Radix UI (Primitives) kết hợp với class-variance-authority và tailwind-merge (Cơ sở để xây dựng Shadcn UI)
  - Lucide React, FontAwesome, React Icons
- **State Management & Data Fetching:** Redux Toolkit, React Query (@tanstack/react-query)
- **Routing:** React Router DOM v7
- **Bản đồ & Biểu đồ:** React Leaflet, Chart.js, Recharts
- **Tiện ích khác:** Axios, Day.js / Moment, SweetAlert2, Sonner, TinyMCE (Rich text editor), html2pdf.js (Export PDF).

### ⚙️ Backend
- **Core:** Node.js, Express 5
- **Database:** MongoDB
- **AI & Document Processing:** 
  - `@google/genai`, `openai` (Xử lý ngôn ngữ tự nhiên)
  - `pdf-parse`, `pdfjs-dist`, `pdf2pic` (Xử lý file PDF)
  - `tesseract.js` (Nhận dạng văn bản trong hình ảnh/PDF)
- **File Upload:** Multer, Cloudinary (Lưu trữ media)
- **Bảo mật & Tiện ích:** JWT (JSON Web Token), bcryptjs, nodemailer, express-rate-limit, node-cron.

### 🐳 Hạ tầng & Triển khai (Infrastructure)
- Docker & Docker Compose (cho phép chạy song song cả FE & BE dễ dàng trong container).

## 📁 Cấu trúc Thư mục (Folder Structure)

```text
VieJobs/
├── be/                       # Backend source code
│   ├── src/                  # Thư mục mã nguồn chính
│   │   ├── controllers/      # Logic xử lý cho các API
│   │   ├── middleware/       # Các hàm trung gian 
│   │   ├── models/           # Định nghĩa database
│   │   ├── routes/           # Định nghĩa các endpoints API
│   │   └── server.js         # File cấu hình server
│   ├── Dockerfile            # Cấu hình build Docker image cho backend
│   └── package.json
│
├── fe/                       # Frontend source code
│   ├── public/               # Tài nguyên tĩnh
│   ├── src/                  # Thư mục mã nguồn chính
│   │   ├── components/       # Các React components có thể tái sử dụng
│   │   │   ├── ui/           # Các UI components cơ bản
│   │   │   ├── admin/        # Components dành riêng cho Admin
│   │   │   └── recruiter/    # Components dành riêng cho Recruiter
│   │   ├── redux/            # Cấu hình Redux Toolkit & Slices
│   │   ├── types/            # TypeScript interfaces & types
│   │   └── App.tsx           # Component gốc của ứng dụng
│   ├── Dockerfile            # Cấu hình build Docker image cho frontend
│   └── package.json
│
├── docker-compose.yml        # Tệp cấu hình chạy song song FE & BE bằng Docker
└── README.md                 # Tài liệu mô tả dự án
```
