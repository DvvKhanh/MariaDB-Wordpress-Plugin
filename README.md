# MariaDB-Wordpress-Plugin

## Bước 1: Chuẩn bị môi trường
- Bạn cần cài đặt Docker và Docker Compose trên máy tính (Windows, Mac hoặc Linux).
  + Windows/Mac: Tải và cài đặt Docker Desktop.
  + Linux: Chạy lệnh sudo apt install docker-compose.
 
## Bước 2: Tạo tệp cấu hình (Docker Compose)
- Tạo một thư mục mới tên là wordpress_project.
- Sau đó tạo một tệp văn bản tên là docker-compose.yml bên trong thư mục đó với nội dung sau:
```
version: '3.8'

services:
  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
    ports:
      - "9000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wp_data:/var/www/html

volumes:
  db_data:
  wp_data:
```

<img width="621" height="882" alt="image" src="https://github.com/user-attachments/assets/a372bbd0-38d2-4f78-ad57-7ec346263cdc" />

## Bước 3: Khởi chạy hệ thống
- Mở Terminal (hoặc CMD/PowerShell) tại thư mục wordpress_project.
- Chạy lệnh:
```
docker-compose up -d
```

<img width="1471" height="172" alt="image" src="https://github.com/user-attachments/assets/2b0d7a94-c768-4f04-b1b4-640623a2552b" />

- Sau khi chạy lệnh, cần đợi vài phút để Docker tải hình ảnh và khởi động các dịch vụ.

## Bước 4: Cấu hình WordPress (Giao diện Web)

- Mở trình duyệt và truy cập: http://localhost:9000
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/65b9406f-8925-4a62-a31d-b04c7a277b28" />

- Chọn ngôn ngữ: Chọn Tiếng Việt hoặc Tiếng Anh rồi nhấn Tiếp tục.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/4c59591b-1062-423a-9328-e3b7171c8f69" />

- Thiết lập thông tin quản trị và sau đó nhấn Cài đặt WordPress
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/fbc07c12-b71d-41d0-9257-87559cfaa4c3" />

## Bước 5: Cài đặt Plugin

- Đăng nhập thông tin quản trị vừa đăng ký vào Dashboard:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/dfc5eb2e-5bce-4c3b-9555-538ae4a9baaa" />

- Dashboard sau khi đăng nhập:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d6cbac6a-244b-4bd3-a4b6-cbe29f9c61b8" />

- Tìm menu bên trái, chọn Plugin -> Thêm Plugin
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0b71fd62-d320-4e79-9f9f-df4f62db63ad" />

- Tìm và cài đặt một plugin bất kỳ:
  + Đối với em, thì em chọn Classic Editor vì:
    + Đơn giản hóa: Tập trung vào mục tiêu chính là triển khai hệ thống LAMP stack/Docker thay vì cấu hình giao diện.
    + Tính ổn định: Đảm bảo website hoạt động mượt mà trên môi trường container hóa với MariaDB.
    + Kiểm soát tốt: Dễ dàng thao tác với mã nguồn HTML trực tiếp trong bài viết, phục vụ tốt cho việc học tập và kiểm tra dữ liệu trong database.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/84dfde92-a9d4-4e4d-9399-ea73f3b0e2e1" />

- Trong Classic Editor nhấn nút Cài đặt ngay, sau đó nhấn Kích hoạt.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/74982624-85ff-4a1e-a21a-ad9bcb491385" />

