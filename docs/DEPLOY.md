## Triển Khai Ứng Dụng React trên Môi Trường Ubuntu
### Cài đặt cơ bản
#### Bước 1: Cài Đặt Node.js và npm

```bash
sudo apt update
sudo apt install nodejs
sudo apt install npm
```
#### Bước 2: Chuẩn Bị Mã Nguồn Ứng Dụng React
```bash
git clone <URL_repository>
cd <tên_thư_mục>
npm install
```
#### Bước 3: Cấu Hình và Build Ứng Dụng React
```bash
npm run build
```
#### Bước 4: Cấu Hình Web Server (Nginx)
```bash
sudo apt install nginx
```
Tạo một file cấu hình mới trong /etc/nginx/sites-available/ (ví dụ: myapp):

```nginx
server {
    listen 80;
    server_name example.com; # Tên miền hoặc IP của bạn

    location / {
        root /path/to/your/app/build; # Đường dẫn đến thư mục build của ứng dụng React
        index index.html;
        try_files $uri $uri/ /index.html;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }
}
```

Kích hoạt cấu hình và khởi động lại Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```
#### Bước 5: Cấu Hình Firewall (nếu cần thiết)
```bash
sudo ufw allow 'Nginx HTTP'
```
#### Bước 6: Kiểm Tra và Debug
```bash
sudo nginx -t
sudo tail -f /var/log/nginx/error.log
```
#### Lưu ý
Đảm bảo rằng bạn đã cấu hình Nginx đúng cách để phục vụ các tệp tin từ thư mục build của ứng dụng React.
Nếu ứng dụng React của bạn yêu cầu kết nối với backend, đảm bảo cấu hình đúng endpoint trong file cấu hình của bạn.

### Quản lý sevice thông qua PM2 (options)
Cài đặt và chạy app.
```bash
sudo npm install -g pm2
pm2 start npm --name "my-app" -- start
```
Kiểm tra danh sách pm2
```sh
pm2 list
```
Stop app pm2
```sh
pm2 stop <app_name_or_id>
```
Xóa app pm2
```sh
pm2 delete <app_name_or_id>
```

### Tạo ssl sử dụng cerbot
Cài đặt
```sh
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt update
sudo apt install certbot python3-certbot-nginx
```
Tự động gia hạn SSL
```sh
sudo crontab -e
```
Bổ sung file cron
```sh
0 0 1 * * certbot renew --quiet
```