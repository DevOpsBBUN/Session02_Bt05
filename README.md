# Bài 5: Quản lý quyền sở hữu thư mục Web (Directory Permission Management)

## Các lệnh đã thực thi

### 1. Thay đổi chủ sở hữu và nhóm sở hữu
Thay đổi chủ sở hữu (owner) của thư mục thành user `devops` và nhóm (group) sở hữu thành nhóm `www-data` (nhóm chạy dịch vụ Nginx) cho toàn bộ thư mục `/var/www/ptit-web/`:
```bash
sudo chown -R devops:www-data /var/www/ptit-web/
```

### 2. Thiết lập quyền truy cập (chmod)
Thiết lập quyền thư mục web tĩnh:
- Chủ sở hữu (devops) có quyền đọc, ghi, thực thi.
- Nhóm sở hữu (www-data) có quyền đọc, thực thi.
- Những người khác có quyền đọc, thực thi.

```bash
# Đặt quyền cho thư mục (755: rwxr-xr-x)
sudo find /var/www/ptit-web/ -type d -exec chmod 755 {} \;

# Đặt quyền cho các file bên trong (644: rw-r--r--)
sudo find /var/www/ptit-web/ -type f -exec chmod 644 {} \;
```
Với thiết lập này: 
- User `devops` có quyền ghi trực tiếp vào file.
- Nginx chạy quyền group `www-data` có quyền đọc file và không bị lỗi `403 Forbidden`.

### 3. Kiểm tra phân quyền
```bash
ls -la /var/www/ptit-web/
```

**Kết quả đầu ra của lệnh `ls -la /var/www/ptit-web/`:**
```text
[Học viên chèn kết quả đầu ra của lệnh ls -la tại đây]
```

## Kiểm tra ghi file bằng user devops
Đăng nhập vào hệ thống bằng tài khoản `devops` và thử chạy lệnh chỉnh sửa file:
```bash
echo "Update" >> /var/www/ptit-web/html/index.html
```

**Các bước kiểm tra ghi file từ user devops (Log Terminal):**
```text
[Học viên chèn log terminal quá trình ghi file thành công bằng user thường (không có sudo) tại đây]
```
