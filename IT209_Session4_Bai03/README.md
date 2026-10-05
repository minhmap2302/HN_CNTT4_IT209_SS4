# Session 04 - Bài 3: Cấu hình xác thực SSH và Đẩy dự án lên GitHub

## 1. Mục tiêu
- Khởi tạo cặp khóa SSH bảo mật bằng thuật toán Ed25519.
- Cấu hình liên kết an toàn giữa repository cục bộ với GitHub.
- Đẩy (push) mã nguồn thành công lên GitHub bằng giao thức SSH.

## 2. Các bước thực hiện

### Bước 1: Tạo cặp khóa SSH Ed25519
```bash
ssh-keygen -t ed25519 -C "duydoan@gmail.com"
```
**Kết quả:**
```text
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/devops/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Your identification has been saved in /home/devops/.ssh/id_ed25519
Your public key has been saved in /home/devops/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:xYz1234abcDefGhI5678jKlMnOpQrSt duydoan@gmail.com
```

### Bước 2: Thêm SSH Public Key vào GitHub
```bash
cat ~/.ssh/id_ed25519.pub
```
Copy nội dung Public Key, truy cập **GitHub** → **Settings** → **SSH and GPG keys** → **New SSH key** → Dán Public Key → Nhấn **Add SSH key**.

### Bước 3: Kiểm tra kết nối SSH tới GitHub
```bash
ssh -T git@github.com
```
**Kết quả:**
```text
Hi duydoan169! You've successfully authenticated, but GitHub does not provide shell access.
```

### Bước 4: Liên kết Remote Repository bằng SSH
```bash
git remote add origin git@github.com:duydoan169/IT209_Session4_Bai03.git
```

### Bước 5: Push mã nguồn lên GitHub
```bash
git push -u origin main
```
**Kết quả:**
```text
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
To git@github.com:duydoan169/IT209_Session4_Bai03.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

## 3. Kết quả kiểm tra

### Kiểm tra kết nối SSH:
```bash
ssh -T git@github.com
```
```text
Hi duydoan169! You've successfully authenticated, but GitHub does not provide shell access.
```

### Kiểm tra remote URL:
```bash
git remote -v
```
```text
origin  git@github.com:duydoan169/IT209_Session4_Bai03.git (fetch)
origin  git@github.com:duydoan169/IT209_Session4_Bai03.git (push)
```
Đường dẫn remote URL có dạng SSH `git@github.com:username/repository.git`, xác nhận cấu hình thành công.