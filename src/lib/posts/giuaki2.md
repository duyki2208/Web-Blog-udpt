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



## 1. Bản vẽ kiến trúc hệ thống

![alt text](../../../images/kientruchethongtodolist.png)

---

## 2. Mô tả chi tiết các thành phần trong hệ thống


### 1. Frontend (Web Browser)
**Vai trò:**
- Hiển thị giao diện người dùng
- Xử lý tương tác người dùng
- Gửi/nhận dữ liệu từ server

**Cách hoạt động:**
- Sử dụng React để xây dựng Single Page Application
- Gửi request đến backend qua REST API
- Nhận real-time updates qua WebSocket
- Quản lý state và UI updates

### 2. API Gateway
**Vai trò:**
- Quản lý và định tuyến các request
- Bảo mật hệ thống
- Kiểm soát lưu lượng

**Cách hoạt động:**
- Nhận request từ client
- Kiểm tra authentication
- Chuyển tiếp request đến backend
- Trả về response cho client

### 3. Backend Server (Flask)
**Vai trò:**
- Xử lý business logic
- Quản lý database
- Xử lý authentication
- Quản lý sessions

**Cách hoạt động:**
- Nhận request từ API Gateway
- Xử lý logic nghiệp vụ
- Tương tác với database
- Trả về kết quả cho client

### 4. Database (PupDB)
**Vai trò:**
- Lưu trữ dữ liệu
- Quản lý transactions
- Đảm bảo data consistency

**Cách hoạt động:**
- Lưu trữ dữ liệu dưới dạng file
- Tự động backup
- Xử lý concurrent access
- Quản lý data integrity

### 5. Giao Thức Giao Tiếp

#### 1. **REST API**

**Vai trò:**
- Giao tiếp giữa client và server
- Xử lý CRUD operations
- Quản lý resources

**Cách hoạt động:**
- Sử dụng HTTP methods (GET, POST, PUT, DELETE)
- Dữ liệu được truyền dưới dạng JSON
- Mỗi request là độc lập
- Sử dụng status codes để thông báo kết quả

#### 2. WebSocket
**Vai trò:**
- Real-time communication
- Bi-directional data flow
- Event handling

**Cách hoạt động:**
- Duy trì kết nối liên tục
- Gửi/nhận dữ liệu real-time
- Tự động reconnect khi mất kết nối
- Xử lý events

### 6. Storage System
**Vai trò:**
- Lưu trữ static files
- Quản lý user uploads
- Cache management

**Cách hoạt động:**
- Lưu trữ file trên local filesystem
- Quản lý file permissions
- Xử lý file operations
- Cache frequently accessed data

### 7. Monitoring System
**Vai trò:**
- Theo dõi hệ thống
- Ghi log
- Báo lỗi

**Cách hoạt động:**
- Ghi log các events và errors
- Theo dõi performance
- Gửi alerts khi có vấn đề
- Tạo reports


---

## 3. Công nghệ và thư viện sử dụng

1. **Flask** 
- Đơn giản, dễ học và sử dụng
- Microframework phù hợp cho ứng dụng nhỏ

2. **React (Frontend Framework)**

- Component-based architecture giúp code dễ quản lý
- Virtual DOM cho performance tốt

3. **PupDB** 
- File-based database đơn giản
- Không cần setup phức tạp

4. **REST API + WebSocket**

- REST API: Standard và widely used
- WebSocket: Real-time communication

5. **Docker** 

- Environment consistency
- Easy deployment

6. **Material-UI** 

- Modern và đẹp
- Responsive design




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

## 5. Chiến lược triển khai và cấu hình hệ thống

1. **Containerization với Docker**
- **Dockerfile** cho mỗi service
- **Docker Compose** cho development
- **Kubernetes** cho production

2. **Cloud Deployment trên AWS**
- **EC2** cho ứng dụng
- **RDS** cho database
- **S3** cho storage
- **CloudFront** cho CDN

3. **CI/CD Pipeline**
- **GitHub Actions** cho automation
- **Automated testing**
- **Automated deployment**
- **Environment management**

4. **Monitoring và Logging**
- **CloudWatch** cho monitoring
- **ELK Stack** cho logging
- **Alert system** cho errors

5. **Backup và Recovery**
- **Daily backups**
- **Cross-region replication**
- **Disaster recovery plan**


