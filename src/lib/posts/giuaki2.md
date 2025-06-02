---
title: ' Bài giữa kì - Deliverable 2'
date: '2025-05-12'
updated: '2025-05-12'
categories:
  - 'Lê Hùng Duy'
coverImage: '/images/logo.png'
coverWidth: 16
coverHeight: 9
excerpt: Ấn để xem thêm...
---

## **Deliverable 2: Thiết kế hệ thống**

### 1. Bản vẽ kiến trúc hệ thống

```
+-------------------+
|    Người dùng     |
+--------+----------+
         |
         v
+--------+----------+
|   Ứng dụng Todo   |  (CLI hoặc Web)
+--------+----------+
         |
         v
+--------+----------+
|    pupdb (JSON)   |
+-------------------+
```

---

### 2. Mô tả chi tiết các thành phần trong hệ thống

- **Người dùng:**  
  Tương tác với ứng dụng qua giao diện dòng lệnh (CLI) hoặc web (Flask).

- **Ứng dụng Todo list:**

  - Xử lý logic nghiệp vụ: thêm, sửa, xóa, hiển thị, đánh dấu hoàn thành task.
  - Giao tiếp với pupdb để lưu trữ và truy xuất dữ liệu.

- **PPupdb:**

  - Lưu trữ dữ liệu dưới dạng file JSON.
  - Đóng vai trò là database đơn giản cho ứng dụng.

- **Giao thức giao tiếp:**

  - Nếu là CLI: giao tiếp qua dòng lệnh.
  - Nếu là web: giao tiếp HTTP (Flask).

- **Thuật toán/Logic:**
  - CRUD cơ bản: Thêm, sửa, xóa, đọc dữ liệu.
  - Không sử dụng sharding/replication do ứng dụng nhỏ, đơn giản.

---

### 3. Công nghệ và thư viện sử dụng

- **Python:** Ngôn ngữ lập trình chính.
- **Pupdb:** Thư viện lưu trữ dữ liệu key-value.
- **Flask (nếu làm web):** Xây dựng giao diện web đơn giản.
- **Click/argparse (nếu làm CLI):** Xử lý tham số dòng lệnh.
- **Lý do chọn:**
  - Đơn giản, dễ học, phù hợp với quy mô đề tài.
  - pupdb giúp lưu trữ dữ liệu nhanh, không cần cài đặt phức tạp.

---

### 4. Mô hình dữ liệu (Database Model)

**Task**

- id: string (unique)
- title: string
- description: string
- status: boolean (hoàn thành/chưa hoàn thành)
- created_at: datetime

**Ví dụ lưu trữ trong pupdb (JSON):**

```json
{
	"tasks": [
		{
			"id": "1",
			"title": "Học bài",
			"description": "Ôn tập chương 1",
			"status": false,
			"created_at": "2024-06-01T10:00:00"
		}
	]
}
```

---

### 5. Chiến lược triển khai và cấu hình hệ thống

- **Triển khai:**
  - Ứng dụng chạy trực tiếp trên máy cá nhân, không cần server riêng.
  - Nếu cần, có thể đóng gói bằng Docker để dễ triển khai trên nhiều môi trường.
- **Cấu hình:**
  - Cài đặt Python, pip, thư viện pupdb.
  - Cấu hình đường dẫn file lưu trữ dữ liệu (mặc định là file JSON trong thư mục dự án).
