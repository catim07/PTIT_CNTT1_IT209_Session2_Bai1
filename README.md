# Session 02 - Bài 1: Khởi tạo Droplet trên DigitalOcean & Xác thực bằng SSH Key

## 1. Mục tiêu
- Thực hành đăng ký tài khoản, lựa chọn cấu hình phần cứng phù hợp và khởi tạo thành công Droplet chạy hệ điều hành Ubuntu 22.04 LTS trên hạ tầng đám mây DigitalOcean.
- Cấu hình xác thực an toàn bằng cặp khóa SSH Keypair thay vì mật khẩu thô và kết nối thành công từ máy cá nhân bằng tài khoản `root`.

## 2. Các bước thực hiện

### Bước 1: Tạo cặp khóa SSH trên máy cá nhân
Chạy lệnh tạo SSH Key bằng thuật toán ed25519:
```bash
ssh-keygen -t ed25519 -C "devops_student@rikkei.edu.vn"
```
Khóa công khai (Public Key) được tạo tại `~/.ssh/id_ed25519.pub`.

### Bước 2: Khởi tạo Droplet trên DigitalOcean Console
- **OS:** Ubuntu 22.04 LTS x64
- **Plan:** Basic ($4/tháng hoặc $6/tháng, Regular SSD, Shared CPU)
- **Datacenter Region:** Singapore (gần Việt Nam nhất)
- **Authentication:** Chọn **SSH Keys**, nhấn **New SSH Key** và dán nội dung tệp `id_ed25519.pub`.
- **Hostname:** `ubuntu-devops-server`

### Bước 3: Đăng nhập thử nghiệm SSH từ máy cá nhân
Chạy lệnh kết nối tới IP Droplet vừa tạo:
```bash
ssh -i ~/.ssh/id_ed25519 root@128.199.200.100
```

## 3. Kết quả kiểm tra
Log Terminal kết nối thành công:
```text
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-105-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

System information as of Sun Oct  4 19:45:00 UTC 2026

System load:  0.0                           Processes:               98
Usage of /:   4.8% of 24.06GB               Users logged in:         0
Memory usage: 12%                           IPv4 address for eth0:   128.199.200.100
Swap usage:   0%

root@ubuntu-devops-server:~# whoami
root
```
Truy cập thành công vào giao diện dòng lệnh của Droplet mà không cần nhập mật khẩu.
