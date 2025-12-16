1. IMPORT file json trong folder "database" vào mongodb compass

2. GỬI Gmail (myaccount.google.com)
Chuẩn bị tài khoản gửi (Gmail):
Đăng nhập Gmail -> Vào cài đặt bảo mật -> Bật "2-Step Verification".
Tạo App Password (Mật khẩu ứng dụng). (Lấy chuỗi mật khẩu 16 ký tự đó.) (MAIL_PASS trong .env backend) (không khoảng trắng, không dấu ngoặc kép)
GOOGLE_CLIENT_ID : trong frontend app/layout.tsx


3. CẤU HÌNH TÀI KHOẢN SEPAY
Đăng ký: Tạo tài khoản tại my.sepay.vn
Thêm ngân hàng: Vào menu "Ngân hàng" -> Thêm tài khoản (MB Bank, VCB...).
Kết nối:
Liên kết ngân hàng
Tạo webhook :
    Gán URL : public_url_backend(cloudflared)/webhook/sepay
    Xác thực API key trên SePay trùng với SEPAY_API_KEY(.env)
Cơ chế: Khách chuyển tiền -> App Ngân hàng báo notification -> App SePay bắt notification -> Gọi về backend về Server -> Xác thực -> Thao tác ghi nhận trên dữ liệu


4. Run
// Run frontend : 
cd frontend
npm run dev

// Run backend
cd backend
npm run start:dev

// Run public url backend thanh toán SePay gọi API trong webhook(backend)
cloudflared tunnel --url http://localhost:4000
--> setup webhook trong trang tài khoản SePay
--> Sửa file frontend/config/bank.config.ts

// Run chatbot
pip install fastapi uvicorn google-genai sentence-transformers faiss-cpu python-multipart
export GEMINI_API_KEY=...
uvicorn gemini:app --port 8000 --reload
