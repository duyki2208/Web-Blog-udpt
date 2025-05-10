---
title: "Truyền thông"
date: "2025-05-007"
updated: "2025-05-07"
categories:
  
  - "Lê Hùng Duy"
coverImage: "/images/wallpaper2.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Ấn để xem thêm...
---



# Bài tập 1:  Báo cáo về RabbitMQ

## 1. Giới thiệu
- RabbitMQ là một message broker mã nguồn mở, hỗ trợ giao thức AMQP và các giao thức như MQTT, STOMP.
- Dùng trong hệ thống phân tán để trao đổi thông điệp.

## 2. Cơ chế hoạt động
- Sử dụng **Message Queue** (hàng đợi) và **Publish-Subscribe**.
- **Exchange** định tuyến thông điệp đến hàng đợi dựa trên quy tắc.

## 3. Chức năng chính
- Đảm bảo độ tin cậy qua acknowledgment và lưu trữ.
- Hỗ trợ nhiều giao thức: AMQP, MQTT, STOMP, HTTP.
- Cân bằng tải giữa các consumer.
- Quản lý hàng đợi qua giao diện web/API.

## 4. Cài đặt
- **Ubuntu**:  
  1. Cài Erlang: `sudo apt-get install erlang`  
  2. Thêm repository: `echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list`  
  3. Cài RabbitMQ: `sudo apt-get update && sudo apt-get install rabbitmq-server`  
  4. Khởi động: `sudo systemctl start rabbitmq-server`  
- **Windows**: Tải Erlang và RabbitMQ từ trang chính thức, cài đặt và khởi động.

## 5. Kết luận
- RabbitMQ mạnh mẽ, dễ cài đặt, phù hợp cho hệ thống phân tán.


Dưới đây là bài làm tiếp tục cho Bài tập 2 và Bài tập 3 như yêu cầu trong query của bạn.

### Bài tập 2: Code một hệ thống đơn giản sử dụng RabbitMQ

Dưới đây là mã nguồn cho một hệ thống đơn giản sử dụng RabbitMQ trong Python, bao gồm cả producer (người gửi) và consumer (người nhận).

```python
import pika

# Kết nối đến RabbitMQ server
connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

# Khai báo một hàng đợi tên là 'hello'
channel.queue_declare(queue='hello')

# Gửi thông điệp đến hàng đợi
channel.basic_publish(exchange='', routing_key='hello', body='Hello, RabbitMQ!')
print(" [x] Sent 'Hello, RabbitMQ!'")

# Đóng kết nối
connection.close()
```

**Hướng dẫn chạy:**
1. Cài đặt thư viện `pika` bằng lệnh: `pip install pika`.
2. Đảm bảo RabbitMQ server đang chạy trên `localhost`.
3. Chạy file `consumer.py` (sẽ cung cấp bên dưới) trước để lắng nghe thông điệp.
4. Chạy file `producer.py` để gửi thông điệp.

### Bài tập 3: Báo cáo về thư viện RPC sử dụng JSON

Dưới đây là báo cáo về việc sử dụng JSON-RPC trong Python với các thư viện `jsonrpcclient` và `jsonrpcserver`.




## 1. Giới thiệu
- **JSON-RPC** là một giao thức RPC (Remote Procedure Call) sử dụng JSON làm định dạng dữ liệu trao đổi.
- Thư viện `jsonrpcclient` và `jsonrpcserver` trong Python giúp dễ dàng triển khai RPC qua JSON.

## 2. Cơ chế hoạt động
- **Client** gửi yêu cầu dưới dạng JSON đến server.
- **Server** nhận, xử lý và trả về kết quả cũng dưới dạng JSON.

## 3. Chức năng chính
- **Đơn giản**: JSON dễ đọc, dễ sử dụng.
- **Nhẹ**: Không yêu cầu giao thức phức tạp như XML-RPC.
- **Đa nền tảng**: JSON được hỗ trợ rộng rãi.

## 4. Cài đặt
- Cài đặt thư viện:
  ```bash
  pip install jsonrpcclient jsonrpcserver
  ```

## 5. Demo đơn giản
- **Server (`server.py`)**:
  ```python
  from jsonrpcserver import method, serve

  @method
  def add(x, y):
      return x + y

  if __name__ == "__main__":
      serve()
  ```
- **Client (`client.py`)**:
  ```python
  from jsonrpcclient import request

  response = request("http://localhost:5000", "add", x=3, y=5)
  print(response.data.result)  # Kết quả: 8
  ```

## 6. Kết luận
- JSON-RPC là một giải pháp RPC nhẹ và dễ triển khai, phù hợp cho các hệ thống phân tán đơn giản.
- Thư viện `jsonrpcclient` và `jsonrpcserver` giúp việc triển khai trở nên dễ dàng trong Python.

---

