---
title: " Bài giữa kì - Deliverable 3 "
date: "2025-05-12"
updated: "2025-05-12"
categories:
  
  - "Lê Hùng Duy"
coverImage: "/images/logo.png"
coverWidth: 16
coverHeight: 9
excerpt: Ấn để xem thêm...
---


# Tóm tắt Tiến độ Dự án Todo App

## 1. Các Tính Năng Đã Hoàn Thành

1. **Quản lý Task Cơ Bản**
 - Thêm task mới với mô tả và ngày hết hạn
 - Chỉnh sửa task hiện có
 - Xóa task
 - Đánh dấu task đã hoàn thành

2. **Lọc và Tìm Kiếm**
 - Lọc task theo ngày, tuần, tháng
 - Tìm kiếm task theo từ khóa
 - Hiển thị tất cả task

3. **Giao Diện Người Dùng**
 - Thiết kế responsive cho mobile
 - Giao diện hiện đại và thân thiện
 - Sidebar điều hướng
 - Hiệu ứng và animation mượt mà

4. **Lưu Trữ Dữ Liệu**
 - Sử dụng JSON file để lưu trữ task
 - Cơ chế backup dữ liệu
 - Xử lý đồng bộ dữ liệu


### 2. **Phần Đang Phát Triển**

1. **Tính Năng Nâng Cao**
-  Nhắc nhở qua email
-  Chia sẻ task giữa người dùng

2. **Cải Thiện Bảo Mật**
-  JWT authentication
-  Rate limiting
-  Input validation nâng cao
-  Mã hóa dữ liệu nhạy cảm



### 3. **Thử Thách Đã Gặp**

1. **Đồng Bộ Dữ Liệu**
- Vấn đề: Xung đột khi nhiều người dùng cùng chỉnh sửa
- Giải pháp: Implement cơ chế lock và version control

2. **Hiệu Suất**
- Vấn đề: Load chậm khi có nhiều task
- Giải pháp: Implement lazy loading và pagination

3. **UX/UI**
- Vấn đề: Giao diện không thân thiện trên mobile
- Giải pháp: Redesign với responsive design

### Demo hoạt động của hệ thống (hoặc video minh họa)


---

## Mã Nguồn Quan Trọng của Todo App

### 1. Cấu Hình và Khởi Tạo

```python
# Cấu hình cơ bản của ứng dụng
app = Flask(__name__)
app.secret_key = 'your-secret-key-123'

# Cấu hình session
app.config.update(
    SESSION_COOKIE_SECURE=False,
    SESSION_COOKIE_HTTPONLY=True,
    SESSION_COOKIE_SAMESITE='Lax',
    PERMANENT_SESSION_LIFETIME=timedelta(days=1),
    SESSION_REFRESH_EACH_REQUEST=True
)

# Cấu hình CORS để cho phép giao tiếp cross-origin
CORS(app, 
     supports_credentials=True,
     resources={r"/*": {
         "origins": "*",
         "methods": ["GET", "POST", "PUT", "DELETE", "OPTIONS"],
         "allow_headers": ["Content-Type", "Authorization"],
         "expose_headers": ["Content-Type", "Authorization"],
         "supports_credentials": True
     }})
```

**Giải thích:**
- Cấu hình session để bảo mật thông tin người dùng
- CORS được cấu hình để cho phép giao tiếp giữa frontend và backend
- Các header được cấu hình để hỗ trợ authentication

### 2. Xử Lý Database

```python
# Khởi tạo database với xử lý lỗi
try:
    logger.info("Initializing databases...")
    users_db = PupDB('users.db')
    tasks_db = PupDB('tasks.db')
    
    # Khởi tạo database tasks nếu trống
    if not tasks_db.get('tasks'):
        logger.info("Initializing empty tasks database")
        tasks_db.set('tasks', {})
except Exception as e:
    logger.error(f"Error initializing database: {str(e)}")
    logger.error(traceback.format_exc())
    # Tạo file database mới nếu không tồn tại
    users_db = PupDB('users.db')
    tasks_db = PupDB('tasks.db')
    tasks_db.set('tasks', {})
```

**Giải thích:**
- Sử dụng PupDB để lưu trữ dữ liệu
- Có xử lý lỗi khi khởi tạo database
- Tự động tạo database mới nếu không tồn tại

### 3. Xử Lý Authentication

