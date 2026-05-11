# 🤝 Hướng dẫn đóng góp — GoldenSpoons

Cảm ơn bạn đã quan tâm đến dự án **GoldenSpoons** — Website đặt bàn nhà hàng trực tuyến.  
Tài liệu này hướng dẫn các thành viên trong nhóm cách thiết lập môi trường, quy trình làm việc với Git, tiêu chuẩn code và các quy tắc chung khi cộng tác.

---

## 📑 Mục lục

1. [Thành viên nhóm](#-thành-viên-nhóm)
2. [Yêu cầu môi trường](#-yêu-cầu-môi-trường)
3. [Cài đặt dự án](#-cài-đặt-dự-án)
4. [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
5. [Quy trình Git](#-quy-trình-git)
6. [Quy tắc đặt tên nhánh](#-quy-tắc-đặt-tên-nhánh)
7. [Quy tắc Commit Message](#-quy-tắc-commit-message)
8. [Quy trình tạo Pull Request](#-quy-trình-tạo-pull-request)
9. [Tiêu chuẩn viết code](#-tiêu-chuẩn-viết-code)
10. [Báo lỗi & Đề xuất tính năng](#-báo-lỗi--đề-xuất-tính-năng)
11. [Liên hệ](#-liên-hệ)

---

## 👥 Thành viên nhóm

| Họ và tên | MSSV | Vai trò / Phần phụ trách |
|-----------|------|--------------------------|
| Nguyễn Thị Tố Đạt | 23810310... | Trưởng nhóm, Backend |
| Bùi Minh Đức | 23810310110 | Frontend |

---

## 🖥️ Yêu cầu môi trường

Trước khi bắt đầu, hãy đảm bảo máy bạn đã cài đặt đầy đủ các công cụ sau:

| Công cụ | Phiên bản tối thiểu | Ghi chú |
|---------|---------------------|---------|
| PHP | >= 8.1 | Cần extension: mbstring, pdo_mysql, openssl |
| Composer | >= 2.x | Quản lý package PHP |
| Node.js | >= 18.x | Kèm npm |
| MySQL | >= 8.0 | Hoặc dùng XAMPP |
| Git | >= 2.x | |

> **Khuyến nghị:** Dùng [XAMPP](https://www.apachefriends.org/) trên Windows hoặc cài đặt thủ công trên Linux/macOS.

---

## 🚀 Cài đặt dự án

### 1. Clone repository

```bash
git clone https://github.com/NTTDat7525/GoldenSpoons.git
cd GoldenSpoons
```

### 2. Cài đặt các package PHP

```bash
composer install
```

### 3. Cài đặt các package Node.js

```bash
npm install
```

### 4. Tạo file cấu hình môi trường

```bash
cp .env.example .env
php artisan key:generate
```

### 5. Cấu hình file `.env`

Mở file `.env` và chỉnh sửa thông tin kết nối database:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=goldenspoons
DB_USERNAME=root
DB_PASSWORD=
```

### 6. Tạo database và chạy migration

```bash
# Tạo database tên 'goldenspoons' trong MySQL trước, sau đó:
php artisan migrate --seed
```

### 7. Khởi động server

```bash
php artisan serve
```

Truy cập ứng dụng tại: [http://localhost:8000](http://localhost:8000)

### 8. Build assets (nếu dùng Vite)

```bash
npm run dev       # Môi trường phát triển
npm run build     # Build production
```

---

## 📁 Cấu trúc thư mục

```
GoldenSpoons/
├── app/
│   ├── Http/
│   │   ├── Controllers/    # Xử lý logic điều hướng
│   │   └── Middleware/     # Middleware xác thực, phân quyền
│   └── Models/             # Eloquent Models (User, Table, Reservation...)
├── database/
│   ├── migrations/         # Lịch sử tạo/thay đổi bảng
│   └── seeders/            # Dữ liệu mẫu
├── resources/
│   ├── views/              # Blade templates (giao diện)
│   ├── css/                # Stylesheet
│   └── js/                 # JavaScript
├── routes/
│   ├── web.php             # Định tuyến web
│   └── api.php             # Định tuyến API (nếu có)
├── public/                 # Tài nguyên public (ảnh, css biên dịch)
├── storage/                # File upload, log
├── .env.example            # Mẫu cấu hình môi trường
└── CONTRIBUTING.md         # File này
```

---

## 🌿 Quy trình Git

Dự án sử dụng mô hình **Feature Branch Workflow**:

```
main ← dev ← feature/tên-tính-năng
              fix/tên-lỗi
```

| Nhánh | Mục đích |
|-------|----------|
| `main` | Nhánh chính — chỉ chứa code ổn định, đã được kiểm tra |
| `dev` | Nhánh phát triển — tích hợp tất cả tính năng mới |
| `feature/...` | Phát triển tính năng mới |
| `fix/...` | Sửa lỗi |
| `docs/...` | Cập nhật tài liệu |

> ⚠️ **Nghiêm cấm push trực tiếp lên nhánh `main` hoặc `dev`.**  
> Mọi thay đổi phải thông qua Pull Request và được ít nhất 1 thành viên review.

---

## 🏷️ Quy tắc đặt tên nhánh

Tên nhánh phải **viết thường**, dùng dấu gạch ngang (`-`), không dấu, không khoảng trắng.

```
feature/dat-ban-online
feature/quan-ly-thuc-don
fix/loi-validate-form-dang-ky
fix/khong-gui-duoc-email-xac-nhan
docs/cap-nhat-readme
```

---

## 📝 Quy tắc Commit Message

Commit message theo định dạng:

```
<loại>: <mô tả ngắn gọn>
```

### Các loại commit

| Loại | Ý nghĩa |
|------|---------|
| `feat` | Thêm tính năng mới |
| `fix` | Sửa lỗi |
| `docs` | Thay đổi tài liệu |
| `style` | Chỉnh sửa giao diện, CSS (không thay đổi logic) |
| `refactor` | Tái cấu trúc code, không thêm tính năng hay sửa lỗi |
| `test` | Thêm hoặc sửa test |
| `chore` | Cập nhật cấu hình, dependency |

### Ví dụ commit message hợp lệ

```
feat: thêm chức năng đặt bàn theo giờ
fix: sửa lỗi không hiển thị bàn trống cuối tuần
docs: cập nhật hướng dẫn cài đặt trong README
style: chỉnh màu nút xác nhận đặt bàn
refactor: tách logic đặt bàn sang ReservationService
```

### Quy tắc bổ sung

- Mô tả **ngắn gọn**, **rõ ràng**, tối đa 72 ký tự
- Viết bằng **tiếng Việt** để cả nhóm dễ đọc
- Dùng **thì hiện tại** ("thêm", "sửa", "cập nhật" — không dùng "đã thêm", "đã sửa")
- Không viết tắt khó hiểu

---

## 🔀 Quy trình tạo Pull Request

### Bước 1 — Tạo nhánh mới từ `dev`

```bash
git checkout dev
git pull origin dev
git checkout -b feature/ten-tinh-nang
```

### Bước 2 — Phát triển và commit

```bash
git add .
git commit -m "feat: mô tả tính năng"
```

### Bước 3 — Push nhánh lên GitHub

```bash
git push origin feature/ten-tinh-nang
```

### Bước 4 — Tạo Pull Request trên GitHub

Vào repository trên GitHub → **New Pull Request** → chọn:
- **base:** `dev`
- **compare:** `feature/ten-tinh-nang`

### Checklist trước khi tạo PR

- [ ] Code đã chạy được trên máy local, không có lỗi
- [ ] Đã kiểm tra các trường hợp ngoại lệ (input rỗng, dữ liệu sai...)
- [ ] Không để lại `dd()`, `var_dump()`, `console.log()` trong code
- [ ] Mô tả PR rõ ràng: làm gì, tại sao, cách test
- [ ] Không có conflict với nhánh `dev`

### Quy tắc review

- Mỗi PR cần **ít nhất 1 thành viên khác** approve trước khi merge
- Người review có thể **Request Changes** nếu cần chỉnh sửa
- Người tạo PR chịu trách nhiệm **resolve conflict** nếu có

---

## 🧹 Tiêu chuẩn viết code

### PHP / Laravel

- Tuân theo chuẩn **PSR-12**
- Đặt tên theo quy ước Laravel:
  - **Controller:** `PascalCase` + hậu tố `Controller` — `ReservationController`
  - **Model:** `PascalCase` số ít — `Reservation`, `Table`, `User`
  - **Migration:** `snake_case` — `create_reservations_table`
  - **Route:** `kebab-case` — `/dat-ban`, `/quan-ly-ban`
  - **Biến & hàm:** `camelCase` — `$tableId`, `getAvailableTables()`
- Không để business logic trong Controller — tách sang **Service** hoặc **Repository** nếu cần
- Validate dữ liệu bằng **Form Request**, không validate thủ công trong Controller

### Blade / HTML

- Không viết inline CSS hay JS trực tiếp trong file `.blade.php`
- Sử dụng **Blade component** hoặc **include** để tái sử dụng giao diện
- Đặt tên file view theo `snake_case`: `reservation_form.blade.php`

### JavaScript / CSS

- Đặt tên biến và hàm bằng **camelCase**
- Không dùng `var`, ưu tiên `const` và `let`
- CSS class theo quy ước **BEM** hoặc nhất quán với cả nhóm

### Chung

- Xóa code thừa, comment thừa trước khi commit
- Không commit file `.env`, `node_modules/`, `vendor/`, `storage/logs/`
- Thêm comment giải thích cho những đoạn code phức tạp

---

## 🐛 Báo lỗi & Đề xuất tính năng

Vui lòng dùng **GitHub Issues** để báo lỗi hoặc đề xuất:

1. Vào tab **Issues** → **New Issue**
2. Chọn template phù hợp (Bug Report / Feature Request)
3. Gắn **label** tương ứng:
   - `bug` — Lỗi trong ứng dụng
   - `enhancement` — Đề xuất cải tiến / tính năng mới
   - `question` — Thắc mắc, cần thảo luận
   - `urgent` — Lỗi nghiêm trọng cần xử lý gấp

### Mẫu báo lỗi

```
**Mô tả lỗi:**
[Mô tả ngắn gọn vấn đề gặp phải]

**Các bước tái hiện:**
1. Vào trang ...
2. Nhấn vào ...
3. Kết quả thấy ...

**Kết quả kỳ vọng:**
[Hệ thống nên hoạt động như thế nào]

**Môi trường:**
- OS: Windows 10 / Ubuntu 22.04
- PHP: 8.2
- Browser: Chrome 124
```
