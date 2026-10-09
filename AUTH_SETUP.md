# Thiết lập đăng ký và đăng nhập

Luồng xác thực dùng Supabase Auth. Không mở trang bằng `file://`; hãy chạy bằng Live Server hoặc một máy chủ web cục bộ.

## 1. Tạo dự án Supabase

1. Tạo một dự án tại [supabase.com](https://supabase.com/).
2. Trong phần API settings, lấy Project URL và publishable key (hoặc anon key cũ).
3. Điền hai giá trị vào `supabase-config.js`:

```js
window.SUPABASE_CONFIG = {
    url: "https://your-project.supabase.co",
    anonKey: "your-publishable-key"
};
```

Chỉ dùng publishable/anon key ở trình duyệt. Không đưa `secret` hoặc `service_role` key vào file này.

## 2. Bật email OTP

1. Trong Authentication > Sign In / Providers, bật Email và bật xác nhận email.
2. Trong Authentication > Email Templates, sửa mẫu xác nhận đăng ký để nội dung có `{{ .Token }}`, ví dụ: `Mã xác minh của bạn là {{ .Token }}`. Không thay mã bằng đường dẫn `{{ .ConfirmationURL }}` nếu muốn nhập mã 6 số.
3. Để gửi tới email thật bất kỳ, mở Authentication > SMTP Settings và cấu hình SMTP từ Resend, Brevo hoặc nhà cung cấp tương tự. SMTP mặc định của Supabase chỉ gửi tới một số địa chỉ được cho phép và bị giới hạn gửi.
4. Trong Authentication > URL Configuration, đặt Site URL theo địa chỉ Live Server đang dùng, thường là `http://127.0.0.1:5500`.

Sau khi nhập đúng mã email, trang chuyển về chế độ đăng nhập. Đăng nhập bằng chính email và mật khẩu vừa tạo sẽ mở `index.html`.