```python
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        email = request.form.get('email')
        password = request.form.get('password')
        
        user = get_user(email)
        if user and check_password_hash(user['password'], password):
            session.clear()  # Xóa session cũ
            session['user_id'] = email
            session.permanent = True
            
            # Tạo response với cookie session
            response = make_response(redirect(url_for('index')))
            response.set_cookie(
                'session',
                session.get('user_id'),
                httponly=True,
                samesite='Lax',
                max_age=86400
            )
            return response
            
        return render_template('login.html', error='Invalid email or password')
    
    return render_template('login.html')
```

**Giải thích:**
- Xử lý đăng nhập với email và password
- Sử dụng password hashing để bảo mật
- Tạo session và cookie an toàn cho người dùng

### 4. API Quản Lý Tasks

```python
@app.route('/api/tasks', methods=['GET'])
def get_tasks():
    if 'user_id' not in session:
        return jsonify({'error': 'Unauthorized'}), 401
    
    try:
        tasks = tasks_db.get('tasks')
        if not tasks:
            return jsonify({})
            
        if not isinstance(tasks, dict):
            tasks = {}
            
        user_tasks = {task_id: task for task_id, task in tasks.items() 
                     if task.get('user_id') == session['user_id']}
        return jsonify(user_tasks)
    except Exception as e:
        logger.error(f"Error getting tasks: {str(e)}")
        return jsonify({})

@app.route('/api/tasks', methods=['POST'])
def add_task():
    if 'user_id' not in session:
        return jsonify({'error': 'Unauthorized'}), 401
    
    try:
        task = request.json
        if not task or 'text' not in task or 'date' not in task:
            return jsonify({'error': 'Invalid task data'}), 400

        tasks = tasks_db.get('tasks')
        if not isinstance(tasks, dict):
            tasks = {}

        task_id = str(int(datetime.now().timestamp() * 1000))
        task['user_id'] = session['user_id']
        tasks[task_id] = task
        tasks_db.set('tasks', tasks)
        
        return jsonify({'id': task_id, **task})
    except Exception as e:
        logger.error(f"Error adding task: {str(e)}")
        return jsonify({'error': 'Internal server error'}), 500
```

**Giải thích:**
- API endpoints cho việc quản lý tasks
- Kiểm tra authentication trước khi thực hiện các thao tác
- Xử lý lỗi và logging đầy đủ
- Tự động gán user_id cho mỗi task

### 5. Xử Lý Lỗi và Logging

```python
# Cấu hình logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

# Middleware xử lý CORS
@app.after_request
def after_request(response):
    response.headers.add('Access-Control-Allow-Credentials', 'true')
    response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization')
    response.headers.add('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE,OPTIONS')
    return response
```

**Giải thích:**
- Sử dụng logging để theo dõi hoạt động của ứng dụng
- Middleware để xử lý CORS headers
- Cấu hình chi tiết cho việc ghi log

### 6. Các Hàm Tiện ích

```python
def get_user(email):
    try:
        user = users_db.get(email)
        if user and 'email' not in user:
            user['email'] = email
            save_user(email, user)
        return user
    except Exception as e:
        logger.error(f"Error getting user: {str(e)}")
        return None

def get_user_tasks(user_id):
    try:
        tasks = tasks_db.get('tasks', {})
        return {task_id: task for task_id, task in tasks.items() 
                if task.get('user_id') == user_id}
    except Exception as e:
        logger.error(f"Error getting user tasks: {str(e)}")
        return {}
```

**Giải thích:**
- Các hàm tiện ích để xử lý dữ liệu người dùng và tasks
- Có xử lý lỗi và logging
- Tự động cập nhật dữ liệu nếu thiếu thông tin




## 5. Kế Hoạch Tiếp Theo

1. **Chuyển Lên Cloud**
- Triển khai trên AWS
- Sử dụng Docker và Kubernetes
- Tự động hóa CI/CD


2. **Tính Năng Mới**
- Chia sẻ và cộng tác task
- Quản lý task nâng cao (subtasks, dependencies)
- Báo cáo và thống kê

3. **Kiểm thử toàn bộ hệ thống**
- Đảm bảo hệ thống hoạt động ổn định khi triển khai thật

4. **Xử lý đồng bộ dữ liệu**

- Đảm bảo dữ liệu cập nhật realtime khi thêm/sửa/xóa.