---
title: " Bài giữa kì"
date: "2025-05-12"
updated: "2025-05-12"
categories:
  
  - "Lê Hùng Duy"
coverImage: "/images/logo.png"
coverWidth: 16
coverHeight: 9
excerpt: Ấn để xem thêm...
---


## 1. Phân tích thư viện PupDB

**PupDB** là một thư viện cơ sở dữ liệu key-value dựa trên tệp, được viết bằng Python, nhằm cung cấp một hệ thống lưu trữ dữ liệu NoSQL đơn giản với API dễ sử dụng. Mục đích chính của PupDB là:
- **Lưu trữ dữ liệu đơn giản**: Cung cấp một cơ sở dữ liệu nhẹ, lưu trữ dữ liệu dưới dạng key-value trong tệp JSON, không yêu cầu cài đặt server phức tạp.
- **API tối giản**: Giao diện tương tự như dictionary trong Python, giúp lập trình viên dễ dàng lưu và truy xuất dữ liệu.
- **Hỗ trợ đa ngôn ngữ**: Cung cấp giao diện HTTP/REST, cho phép sử dụng PupDB từ các ngôn ngữ lập trình khác ngoài Python.
- **Hỗ trợ đa tiến trình và đa luồng**: Cho phép truy cập đồng thời từ nhiều tiến trình hoặc luồng với các instance PupDB riêng biệt.

### PupDB có thể giải quyết vấn đề gì?
- **Lưu trữ dữ liệu cho ứng dụng nhỏ**: Lưu trữ cài đặt, dữ liệu người dùng, hoặc dữ liệu tạm thời trong các dự án không cần cơ sở dữ liệu phức tạp.
- **Prototyping nhanh**: Giúp lập trình viên xây dựng ứng dụng thử nghiệm mà không cần thiết lập cơ sở dữ liệu như MongoDB hay SQLite.
- **Tích hợp đa ngôn ngữ**: Thông qua giao diện REST, PupDB có thể được sử dụng trong các dự án sử dụng Java, PHP, hoặc bất kỳ ngôn ngữ nào hỗ trợ HTTP.
- **Quản lý dữ liệu cục bộ**: Phù hợp cho các ứng dụng desktop (như ứng dụng Electron) hoặc các công cụ CLI cần lưu trữ dữ liệu nhẹ.

### Điểm mạnh
- **Đơn giản và nhẹ**: PupDB dễ cài đặt (`pip install pupdb`) và không yêu cầu cấu hình server, lý tưởng cho các dự án nhỏ.
- **API dễ sử dụng**: Cung cấp các phương thức như `set()`, `get()`, `remove()`, `keys()`, giống cách hoạt động của dictionary Python.
- **Hỗ trợ đa tiến trình/luồng**: Cho phép truy cập đồng thời từ nhiều tiến trình hoặc luồng với các instance riêng biệt.
- **Giao diện REST**: Cho phép sử dụng PupDB qua HTTP, mở rộng khả năng tích hợp với các ngôn ngữ khác.
- **Mã nguồn mở**: Được cấp phép dưới MIT License, có thể tùy chỉnh và sử dụng miễn phí.
### Điểm yếu
- **Không phù hợp với dữ liệu lớn**: PupDB không được thiết kế cho cơ sở dữ liệu lớn hơn vài megabyte do đọc/ghi tệp JSON chậm.
- **Thiếu tính năng nâng cao**: Không hỗ trợ lập chỉ mục (indexing), phân vùng (partitioning), hoặc truy vấn phức tạp.
- **Hiệu suất I/O thấp**: Mỗi thao tác `set()` ghi trực tiếp vào tệp, gây tốn I/O, đặc biệt khi có nhiều thao tác ghi.
- **Không đồng bộ dữ liệu tức thời**: Dữ liệu trong bộ nhớ có thể không đồng bộ với tệp nếu tệp bị sửa đổi bởi tiến trình khác trong các thao tác dài.
- **Hỗ trợ cộng đồng hạn chế**: Với chỉ 82 stars trên GitHub và một số vấn đề mở (open issues), PupDB có cộng đồng nhỏ, ít được cập nhật thường xuyên.

### So sánh với các thư viện/framework khác
- **So với TinyDB**: TinyDB cũng là cơ sở dữ liệu key-value dựa trên JSON, nhưng hỗ trợ truy vấn phức tạp hơn (giống MongoDB). PupDB có lợi thế với giao diện REST và hỗ trợ đa tiến trình/luồng, nhưng TinyDB có cộng đồng lớn hơn và hiệu suất I/O tốt hơn nhờ cơ chế caching.
- **So với SQLite**: SQLite là cơ sở dữ liệu quan hệ mạnh mẽ, hỗ trợ SQL và phù hợp với dữ liệu lớn hơn. PupDB đơn giản hơn nhưng không có tính năng truy vấn phức tạp như SQLite.
- **So với MongoDB**: MongoDB là cơ sở dữ liệu NoSQL đầy đủ, phù hợp cho ứng dụng lớn, nhưng yêu cầu server và cấu hình phức tạp. PupDB nhẹ hơn và phù hợp với các dự án nhỏ không cần server.
### Ứng dụng của PupDB
- **Ứng dụng CLI hoặc desktop**: Lưu trữ cấu hình, lịch sử lệnh, hoặc dữ liệu người dùng trong các công cụ CLI hoặc ứng dụng Electron.
- **Prototyping**: Xây dựng nhanh API hoặc ứng dụng thử nghiệm cần lưu trữ dữ liệu tạm thời.
- **Ứng dụng đa ngôn ngữ**: Sử dụng giao diện REST để lưu trữ dữ liệu từ các ứng dụng Java, PHP, hoặc JavaScript.
- **Ứng dụng học tập**: Phù hợp cho sinh viên học về quản lý dữ liệu hoặc xây dựng ứng dụng nhỏ.
- **Quản lý dữ liệu cục bộ**: Lưu trữ danh sách công việc, ghi chú, hoặc dữ liệu nhỏ trong các dự án không cần cơ sở dữ liệu phức tạp.


