# MariaDB-Wordpress-Plugin
# Giới thiệu
- Dự án xây dựng website sử dụng WordPress kết hợp với MariaDB.
- WordPress đảm nhiệm phần giao diện và quản lý nội dung, trong khi MariaDB lưu trữ toàn bộ dữ liệu. Hệ thống có thể mở rộng thông qua plugin để bổ sung các chức năng cần thiết.

# Mục tiêu
- Xây dựng website động hoàn chỉnh.
- Kết nối WordPress với MariaDB.
- Triển khai nhanh bằng Docker.
- Tìm hiểu cách cài đặt và sử dụng plugin.

# Công nghệ sử dụng
- WordPress (PHP, CMS).
- MariaDB (Database).
- Docker & Docker Compose.

# Nguyên lý hoạt động
- Người dùng truy cập website.
- WordPress xử lý yêu cầu (PHP).
- Gửi truy vấn đến MariaDB.
- MariaDB trả dữ liệu.
- WordPress hiển thị kết quả.

# Plugin
- Plugin giúp mở rộng chức năng mà không cần sửa code.
- Một số plugin phổ biến:
  + Elementor (thiết kế giao diện)
  + Yoast SEO (tối ưu SEO)
  + Contact Form 7 (form liên hệ)

## Bước 1: Chuẩn bị môi trường
- Bạn cần cài đặt Docker và Docker Compose trên máy tính (Windows, Mac hoặc Linux).
  + Windows/Mac: Tải và cài đặt Docker Desktop.
  + Linux: Chạy lệnh sudo apt install docker-compose.
 
- Kiểm tra phiên bản Docker-compose và Docker
```
docker-compose --version
docker --version
```
<img width="684" height="118" alt="image" src="https://github.com/user-attachments/assets/35439eea-ebb8-4220-92a9-940b2db805f0" />

## Bước 2: Tạo thư mục project
- Gõ lệnh:
```
mkdir wordpress_lab
cd wordpress_lab
```

<img width="441" height="79" alt="image" src="https://github.com/user-attachments/assets/35ffdc50-8ccb-4acb-9835-b93bbd526544" />

## Bước 3: Tạo file cấu hình
- Gõ lệnh:```nano docker-compose.yml```
- Nội dung file docker-compose.yml
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
<img width="1478" height="752" alt="image" src="https://github.com/user-attachments/assets/b70a756a-b073-46a1-823e-bbdf876d98d5" />

## Bước 4: Khởi chạy hệ thống
- Chạy lệnh:
```
sudo docker-compose up -d
```
<img width="984" height="655" alt="image" src="https://github.com/user-attachments/assets/89a9d11a-8a6b-4a1b-9124-8955ca95e79d" />

- Sau khi chạy lệnh, cần đợi vài phút để Docker tải hình ảnh và khởi động các dịch vụ.

## Bước 5: Kiểm tra container
- Gõ lệnh:```sudo docker ps```
<img width="1464" height="165" alt="image" src="https://github.com/user-attachments/assets/31c2cae3-3f65-4d71-ba73-d899362cab95" />

## Bước 6: Cấu hình WordPress (Giao diện Web)
- Lấy ip: ```ip a```
<img width="1259" height="631" alt="image" src="https://github.com/user-attachments/assets/593ff72b-70d4-4dff-9c7d-7e3b16520fdc" />

- Mở trình duyệt và truy cập: http://192.168.91.154:9000/
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/64b9a529-255d-4b68-9bda-c0c2beb28094" />

- Chọn ngôn ngữ: Chọn Tiếng Việt hoặc Tiếng Anh rồi nhấn Tiếp tục.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/9369a653-da96-444d-8e29-f1d18aba7edb" />

- Thiết lập thông tin quản trị và sau đó nhấn Cài đặt WordPress
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/5cb9cb50-04f8-4f2c-bf91-eed5b8744f2b" />

## Bước 7: Cài đặt Plugin
- Đăng nhập thông tin quản trị vừa đăng ký vào Dashboard:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/1a3b0d51-4e0f-4c40-8e7d-f0625df90c53" />

- Dashboard sau khi đăng nhập:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/78feb336-3a0f-49d4-9cf6-08b8c5686712" />

- Tìm menu bên trái, chọn Plugin -> Thêm Plugin
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/ae9e5132-5d01-4580-b28d-a93724010ed1" />

- Tìm và cài đặt một plugin bất kỳ:
  + Đối với em, thì em chọn Classic Editor vì:
    + Đơn giản hóa: Tập trung vào mục tiêu chính là triển khai hệ thống LAMP stack/Docker thay vì cấu hình giao diện.
    + Tính ổn định: Đảm bảo website hoạt động mượt mà trên môi trường container hóa với MariaDB.
    + Kiểm soát tốt: Dễ dàng thao tác với mã nguồn HTML trực tiếp trong bài viết, phục vụ tốt cho việc học tập và kiểm tra dữ liệu trong database.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c7c08e62-30c5-447e-982d-d69794e9e278" />

- Trong Classic Editor nhấn nút Cài đặt ngay, sau đó nhấn Kích hoạt.
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/8c7d05ef-5e7f-4ea9-9614-04679bf12585" />

## Kiểm tra quyền quản trị và viết bài mới
- Vì em đã chọn Classic Editor để kiểm soát tốt mã nguồn HTML, nên em sẽ kiểm tra xem nó đã thay đổi giao diện soạn thảo chưa:
  + Truy cập Dashboard: truy cập địa chỉ http://192.168.91.154:9000/wp-admin
  + Tạo nội dung: Chọn menu Bài viết (Posts) -> Thêm bài viết -> Xuất bản -> Cập nhật

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/190af4d8-2a43-4d1d-8e2a-fbeb35cd001d" />

## Kiểm tra hiển thị thực tế
- Truy cập đường link: http://192.168.91.154:9000/
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f4a49682-15c0-4315-a24f-3c0d8f088178" />

## Chỉnh sửa giao diện bài viết
- Truy cập địa chỉ http://192.168.91.154:9000/wp-admin
- Chọn Giao diện -> Sửa giao diện
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/a61f3788-420a-4a94-8025-61bc9caa8455" />

- Chèn thêm ảnh vào giao diện bài viết -> nhấn lưu thay đổi
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/345ac80c-d518-4115-8f41-c72a9864d987" />

- Kết quả sau khi chỉnh sửa giao diện:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f7b45351-dede-42d9-ba47-564efb6de2f2" />