---

# Kế hoạch bài giữa kỳ: Ứng dụng Quản lý Danh sách Công việc với PupDB

## 1. Mô tả bài toán
Xây dựng một ứng dụng dòng lệnh (CLI) bằng Python sử dụng PupDB để quản lý danh sách công việc. Ứng dụng sẽ có các chức năng:
- Thêm, xóa, và chỉnh sửa công việc (mỗi công việc có ID, tiêu đề, trạng thái hoàn thành).
- Tìm kiếm công việc theo tiêu đề.
- Hiển thị danh sách công việc.
- Lưu trữ dữ liệu trong tệp JSON bằng PupDB.
- (Tùy chọn) Tích hợp REST API để truy cập danh sách công việc từ các ứng dụng khác.

### Mục tiêu
- Thể hiện khả năng sử dụng PupDB để lưu trữ và truy xuất dữ liệu key-value.
- Xây dựng một ứng dụng CLI thân thiện với người dùng.
- Đảm bảo dữ liệu được lưu trữ an toàn trong tệp JSON.
- Tạo mã nguồn sạch và báo cáo chi tiết.

## 2. Kế hoạch thực hiện
### Tuần 1: Nghiên cứu và thiết kế
- **Mục tiêu**: Hiểu PupDB, thiết kế cấu trúc dữ liệu, và lên kế hoạch phát triển.
- **Công việc**:
  - Nghiên cứu PupDB (các phương thức set, get, remove, keys) và giao diện REST.
  - Thiết kế cấu trúc dữ liệu: mỗi công việc là một cặp key-value (key là ID, value là `{title, completed}`).
  - Chuẩn bị môi trường: Cài đặt Python, PupDB (`pip install pupdb`), và `inquirer` cho CLI.
  - Lên kế hoạch giao diện CLI với menu tương tác.
- **Kết quả**: Cấu trúc dữ liệu và môi trường phát triển sẵn sàng.

### Tuần 2: Phát triển core functionality
- **Mục tiêu**: Xây dựng các chức năng chính của ứng dụng.
- **Công việc**:
  - Viết hàm thêm, xóa, và chỉnh sửa công việc bằng PupDB (`set`, `remove`).
  - Sử dụng PupDB để lưu trữ danh sách công việc trong tệp JSON.
  - Xây dựng chức năng hiển thị danh sách công việc (`keys`, `get`).
  - Tích hợp `inquirer` để tạo giao diện CLI tương tác.
- **Kết quả**: Ứng dụng có thể thêm, xóa, chỉnh sửa, và hiển thị công việc.

### Tuần 3: Hoàn thiện tính năng và giao diện
- **Mục tiêu**: Thêm chức năng tìm kiếm và cải thiện trải nghiệm người dùng.
- **Công việc**:
  - Thêm chức năng tìm kiếm công việc theo tiêu đề (lặp qua `keys` và kiểm tra `get`).
  - Xử lý lỗi (ví dụ: ID trùng lặp, công việc không tồn tại).
  - Cải thiện giao diện CLI với menu rõ ràng và thông báo lỗi.
  - (Tùy chọn) Tích hợp REST API bằng `pupdb.server` để truy cập công việc qua HTTP.
- **Kết quả**: Ứng dụng hoàn chỉnh với đầy đủ tính năng và giao diện thân thiện.

### Tuần 4: Kiểm thử và nộp bài
- **Mục tiêu**: Đảm bảo ứng dụng hoạt động ổn định và chuẩn bị báo cáo.
- **Công việc**:
  - Kiểm thử ứng dụng với các trường hợp (thêm nhiều công việc, tìm kiếm, xóa).
  - Viết báo cáo mô tả bài toán, cách triển khai, thách thức, và bài học rút ra.
  - Đóng gói mã nguồn và nộp bài.
- **Kết quả**: Ứng dụng hoàn thiện, báo cáo chi tiết, và nộp đúng hạn.

## 3. Công nghệ sử dụng
- **PupDB**: Quản lý và lưu trữ dữ liệu công việc trong tệp JSON.
- **Python**: Ngôn ngữ lập trình chính.
- **Inquirer**: Tạo giao diện dòng lệnh tương tác.
- **Flask/Gunicorn** (tùy chọn): Tích hợp REST API của PupDB.

## 4. Kết quả mong đợi
- Một ứng dụng CLI quản lý công việc, chạy mượt mà trên Python.
- Dữ liệu công việc được lưu trữ an toàn trong tệp JSON.
- Mã nguồn sạch, có chú thích rõ ràng, và dễ bảo trì.
- Báo cáo chi tiết giải thích cách triển khai và các bài học rút ra.

## 5. Rủi ro và giải pháp
- **Rủi ro**: Tệp JSON bị hỏng do lỗi ghi dữ liệu.
  - **Giải pháp**: Thêm kiểm tra dữ liệu trước khi ghi và sao lưu tệp JSON.
- **Rủi ro**: Hiệu suất chậm khi danh sách công việc lớn.
  - **Giải pháp**: Giới hạn số lượng công việc trong bài toán (vài chục công việc).
- **Rủi ro**: Giao diện CLI khó sử dụng.
  - **Giải pháp**: Sử dụng Inquirer để tạo menu tương tác thân thiện.
---